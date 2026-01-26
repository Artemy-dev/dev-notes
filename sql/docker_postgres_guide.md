# Docker + PostgreSQL

---

## Установка Docker

Скачиваем и устанавливаем [Docker](https://www.docker.com/get-started/)

### Проверка установки

```bash
docker --version
```

```bash
docker-compose --version
```

---

## Создание проекта и docker-compose.yml

Создаём папку проекта и внутри docker-compose.yml:

```yaml
services:
  db:
    image: postgres
    restart: always
    shm_size: 128mb
    environment:
      POSTGRES_PASSWORD: 1234
      POSTGRES_USER: postgres
      POSTGRES_DB: data
    ports:
      - "5432:5432"  # если локальный PostgreSQL НЕ установлен
      - "5433:5432"  # если локальный PostgreSQL уже есть на ПК
```

Объяснение про порты:

- `5432:5432` стандартный порт Postgres в контейнере и на локальном ПК.
- `5433:5432` локальный порт 5433 на ПК → порт 5432 в контейнере. Используется, если на ПК уже есть PostgreSQL, чтобы не было конфликта.

---

## Запуск контейнера
```bash
docker-compose up -d
```

`-d` - запуск в фоне

### Проверка работы контейнера

```bash
docker ps
```

---

## Подключение к БД из IDE

Параметры подключения

| Параметр | Значение      |
| -------- | ------------- |
| Host     | localhost     |
| Port     | 5432 или 5433 |
| Database | data          |
| User     | postgres      |
| Password | 1234          |

После подключения можно писать SQL-запросы, создавать таблицы и наполнять их данными.

---

## Создание и заполнение таблиц (пример)

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50),
    age INT
);

INSERT INTO users (name, age) VALUES ('Artemy', 25);
INSERT INTO users (name, age) VALUES ('Maria', 30);

SELECT * FROM users;
```

---

## Остановка и удаление контейнера

Остановить контейнер:

```bash
docker-compose down
```

Остановить + удалить данные:

```bash
docker-compose down -v
```
