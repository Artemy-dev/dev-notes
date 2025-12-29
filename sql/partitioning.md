# Партиционирование больших таблиц

**Партиционирование** - это разделение одной большой таблицы в базе данных на несколько меньших частей (**партиций**) по определённому правилу.

**Представьте себе огромное хранилище документов:**

- **Без партиционирования:** Все документы свалены в одну стопку. Чтобы найти документ за 2024 год, нужно перерыть всё.
- **С партиционированием:** Документы разложены по папкам по годам: "2023", "2024", "2025". Нужный документ ищется только в одной папке.

**Технически** - это всё ещё одна логическая таблица для приложения, но физически данные хранятся отдельно.

---

## Для чего применяется?

| **Проблема**	| **Решение через партиционирование** |
|-----------|---------------------------------|
| Медленные запросы в огромной таблице | Запрос обрабатывает не всю таблицу, а только нужную часть (партицию) |
| Сложность управления старыми данными | Старые партиции можно быстро архивировать или удалять (`DROP PARTITION`) |
| Нагрузка на диск | Можно хранить редкоиспользуемые партиции на HDD, а активные на SSD |

**Основные типы партиционирования:**

- **По диапазону (RANGE):** По дате (created_at), по цифровому диапазону (user_id)
- **По списку (LIST):** По регионам (region_id), по типам (order_type)

---

## Пример "большой" таблицы

Допустим, у нас таблица заказов интернет-магазина, которая выросла до 100+ миллионов строк:

| id |	user_id |	amount |	status |	created_at |
|---|---|---|---|---|
| 1 |	42 |	1499.99 |	'completed' |	'2023-01-15 12:30:00' |
| ... |	... |	... |	... |	... |
| 500000 |	18 |	599.50 |	'pending' |	'2024-08-21 18:15:22' |
| ... |	... |	... |	... |	... |
| 1000000 |	921 |	1899.00 |	'completed' |	'2025-03-09 09:05:33' |


```sql
CREATE TABLE orders (
    id BIGSERIAL PRIMARY KEY,
    user_id INTEGER NOT NULL,
    amount DECIMAL(10,2),
    status VARCHAR(50),
    created_at TIMESTAMP DEFAULT NOW()
);
```

**Проблемные запросы:**

```sql
SELECT * FROM orders WHERE created_at BETWEEN '2024-01-01' AND '2024-03-01';
```

- Полное сканирование таблицы

```sql
DELETE FROM orders WHERE created_at < '2024-01-01';
```

- Долгая операция с высокой нагрузкой
- Возможны блокировки
- Запрос может быть прерван по таймауту

---

## Пример партиционирования по годам

Вместо одной монолитной таблицы **orders** используем партиционирование по годам на основе даты создания заказа.

```text
orders (логическая таблица)
├── orders_2023 (партиция за 2023 год)
├── orders_2024 (партиция за 2024 год)
├── orders_2025 (партиция за 2025 год)
└── orders_default (партиция по умолчанию)
```

Все заказы за 2023 год автоматически попадают в orders_2023, за 2024 в orders_2024 и т.д.

---

## SQL-запросы для миграции (PostgreSQL)

### Шаг 1. Создание основной таблицы

```sql
CREATE TABLE orders_new (
    id          BIGSERIAL NOT NULL,
    user_id     INTEGER NOT NULL,
    amount      NUMERIC(10,2) NOT NULL,
    status      VARCHAR(50) NOT NULL,
    created_at  TIMESTAMPTZ NOT NULL DEFAULT NOW(),

    -- PRIMARY KEY обязан включать ключ партиционирования
    PRIMARY KEY (id, created_at)
) PARTITION BY RANGE (created_at);
```

- BIGSERIAL - автоматический счётчик для чисел (до ~9 квинтиллионов)
- TIMESTAMPTZ - безопасно для часовых поясов
- PRIMARY KEY (id, created_at) - требование PostgreSQL (начиная с PostgreSQL 11+)
- BIGSERIAL - единая sequence на все партиции
- sequence - счётчик, который выдаёт числа

### Шаг 2. Создание годовых партиций

```sql
CREATE TABLE orders_2023 PARTITION OF orders_new
FOR VALUES FROM (DATE '2023-01-01') TO (DATE '2024-01-01');

CREATE TABLE orders_2024 PARTITION OF orders_new
FOR VALUES FROM (DATE '2024-01-01') TO (DATE '2025-01-01');

CREATE TABLE orders_2025 PARTITION OF orders_new
FOR VALUES FROM (DATE '2025-01-01') TO (DATE '2026-01-01');
```

### Шаг 3. DEFAULT-партиция

```sql
CREATE TABLE orders_default PARTITION OF orders_new DEFAULT;
```

- защищает от падения INSERT
- ловит ошибки в данных
- принимает строки, не попавшие ни в одну явную партицию (в том числе данные за будущие периоды)

### Шаг 4. Индексы

Индексы не наследуются автоматически, поэтому создаём их на родительской таблице.

```sql
-- Индексы создаются на родительской таблице
CREATE INDEX idx_orders_user_id ON orders_new (user_id);
CREATE INDEX idx_orders_created_at ON orders_new (created_at);
CREATE INDEX idx_orders_status ON orders_new (status);
```

PostgreSQL создаст соответствующие индексы на всех партициях.

### Шаг 5. Перенос данных из старой таблицы

```sql
INSERT INTO orders_new (id, user_id, amount, status, created_at)
SELECT id, user_id, amount, status, created_at
FROM orders;
```

PostgreSQL сам разложит строки по нужным партициям.

### Шаг 6. Проверка распределения данных

```sql
SELECT
    tableoid::regclass AS partition_name,
    COUNT(*)           AS row_count
FROM orders_new
GROUP BY tableoid
ORDER BY partition_name;
```

### Шаг 7. Атомарная замена таблицы

```sql
BEGIN;

ALTER TABLE orders RENAME TO orders_old;
ALTER TABLE orders_new RENAME TO orders;

COMMIT;
```

### Шаг 8. Обновление sequence

После ручной вставки данных необходимо синхронизировать sequence:

```sql
SELECT setval(
    pg_get_serial_sequence('orders', 'id'),
    (SELECT MAX(id) FROM orders)
);
```

### Шаг 9. Очистка (после проверки)

```sql
-- После того как убедились, что всё работает
DROP TABLE orders_old;
```

`CASCADE` не используем - можно снести зависимости.

### Шаг 10. Создание будущей партиции заранее

```sql
CREATE TABLE orders_2026 PARTITION OF orders
FOR VALUES FROM (DATE '2026-01-01') TO (DATE '2027-01-01');
```
