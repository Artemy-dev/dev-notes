# Alembic (миграции для SQLAlchemy)

---

## Установка Alembic
```bash
pip install alembic
```

#### Проверка

```bash
alembic --version
```

---

## Инициализация

```bash
alembic init alembic
```

Создаст папку `alembic/` и файл `alembic.ini`

## Минимальная структура проекта

```tex
project/
│
├── database/
│   ├── manager.py      # engine + session
│   └── models.py       # SQLAlchemy модели
│
├── alembic/            
├── alembic.ini         # конфиг alembic
```

---

## database/manager.py (подключение к БД)

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker

DATABASE_URL = "postgresql+psycopg2://admin:1234@localhost:5432/data"
# admin - логин
# 1234 - пароль
# 5432 - порт
# data - имя БД

engine = create_engine(DATABASE_URL)
SessionLocal = sessionmaker(bind=engine)
```

---

## database/models.py (пример моделей)

```python
from sqlalchemy import Column, Integer, String
from sqlalchemy.orm import declarative_base

Base = declarative_base()

class User(Base):
    __tablename__ = "users"

    id = Column(Integer, primary_key=True)
    name = Column(String(50))
    age = Column(Integer)
```

---

## Настройка Alembic

#### В `alembic.ini` найти строку:
```tex
sqlalchemy.url = driver://user:pass@localhost/dbname
```

#### Заменить на:
```tex
sqlalchemy.url = postgresql+psycopg2://admin:1234@localhost:5432/data
```

#### В `alembic/env.py` импортировать Base
```python
from database.models import Base
```

#### Найти строку:
```python
target_metadata = None
```

#### Заменить на:
```python
target_metadata = Base.metadata
```

---

## Создание первой миграции

```bash
alembic revision --autogenerate -m "create users table"
```

Создаст файл `alembic/versions/xxxx_create_users_table.py`

### Применение миграции

```bash
alembic upgrade head
```

---

## Обновление таблицы (изменение схемы)

#### Пример: добавить поле `email` в `users`

#### Меняем модель `models.py`

```python
class User(Base):
    __tablename__ = "users"

    id = Column(Integer, primary_key=True)
    name = Column(String(50))
    age = Column(Integer)
    email = Column(String(100))   # новое поле
```

#### Генерируем миграцию
```bash
alembic revision --autogenerate -m "add email to users"
```

#### Применяем
```bash
alembic upgrade head
```

В БД появится новый столбец `email`

---

## Откат миграции (rollback)

#### Откат последней миграции
```bash
alembic downgrade -1
```

Что произойдёт:
- отменится последняя миграция
- столбец email будет удалён
- версия в alembic_version откатится назад

#### Откат к конкретной версии
Посмотреть историю
```bash
alembic history
```

Пример
```bash
716d9b906caf -> 7cdb0bff9eb6 (head), add email to users
<base> -> 716d9b906caf, create users table
```

Откатиться
```bash
alembic downgrade 716d9b906caf
```

Вернуться обратно к последней миграции 
```bash
alembic upgrade 7cdb0bff9eb6
```

---

## Создание новой таблицы

#### Добавляем модель

```python
class Post(Base):
    __tablename__ = "posts"

    id = Column(Integer, primary_key=True)
    title = Column(String(100))
    content = Column(String)
```

#### Генерируем миграцию
```bash
alembic revision --autogenerate -m "create posts table"
```

#### Применяем
```bash
alembic upgrade head
```

---

## Типовой workflow

1. Меняешь models.py
2. Генерируешь миграцию: `alembic revision --autogenerate -m "что изменил"`

3. Применяешь: `alembic upgrade head`
