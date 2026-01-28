# Docker + PostgreSQL

**Docker** - инструмент для запуска приложений в изолированных контейнерах. Позволяет запускать программы без установки на систему и конфликтов с локальными зависимостями.

**Docker Compose** - утилита для управления несколькими контейнерами сразу через один файл (docker-compose.yml).

**PostgreSQL** - реляционная база данных.

### Почему в Docker
- Не нужно устанавливать Postgres на ПК.
- Контейнер изолирован, не конфликтует с локальными версиями.
- Легко менять версии Postgres, создавать чистые среды.

### Разница с локальным pgAdmin/Postgres
- В локальной установке БД работает только на твоей машине.
- В Docker можно запускать несколько версий Postgres и легко сбрасывать базы.
- Настройка окружения через docker-compose.yml полностью контролируется через код.

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
  db:                   # Имя сервиса. Можно любое, это идентификатор контейнера в Docker
    image: postgres     # Образ, который Docker будет использовать. Здесь официальный PostgreSQL
    restart: always     # Если контейнер падает или Docker перезагружается, контейнер стартует снова
    shm_size: 128mb     # Размер общей памяти (shared memory) для Postgres. Нужно для некоторых операций в БД
    environment:
      POSTGRES_PASSWORD: 1234   # пароль для пользователя PostgreSQL (пользователь сам придумывает)
      POSTGRES_USER: admin   # имя пользователя PostgreSQL (пользователь сам придумывает)
      POSTGRES_DB: data         # имя создаваемой базы данных при первом запуске (пользователь сам задаёт)
    ports:
      - "5432:5432"     # локальный порт 5432 → порт 5432 контейнера, если локального Postgres нет
      - "5433:5432"     # локальный порт 5433 → порт 5432 контейнера, если локальный Postgres есть, чтобы не конфликтовать
```

Объяснение про порты:

- `5432:5432` стандартный порт Postgres в контейнере и на локальном ПК.
- `5433:5432` локальный порт 5433 на ПК → порт 5432 в контейнере. Используется, если на ПК уже есть десктопная PostgreSQL, чтобы не было конфликта.

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

Пример вывода:

```text
CONTAINER ID   IMAGE      COMMAND                  CREATED       STATUS          PORTS                                         NAMES
0718f3a2cfd5   postgres   "docker-entrypoint.s…"   5 hours ago   Up 40 minutes   0.0.0.0:5433->5432/tcp, [::]:5433->5432/tcp   training-time-db-1
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
