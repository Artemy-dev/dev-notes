# **Cheat Sheet** по основным терминам и запросам **SQL** — от создания таблиц до выборки и объединения данных

## Основные термины SQL

**Database (база данных)** — *Место хранения структурированных данных. Может содержать множество таблиц.*

**Table (таблица)** — *Структура для хранения данных в виде строк и столбцов.*

**Row (строка, запись)** — *Одна запись в таблице.*

**Column (столбец, поле)** — *Атрибут данных, определяющий тип информации.*

**Primary Key (первичный ключ)** — *Уникальный идентификатор записи в таблице.*

**Foreign Key (внешний ключ)** — *Поле, которое ссылается на первичный ключ другой таблицы, для связи данных.*

**Index (индекс)** — *Структура для ускорения поиска данных.*

**Query (запрос)** — *Команда для работы с данными (выборка, вставка, обновление, удаление).*

## Основные запросы SQL для junior/middle разработчика

### CREATE TABLE

**Описание:** Создаёт новую таблицу с указанными полями.

**Пример:**

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    age INT
);
```

```cmd
| id       | first_name | last_name | age      |
| -------- | ---------- | --------- | -------- |
| *пусто*  | *пусто*    | *пусто*   | *пусто*  |
```

(Таблица создана, данных ещё нет)

### INSERT

**Описание:** Добавляет новую запись в таблицу.

**Пример:**

```sql
INSERT INTO users (first_name, last_name, age) 
VALUES 
('John', 'Doe', 28),
('Alice', 'Smith', 24),
('Bob', 'Johnson', 30);
```

```cmd
| id | first_name | last_name | age |
| -- | ---------- | --------- | --- |
| 1  | John       | Doe       | 28  |
| 2  | Alice      | Smith     | 24  |
| 3  | Bob        | Johnson   | 30  |
```

### SELECT

**Описание:** Выбирает данные из таблицы.

**Пример:**

```sql
SELECT first_name, last_name 
FROM users;
```

```cmd
| first_name | last_name |
| ---------- | --------- |
| John       | Doe       |
| Alice      | Smith     |
| Bob        | Johnson   |
```

### UPDATE

**Описание:** Обновляет данные существующих записей.

**Пример:**

```sql
UPDATE users 
SET age = 31 
WHERE first_name = 'Bob';
```

```cmd
| id | first_name | last_name | age |
| -- | ---------- | --------- | --- |
| 1  | John       | Doe       | 28  |
| 2  | Alice      | Smith     | 24  |
| 3  | Bob        | Johnson   | 31  |
```

(обновили возраст Bob с 30 → 31)

### DELETE

**Описание:** Удаляет записи из таблицы.

**Пример:**

```sql
DELETE FROM users 
WHERE first_name = 'Bob';
```

```cmd
| id | first_name | last_name | age |
| -- | ---------- | --------- | --- |
| 1  | John       | Doe       | 28  |
| 2  | Alice      | Smith     | 24  |
```

(Bob удалён)

### ALTER TABLE

**Описание:** Изменяет структуру таблицы (добавляет/удаляет столбцы, меняет типы данных).

**Пример:**

```sql
ALTER TABLE users 
ADD COLUMN email VARCHAR(100);
```

```cmd
| id | first_name | last_name | age | email |
| -- | ---------- | --------- | --- | ----- |
| 1  | John       | Doe       | 28  | NULL  |
| 2  | Alice      | Smith     | 24  | NULL  |
```

(Добавлен столбец email)

### JOIN

**Описание:** Объединяет данные из нескольких таблиц.

**Пример (INNER JOIN):**

```sql
SELECT orders.id, users.first_name, users.last_name 
FROM orders
INNER JOIN users ON orders.user_id = users.id;
```

```cmd
| id | first_name | last_name | order_id |
| -- | ---------- | --------- | -------- |
| 1  | John       | Doe       | 101      |
| 2  | Alice      | Smith     | 102      |
```

(что у John заказ 101, у Alice 102)

### WHERE

**Описание:** Фильтрует данные по условию.

**Пример:**

```sql
SELECT * FROM users 
WHERE age > 25;
```

```cmd
| id | first_name | last_name | age |
| -- | ---------- | --------- | --- |
| 1  | John       | Doe       | 28  |
```

(выборка age > 25)

### ORDER BY

**Описание:** Сортирует результат по одному или нескольким столбцам.

**Пример:**

```sql
SELECT * FROM users 
ORDER BY age DESC;
```

```cmd
| id | first_name | last_name | age |
| -- | ---------- | --------- | --- |
| 1  | John       | Doe       | 28  |
| 2  | Alice      | Smith     | 24  |
```

(сортировка по age DESC — John старше Alice)

### GROUP BY

**Описание:** Группирует записи по указанным столбцам (часто с агрегатными функциями).

**Пример:**

```sql
SELECT age, COUNT(*) as count 
FROM users 
GROUP BY age;
```

```cmd
| age | count |
| --- | ----- |
| 24  | 1     |
| 28  | 1     |
```

(группировка по возрасту)

### AGGREGATE FUNCTIONS

**Описание:** Выполняет операции над группой данных.

* `COUNT()` — количество записей
* `SUM()` — сумма
* `AVG()` — среднее значение
* `MIN()`, `MAX()` — минимальное и максимальное значения

**Пример:**

```sql
SELECT AVG(age) as avg_age 
FROM users;
```

```cmd
| avg_age |
| ------- |
| 26      |
```

(среднее значение возраста: (28+24)/2 = 26)

### DISTINCT

**Описание:** Убирает дублирующиеся значения в выборке.

**Пример:**

```sql
SELECT DISTINCT age 
FROM users;
```

```cmd
| age |
| --- |
| 24  |
| 28  |
```

### LIMIT

**Описание:** Ограничивает количество возвращаемых строк.

**Пример:**

```sql
SELECT * 
FROM users 
ORDER BY age DESC 
LIMIT 2;
```

```cmd
| id | first_name | last_name | age |
| -- | ---------- | --------- | --- |
| 1  | John       | Doe       | 28  |
| 2  | Alice      | Smith     | 24  |
```

### BETWEEN

**Описание:** Фильтрует значения в диапазоне.

**Пример:**

```sql
SELECT * 
FROM users 
WHERE age BETWEEN 25 AND 30;
```

```cmd
| id | first_name | last_name | age |
| -- | ---------- | --------- | --- |
| 1  | John       | Doe       | 28  |
```

### LIKE

**Описание:** Фильтрует строки по шаблону.

**Пример:**

```sql
SELECT * 
FROM users 
WHERE first_name LIKE 'J%';
```

```cmd
| id | first_name | last_name | age |
| -- | ---------- | --------- | --- |
| 1  | John       | Doe       | 28  |
```

### UNION

**Описание:** Объединяет результаты двух запросов.

**Пример:**

```sql
SELECT first_name 
FROM users 
WHERE age < 25

UNION

SELECT first_name 
FROM users 
WHERE age > 27;
```

```cmd
| first_name |
| ---------- |
| Alice      |
| John       |
| Bob        |
```

### CASE

**Описание:** Условная логика прямо в запросе.

**Пример:**

```sql
SELECT 
    first_name, 
    CASE 
        WHEN age >= 28 THEN 'Adult'
        ELSE 'Young'
    END AS status
FROM users;
```

```cmd
| first_name | status |
| ---------- | ------ |
| John       | Adult  |
| Alice      | Young  |
| Bob        | Adult  |
```

### TRUNCATE

**Описание:** Полностью очищает таблицу.

**Пример:**

```sql
TRUNCATE TABLE users;
```

```cmd
| id       | first_name | last_name | age      |
| -------- | ---------- | --------- | -------- |
| *пусто*  | *пусто*    | *пусто*   | *пусто*  |
```
