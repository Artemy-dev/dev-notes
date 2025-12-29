# Нормализация таблиц пользователей (SQLite)

**Нормализация** — это процесс разделения одной большой таблицы на несколько логически связанных таблиц, чтобы:

* убрать дублирование данных
* упростить структуру
* повысить читаемость и поддержку схемы
* не таскать лишние колонки в каждом запросе

---

## Исходная проблема

Изначально у нас есть одна большая таблица пользователей:

```text
users
| id | user_id | created_at | status | banned | name | age | description | phone | email | telegram_login | bonus_balance |
```

### Минусы такого подхода

* Таблица быстро разрастается
* Большинство запросов используют 3–5 колонок, но читают все
* Логически разные данные (профиль, контакты, баланс) смешаны
* Сложно менять и расширять схему

---

## Идея нормализации

Разделить данные по **смыслу**, сохранив связь через `user_id`.

В результате приложение **явно знает**, из каких таблиц брать данные (через JOIN).

---

## Итоговая структура

### 1️. Основная таблица пользователя `users_core`

```text
| id | user_id | created_at | status | banned |
```

Хранит:

* факт существования пользователя
* системный статус
* блокировку

---

### 2. Профиль пользователя users_profile

```text
| user_id | name | age | description |
```

Хранит:

* публичную / описательную информацию
* редко используемые поля

---

### 3. Контактные данные users_contacts

```text
| user_id | phone | email | telegram_login |
```

Хранит:

* контактную информацию
* данные, которые часто меняются

---

### 4. Баланс пользователя

```text
users_balance
| user_id | bonus_balance |
```

Хранит:

* финансовые данные
* позволяет изолировать операции с балансом

---

## SQL-схема (SQLite)

### users_core

```sql
CREATE TABLE users_core (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    user_id INTEGER NOT NULL UNIQUE,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    status TEXT CHECK (status IN ('admin', 'user')) NOT NULL,
    banned INTEGER NOT NULL DEFAULT 0
);
```

---

### users_profile

```sql
CREATE TABLE users_profile (
    user_id INTEGER PRIMARY KEY,
    name TEXT,
    age INTEGER,
    description TEXT,
    FOREIGN KEY (user_id) REFERENCES users_core(user_id)
);
```

---

### users_contacts

```sql
CREATE TABLE users_contacts (
    user_id INTEGER PRIMARY KEY,
    phone TEXT,
    email TEXT,
    telegram_login TEXT,
    FOREIGN KEY (user_id) REFERENCES users_core(user_id)
);
```

---

### users_balance

```sql
CREATE TABLE users_balance (
    user_id INTEGER PRIMARY KEY,
    bonus_balance INTEGER NOT NULL DEFAULT 0,
    FOREIGN KEY (user_id) REFERENCES users_core(user_id)
);
```

---

## Как теперь выглядят запросы

### Получить базовую информацию

```sql
SELECT status, banned
FROM users_core
WHERE user_id = ?;
```

---

### Получить профиль пользователя

```sql
SELECT p.name, p.age, p.description
FROM users_profile p
WHERE p.user_id = ?;
```

---

### Получить все данные пользователя

```sql
SELECT
    c.status,
    c.banned,
    p.name,
    p.age,
    b.bonus_balance
FROM users_core c
LEFT JOIN users_profile p ON p.user_id = c.user_id
LEFT JOIN users_balance b ON b.user_id = c.user_id
WHERE c.user_id = ?;
```

---

## Это НЕ партиционирование

| Признак                      | Партиционирование | Нормализация |
| ---------------------------- | ----------------- | ------------ |
| Делим строки                 | ✅                 | ❌            |
| Делим колонки                | ❌                 | ✅            |
| Таблица логически одна       | ✅                 | ❌            |
| JOIN в запросах              | ❌                 | ✅            |
| Приложение знает о структуре | ❌                 | ✅            |

---

## Когда нормализация — правильный выбор

* Малые и средние объёмы данных
* SQLite / embedded БД
* Telegram-боты
* Частые изменения структуры

---

## Коротко

> **Нормализация — это про порядок и смысл данных.**
> **Партиционирование — про масштаб и производительность.**

В твоём случае нормализация — **абсолютно правильное архитектурное решение**.
