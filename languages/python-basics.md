# Python Basics - Основы языка в 100 строках

```python
# Переменные разных типов
num = 42         # целое число
flt = 3.14       # дробное число
txt = "Hello"    # строка
flag = True      # булево значение
nothing = None   # пустое значение (отсутствие данных)

# Комментарии (#) - однострочный комментарий
"""
Многострочный комментарий.
Может занимать несколько строк
"""

# Конвертация типов
x = "42"
y = int(x)     # строку в число
z = float(x)   # строку в число с плавающей точкой
b = bool(x)    # строка непустая -> True

# Булевы выражения и логические операторы
is_active = True
has_items = False
print(is_active and has_items)   # False - оба должны быть True
print(is_active or has_items)    # True - хотя бы одно True
print(not is_active)             # False - отрицание

# Типы данных
lst = [1, 2, 3]         # список
tpl = (1, 2, 3)         # кортеж
dct = {"a": 1}          # словарь
st = {1, 2, 3}          # множество
frz = frozenset([1,2])  # неизменяемое множество

# Срезы списков (list slicing)
lst = [0, 1, 2, 3, 4]
print(lst[1:4])         # [1, 2, 3] - с 1 до 3 индекса
print(lst[:3])          # [0, 1, 2] - с начала до 2 индекса
print(lst[::2])         # [0, 2, 4] - каждый второй элемент

# Работа со строками
text = " hello world "
print(text.upper())             # " HELLO WORLD "
print(text.strip())             # "hello world" — убирает пробелы по краям
print(text.split())             # ['hello', 'world'] — разбивает по пробелам
print("-".join(["a","b","c"]))  # "a-b-c" — объединение элементов списка

# Форматирование строк
name = "Alice"
age = 25
print(f"My name is {name} and I am {age} years old.")                  # f-strings (Python 3.6+)
print("My name is {} and I am {} years old.".format(name, age))        # Метод .format()
print("My name is {n} and I am {a} years old.".format(n=name, a=age))  # Метод .format()
print("My name is %s and I am %d years old." % (name, age))            # %-форматирование (старый стиль)

# Методы списков
lst = [1, 2, 3]
lst.append(4)        # добавляем элемент в конец
lst.insert(1, 10)    # вставляем 10 на индекс 1
lst.pop()            # удаляет последний элемент
lst.pop(1)           # удаляет элемент с индексом 1

# Методы словарей и множеств
d = {"a":1, "b":2}
print(d.keys())      # dict_keys(['a', 'b'])
print(d.values())    # dict_values([1, 2])
print(d.items())     # dict_items([('a', 1), ('b', 2)])
print(d.get("a"))    # безопасный доступ к ключу
print(d.get("c", 0)) # если ключа нет, возвращает 0
d.update({"c": 3})   # обновляем или добавляем ключ

# Методы множеств
s1 = {1,2,3}
s2 = {2,3,4}
print(s1.union(s2))         # {1,2,3,4}
print(s1.intersection(s2))  # {2,3}
print(s1.difference(s2))    # {1}
s.add(4)                    # добавляем элемент
s.remove(2)                 # удаляем элемент, KeyError если нет
s.discard(5)                # удаляем элемент, ошибки нет если нет

# Условные операторы (if, elif, else)
if num == 0:            # проверяем равенство нулю
    print("Ноль")
elif num % 2 == 0:      # проверяем делимость на 2
    print("Четное")
else:                   # если ни одно условие не выполнено
    print("Нечетное")

# Циклы for и while
for n in lst:       # проходим по всем элементам списка
    print(n)
    
while num > 40:     # пока num больше 40
    print("Hello")
    num -= 1        # уменьшаем num на 1

# Цикл for с range()
for i in range(5):  # 0, 1, 2, 3, 4
    print(i)

for i in range(2, 10, 2):  # 2, 4, 6, 8
    print(i)

# Цикл for по словарю и строке
for key, value in d.items():
    print(key, value)

for char in "Python":
    print(char)

# break / continue
for i in range(5):
    if i == 2:
        continue     # пропускаем этот шаг
    if i == 4:
        break        # выходим из цикла

# enumerate, zip
lst1 = ["a", "b", "c"]
lst2 = [1, 2, 3]

for idx, val in enumerate(lst1):
    print(idx, val)  # 0 a, 1 b, 2 c

for x, y in zip(lst1, lst2):
    print(x, y)      # a 1, b 2, c 3

# any, all
print(any([False, True, False]))  # True
print(all([True, True, False]))   # False

# Тернарный оператор
x = 10
y = "Even" if x % 2 == 0 else "Odd"
print(y)  # Even

# Функции и лямбды
def add(x: int, y: int) -> int:  # функция сложения с аннотацией типов
    return x + y                 # возвращаем сумму

sqr = lambda x: x ** 2           # лямбда-функция для возведения в квадрат

print(add(3, 2), sqr(5))   # выводим результаты работы функций

# Функции с параметрами по умолчанию и ключевыми аргументами
def greet(name="User", loud=False):
    msg = f"Hello, {name}"
    if loud:
        msg = msg.upper()
    print(msg)

greet()                # Hello, User
greet("Alice")         # Hello, Alice
greet("Bob", loud=True)  # HELLO, BOB

# Генераторы списков и словарей
squares = [i * i for i in range(5)]     # список квадратов чисел 0-4
doubles = {i: i * 2 for i in range(5)}  # словарь удвоенных чисел
print(squares, doubles)

# Декоратор
def log_start(func):                        # декоратор для логирования
    def wrapper(*args, **kwargs):           # обертка функции
        print("Начало выполнения функции")  # сообщение перед вызовом
        result = func(*args, **kwargs)      # вызов оригинальной функции
        print("Функция выполнена")          # сообщение после выполнения
        return result
    return wrapper

@log_start          # применяем декоратор к функции
def say_hi():
    print("Hello")

say_hi()            # вызываем функцию

# Импорт
import math as m       # импорт модуля с псевдонимом
from math import sqrt  # импорт конкретной функции

circle_radius = 5
circle_area = m.pi * circle_radius ** 2  # вычисляем площадь круга
print(f"Площадь круга с радиусом {circle_radius}: {circle_area:.2f}")
print(f"Квадратный корень из {num}: {sqrt(num)}")

# Модули стандартной библиотеки (кратко)
import os
import random
from datetime import datetime

print("Текущий каталог:", os.getcwd())
print("Случайное число 0-9:", random.randint(0, 9))
print("Текущее время:", datetime.now())

# Работа с файлами (запись/чтение)
with open("file.txt", "w", encoding="utf-8") as f:  # открываем файл для записи (перезапись)
    f.write("Text")                                 # записываем строку

with open("file.txt", "a", encoding="utf-8") as f:  # открываем файл для дозаписи
    f.write("\nNew Text")                            # добавляем строку в конец файла

with open("file.txt", "r", encoding="utf-8") as f:  # открываем файл для чтения
    print(f.read())                                 # читаем и выводим содержимое

# Пример использования with для нескольких файлов
with open("file1.txt", "w") as f1, open("file2.txt", "w") as f2:
    f1.write("File 1")
    f2.write("File 2")

# Исключения
try:
    num / 2                        # потенциально опасная операция
except ZeroDivisionError:          # обработка деления на ноль
    print("Деление на ноль")
else:                              # если ошибок нет
    print("Ошибок нет")
finally:                           # выполняется всегда
    print("Завершение блока try")

# ООП
class Balance:                             # создаем класс Баланс
    def __init__(self, amount=0):          # конструктор с дефолтным балансом
        self.amount = amount               # инициализация баланса

    def show(self):                        # метод отображения баланса
        print(f"Баланс: {self.amount}")

    def add(self, value):                  # метод добавления суммы
        self.amount += value               # увеличиваем баланс
        print(f"Добавлено: {value}")

    def withdraw(self, value):             # метод снятия суммы
        if value > self.amount:            # проверка, хватает ли средств
            print("Недостаточно средств")
        else:
            self.amount -= value           # уменьшаем баланс
            print(f"Снято: {value}")

wallet = Balance(100)                      # создаём кошелёк с балансом 100
wallet.show()                              # показываем текущий баланс
wallet.add(50)                             # добавляем 50
wallet.withdraw(30)                        # снимаем 30
wallet.withdraw(150)                       # пытаемся снять больше, чем есть
```
