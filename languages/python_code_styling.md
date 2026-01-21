## Black

**Black** - автоформаттер кода для Python. Он автоматически приводит код к единому стилю оформления, не задавая пользователю почти никаких настроек, чтобы разработчик мог сосредоточиться на логике, а не на пробелах и переносах строк. Основная идея Black - "один правильный стиль для всех". 

### Какие задачи решает
- Приводит код к единому форматированию во всём проекте.
- Убирает споры о стиле в команде (где ставить скобки, переносы строк и т.д.).
- Повышает читаемость кода.
- Упрощает код-ревью (меньше шума из-за форматирования).

### Когда использовать
- В любом проекте с несколькими разработчиками.
- Перед коммитом в репозиторий.
- Перед отправкой кода на ревью.
- В CI, чтобы гарантировать единый стиль.

### Установка
```bash
pip install black
```

### Базовая настройка
Конфигурация хранится в файле `pyproject.toml` в корне проекта.

Минимальный пример:
[tool.black]
line-length = 88
target-version = ["py311"]

Основные команды
Форматирует файл: black main.py
Форматирует весь проект: black .
Показывает, что будет изменено, но не меняет файл: black main.py --diff

Флаги
Показать изменения без применения: --diff
Вернуть ошибку, если файл не отформатирован: --check
Длина строки: --line-length N
Исключить файлы и папки: --exclude REGEX

Пример (До/После)
До:
def func(a,b): return a+b

После:
def func(a, b):
    return a + b


flake8

flake8 - линтер для Python. Он анализирует код и находит ошибки, потенциальные баги, нарушения стиля и плохие практики в коде, но не изменяет код автоматически.

Какие задачи решает
- Находит синтаксические ошибки.
- Выявляет неиспользуемые переменные и импорты.
- Проверяет соответствие PEP8.
- Находит потенциально опасные конструкции.
- Повышает общее качество кода.

	Когда использовать
- Во время разработки, чтобы ловить ошибки сразу.
- Перед коммитом.
- В CI для блокировки плохого кода.
- При обучении Python (очень хорошо показывает проблемы).

Установка
pip install flake8


Базовая настройка
Конфигурация хранится в файле .flake8

Минимальный пример:
[flake8]
max-line-length = 88
exclude = venv,migrations
ignore = E203,W503

Основные команды
Проверка одного файла: flake8 main.py
Проверка всего проекта: flake8 .

Флаги
Количество найденных ошибок: --count
Статистика по типам ошибок: --statistics
Показывает строку кода с ошибкой: --show-source
Длина строки: --max-line-length N

Пример
Код:
import os

def func():
    pass
    x = 10

Вывод flake8:
F401 'os' imported but unused
F841 local variable 'x' is assigned to but never used


isort

isort - автоформаттер импортов. Он автоматически сортирует импорты по группам и по алфавиту.

Какие задачи решает
- Приводит импорты к единому виду.
- Разделяет стандартные, сторонние и внутренние импорты.
- Убирает дубли.
- Повышает читаемость начала файлов.

Когда использовать
- В проектах с большим количеством импортов.
- В командах, где у всех разный стиль.
- Перед коммитом.
- Вместе с Black.

Установка
pip install isort

Базовая настройка
Конфигурация хранится в файле pyproject.toml в корне проекта.

Минимальный пример:
[tool.isort]
profile = "black"
line_length = 88

profile = "black" - используется для совместимости с Black.

Основные команды
Сортирует импорты в файле: isort main.py
Сортирует импорты во всём проекте: isort .
Показывает изменения без применения: isort main.py --diff

Полезные флаги
Показать изменения: --diff
Проверить без изменений: --check-only
Стиль совместимый с Black: --profile black
Исключить папку: --skip venv

Пример (До/После)
До:
import myapp.models
import os
import requests

После isort:
import os

import requests

import myapp.models


autoflake

autoflake - это утилита для автоматического удаления неиспользуемых импортов и переменных из Python-кода. По умолчанию не форматирует код.

Какие задачи решает
- Удаляет неиспользуемые импорты.
- Убирает неиспользуемые переменные.
- Чистит код от "мусора" после рефакторинга.
- Уменьшает количество предупреждений линтеров.

Когда использовать
- После рефакторинга.
- Когда flake8 постоянно ругается на unused.
- Перед коммитом.
- При очистке старого кода.

Установка
pip install autoflake

Базовая настройка
Конфигурация хранится в файле pyproject.toml в корне проекта.

Минимальный пример:
[tool.autoflake]
check_diff = true
remove_all_unused_imports = true

Основные команды
Проверка файла: autoflake main.py
Изменяет файл: autoflake main.py --in-place
Чистит весь проект: autoflake . --recursive --in-place

Полезные флаги
Применять изменения: --in-place
Проход по папкам: --recursive
Удалить все неиспользуемые импорты: --remove-all-unused-imports
Удалить переменные: --remove-unused-variables
Только проверка: --check

Пример (До/После)
До:
import os
import sys

def func():
    x = 10
    return 5

После:
def func():
    return 5


pyright

pyright - статический анализатор типов для Python (игнорирует динамические типы без аннотаций). Он проверяет типы без запуска программы и находит потенциальные ошибки, связанные с типизацией и логикой.

Какие задачи решает
- Находит ошибки типов.
- Проверяет корректность аннотаций.
- Обнаруживает обращения к несуществующим атрибутам.
- Ловит возможные None-ошибки.
- Повышает надёжность кода.

Когда использовать
- В проектах с type hints.
- В больших кодовых базах.
- Перед релизом.
- Вместо или вместе с mypy.

Установка
pip install pyright

Базовая настройка
Конфигурация хранится в файле pyproject.toml в корне проекта.

Минимальный пример:
[tool.pyright]
typeCheckingMode = "basic"
reportMissingImports = true

Основные команды
Проверка файла: pyright main.py
Проверка всего проекта: pyright .

Полезные флаги
Статистика по типам: --stats
Проверка пакета: --verifytypes package
Уровень строгости: --level basic/strict

Пример
Код:
def add(a: int, b: int) -> int:
    return a + "1"

Вывод:
Operator "+" not supported for types "int" and "str"


Пример (До/После) для всех 5 инструментов.
До:
import os
import sys
import math
import random
import requests
import json
import datetime


DISCOUNT=0.1
NAME = "Super Mega Ultra Discount Assistant Bot Version 1.0 Created By Unknown Developer For Educational Purposes Only"


def calc(price,percent):
    return price-(price*percent)


def helper():
    user_input=input("Enter price: ")
    p=float(user_input)
    result=calc(p,DISCOUNT)
    x=10
    print("Your price with discount is: "+str(result))


def main():
    helper()
    if random.randint(1,10)>5: print("Lucky day!")


main()

Проблемы в этом коде
- 7 импортов, используются только 1.
- Плохое форматирование.
- Длинная строка.
- Неиспользуемая переменная x.
- Отсутствие типизации.
- Смешанный стиль.

После:
import random


DISCOUNT = 0.1
NAME = (
    "Super Mega Ultra Discount Assistant Bot Version 1.0 "
    "Created By Unknown Developer For Educational Purposes Only"
)


def calc(price: float, percent: float) -> float:
    return price - (price * percent)


def helper() -> None:
    user_input = input("Enter price: ")
    price = float(user_input)
    result = calc(price, DISCOUNT)
    print(f"Your price with discount is: {result}")


def main() -> None:
    helper()
    if random.randint(1, 10) > 5:
        print("Lucky day!")


if __name__ == "__main__":
    main()
