### Обзор языка JavaScript

* Высокоуровневый со сборщиком мусора (GC).
* JIT (Just-In-Time) компилируемый. Код сначала читают построчно (работает как интерпретируемая), наиболее часто используемые участки кода компилируются в машинный код во время выполнения.
* Однопоточный. Имеет один главный поток и один стек. Операции выполняются последовательно, но благодаря Event Loop (цикл событий) может обрабатывать асинхронные задачи без блокировки основного потока.
* Динамически типизированный. Тип данных определяется автоматически во время выполнения.
* Мультипарадигмальный. Поддерживает несколько подходов к написанию кода: ООП (работа с объектами и классами), Функциональный (функции как значения, замыкания, чистые функции), Процедурный (последовательное выполнение инструкций).

```javascript
// Процедурный стиль - работа напрямую с переменной и последовательные операции
let n = 5;        // создаём переменную со значением 5
n += 10;          // увеличиваем значение на 10 (n = n + 10)
console.log(n);   // выводим результат: 15

// Функциональный стиль - используем чистую функцию без изменения состояния
const add = (n, x) => n + x; // функция принимает два числа и возвращает их сумму
console.log(add(5, 10));     // передаём значения в функцию и выводим результат: 15

// ООП стиль - данные и поведение объединены в объект
class Num {
  constructor(n) {      // конструктор вызывается при создании объекта
    this.n = n;         // сохраняем значение внутри объекта
  }

  add(x) {              // метод изменяет внутреннее состояние объекта
    this.n += x;        // увеличиваем значение
    return this;        // возвращаем объект для цепочки вызовов
  }

  log() {               // метод для вывода значения
    console.log(this.n);
  }
}

new Num(5)              // создаём объект со значением 5
  .add(10)              // добавляем 10
  .log();               // выводим результат: 15
```

### Установка необходимого софта

* **VS Code** - редактор кода [скачать с официального сайта](https://code.visualstudio.com/).
* **Node.js** - среда выполнения JavaScript на компьютере [скачать с официального сайта](https://nodejs.org/en/download).

Проверка установки **Node.js**. Открыть термина и выполнить:

```bash
node -v   # Покажет версию Node.js (например, v24.13.1)
npm -v    # Покажет версию менеджера пакетов npm (например, 11.8.0)
```

На **Windows** может возникнуть ошибка политики выполнения PowerShell. Запусти PowerShell от имени администратора и выполни:

```bash
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### Создание проекта и запуск первого скрипта

Создать новый файл с расширением `.js` (например, `script.js`). Написать код:

```javascript
console.log('Hello, World!');
```

Открыть терминал в VS Code (`Terminal` → `New Terminal`). Запустить файл командой:

```bash
node script.js
```

Выведет: 

```text
Hello, World!
```

### Комментарии

```javascript
// Однострочный комментарий

/*
Многострочный
комментарий
*/
```

### Переменные

Ключевые слова для объявления переменных:

* **var** - не рекомендуется (устаревший способ объявления переменных).
* **let** - используется, когда значение будет изменяться.
* **const** - рекомендуется по умолчанию, если переназначение не требуется.

```javascript
var a = 1;
var a = 2;      // переназначение допустимо
console.log(a); // 2

let b = 5;
b = 10;         // переназначение допустимо
console.log(b); // 10

const c = 3.14;
// c = 2;       // ошибка: нельзя изменить const
console.log(c); // 3.14

// Рекомендуемый стиль
const name = 'Tim'; // не изменяется - используем const
let age = 20;       // может измениться - используем let
age = 21;           // допустимо
```

### Конкатенация

```javascript
// Конкатенация строк через оператор +
const a = 'Hello';
const b = 'World';

console.log(a + ' ' + b); // Hello World

// Добавление строки к существующей переменной
let str = 'Hello';
str += ' JavaScript';

console.log(str); // Hello JavaScript
```

### Арифметические операторы ( `+`, `-`, `*`, `/`, `%`, `**` )

```javascript
const a = 5;
const b = 3;
console.log(a + b);   // Сложение: 8
console.log(a - b);   // Вычитание: 2
console.log(a * b);   // Вычитание: 15
console.log(a / b);   // Деление: 1.6666666666666667
console.log(a % b);   // Остаток от деления: 2
console.log(a ** b);  // Возведение в степень: 125
```

### Операторы присваивания ( `=`, `+=`, `-=`, `*=`, `/=` )

```javascript
let num = 10;           // Присваивание переменной num знаения 10
console.log(num += 5);  // Сложение с присваиванием:  15
console.log(num -= 3);  // Вычитание с присваиванием: 12
console.log(num *= 2);  // Умножение с присваиванием: 24
console.log(num /= 3);  // Деление с присваиванием:   8
```

### Операторы сравнения ( `==`, `===`, `!=`, `!==`, `>`, `<`, `>=`, `<=` )

* `==` - Нестрогое равенство (Абстрактное равенство, cравнение с приведением типов). Проверяет равенство значений, допуская преобразование типов.
* `===` - Строгое равенство (Идентичность). Проверяет равенство значений и типов данных без преобразования. **Рекомендуется.**
* `!=` - Нестрогое неравенство.
* `!==` - Строгое неравенство.
* `>` - Больше.
* `<` - Меньше.
* `>=` - Больше или равно.
* `<=` - Меньше или равно.

```javascript
console.log(5 == '5');     // true
console.log(5 === '5');    // false
console.log(5 != '5');     // false
console.log(5 !== '5');    // true
console.log(10 > 5);       // true
console.log(5 < 10);       // true
console.log(5 >= 5);       // true
console.log(5 <= 4);       // false
```

### Логические операторы ( &&, ||, !, ?? )

* `&&` - **Логическое И (AND)**. Возвращает `true`, если оба операнда истинны. Если первый операнд ложный, возвращает его значение; иначе возвращает второй операнд.
* `||` - **Логическое ИЛИ (OR)**. Возвращает `true`, если хотя бы один операнд истинен. Если первый операнд истинный, возвращает его значение; иначе возвращает второй операнд.
* `!` - **Логическое НЕ (NOT)**. Возвращает `true`, если операнд ложный, и false, если операнд истинный (инверсия).
* `??` - **Оператор нулевого слияния (Nullish coalescing)**. Возвращает правый операнд, если левый равен `null` или `undefined`, иначе возвращает левый операнд.

```javascript
// Логические операторы с булевыми значениями
console.log(true && false); // false (И)
console.log(true || false); // true  (ИЛИ)
console.log(!true);         // false (НЕ)

// Короткое замыкание (&& возвращает первое ложное или последнее)
console.log(0 && 'hello');  // 0
console.log(1 && 'hello');  // hello
console.log('a' && 'b');    // b

// Короткое замыкание (|| возвращает первое истинное или последнее)
console.log(0 || 'hello');  // hello
console.log(1 || 'hello');  // 1
console.log('a' || 'b');    // a

// Оператор НЕ с преобразованием типов
console.log(!'');           // true (пустая строка → false → true)
console.log(!0);            // true (0 → false → true)
console.log(!!'text');      // true (приведение к булевому типу)

// Значения, которые интерпретируются как false (ложные):
// false, 0, '' (пустая строка), null, undefined, NaN
console.log(Boolean(''));   // false
console.log(Boolean('text')); // true

// Оператор нулевого слияния (??) - только для null/undefined
let value;
console.log(value ?? 'default');  // default (value = undefined)
value = '';
console.log(value ?? 'default');  // '' (пустая строка НЕ заменяется)
value = 0;
console.log(value ?? 'default');  // 0 (0 НЕ заменяется)
value = null;
console.log(value ?? 'default');  // default
```

### Тернарный оператор ( условие ? a : b; )

```javascript
let balance = 100;
let price1 = 120;
let price2 = 80;

// Вариант 1. Тернарный оператор для присваивания значения
let message = balance > price1 ? 'Покупка совершена' : 'Недостаточно средств';
console.log(message);  // Недостаточно средств

// Вариант 2. Вложенный тернарный оператор (цепочка условий)
console.log(
  balance > price1 ? 'Куплен товар 1' : 
  balance > price2 ? 'Куплен товар 2' : 
  'Недостаточно средств'
);  // Куплен товар 2
```

### Типы данных

* Примитивы - простые значения, не являющиеся объектами. Все примитивы неизменяемы.
* Объекты - коллекции данных и структур, могут содержать множества значений.

```javascript
// Примитивы
let age = 25;             // Number (целое число)
let price = 99.99;        // число с плавающей точкой
let infinity = Infinity;  // бесконечность
let notNumber = NaN;      // Not a Number (не число)

let name = 'Tim';       // String (строка), одинарные кавычки
let text = "abc";       // двойные кавычки
let message = `Привет, ${name}`; // обратные кавычки (шаблонные строки)

let isAdmin = true;     // Boolean (булевый/логический тип), истина
let isLogged = false;   // ложь

let info;               // Undefined (неопределенный), переменная объявлена, но не инициализирована
let about = undefined;  // явное присвоение undefined
let data = null;        // Null (пусто)

const bigNumber = 999999999999999n;  // BigInt (большие целые числа)
const id1 = Symbol('id');            // Symbol (символ), создание уникального символа

// Объекты
let user = {  // Object (объект) - коллекция ключ-значение
  name: 'Tim',
  age: 25,
  isAdmin: true
};

let colors = ['red', 'green', 'blue'];  // Array (массив) - упорядоченная коллекция

function greet() {  // Function (функция) - вызываемый объект
  return 'Hello!';
}
```

### Определение типа данных (typeof)

```javascript
console.log(typeof 10);     // number
console.log(typeof 'abc');  // string
console.log(typeof true);   // boolean
```

### Преобразование типов

* **Явное** (ручное) - когда мы сами вызываем функции преобразования.
* **Неявное** (автоматическое) - когда JavaScript сам преобразует типы в операциях.

```javascript
// Явное преобразование
console.log(String(123));    // "123"
console.log(Number('123'));  // 123
console.log(Number(''));     // 0
console.log(Number(true));   // 1

// Унарный плюс (быстрый способ)
console.log(+'123');  // 123
console.log(+true);   // 1
console.log(+false);  // 0

// Неявное преобразование
console.log(5 + '5');    // "55" (число 5 становится строкой)
console.log('5' * '2');  // 10 (умножение преобразует в числа)
console.log('10' - 5);   // 5 (вычитание преобразует в числа)
```

### Шаблонные строки

**Backtick (`)** - обратная кавычка. Аналог f-строки в Python.

```javascript
const username = 'admin';
const password = '12345';
console.log(`Логин: ${username}, пароль: ${password}`);  // Логин: admin, пароль: 12345
```

### Методы строк

```javascript
const ide = 'Visual Studio';

console.log(ide[0] + ide[7] + 'Code');                // VSCode
console.log(ide.charAt(0) + ide.charAt(7) + 'Code');  // VSCode
console.log(ide.length);            // 13 - количнство символов в строке
console.log(ide.indexOf('i'));      // 1 - индекс буквы i (первое вхождение)
console.log(ide.lastIndexOf('i'));  // 11 - индекс буквы i (последнее вхождение)
console.log(ide.includes('S'));     // true (проверка, включает ли строка Visual Studio подстроку S)
console.log(ide.slice(7));          // Studio (обрезает строку до указанного индекса)
console.log(ide.slice(7, 11));      // Stud
console.log(ide.toLowerCase());         // visual studio
console.log(ide.toUpperCase());         // VISUAL STUDIO
console.log(ide.replace('i', '*'));     // V*sual Studio (заменяет только первое вхождение)
console.log(ide.replace(/i/g, '*'));    // V*sual Stud*o (/.../g - для поиска всех вхождений)
console.log(ide.replaceAll('i', '*'));  // V*sual Stud*o
console.log(ide.padStart(20, '='));  // =======Visual Studio
console.log(ide.padEnd(20, '='));    // Visual Studio=======
```

### Условия (if / else if / else)

```javascript
const num = 15;

if (num === 0) {
    console.log(`Число ноль`);
} else if (num % 2 === 0) {
    console.log(`Число ${num} четное`);
} else {
    console.log(`Число ${num} нечетное`);
}  // Выведет: Число 15 нечетное
```

### Конструкция switch-case

* **switch** - выполняет разные блоки кода в зависимости от значения выражения.
* **case** - проверяет совпадение значения.
* **break** - прерывает выполнение switch (без него выполнение "провалится" дальше).
* **default** - выполняется, если ни один case не совпал (аналог else).

```javascript
const role = 'admin';

switch (role) {
    case 'admin':
        console.log('Полный доступ');
        break;
    case 'user':
        console.log('Только просмотр');
        break;
    default:
        console.log('Нет доступа');
}
// Выведет: Полный доступ
```

### Цикл for

```javascript
// Базовый for
for (let i = 0; i < 5; i++) {
    console.log(i); // 0, 1, 2, 3, 4
}

// break - прерывание цикла
for (let i = 0; i < 10; i++) {
    if (i === 5) break;
    console.log(i); // 0, 1, 2, 3, 4
}

// continue - пропуск итерации
for (let i = 0; i < 5; i++) {
    if (i === 2) continue;
    console.log(i); // 0, 1, 3, 4
}
```

### Цикл while

```javascript
// Базовый while
let i = 0;
while (i < 5) {
    console.log(i); // 0, 1, 2, 3, 4
    i++;
}

// break
let j = 0;
while (j < 10) {
    if (j === 5) break;
    console.log(j); // 0, 1, 2, 3, 4
    j++;
}

// continue
let k = 0;
while (k < 5) {
    k++;
    if (k === 3) continue;
    console.log(k); // 1, 2, 4, 5
}
```

### Цикл do...while (выполнится хотя бы один раз)

```javascript
let i = 10;
do {
    console.log(i); // 10
    i++;
} while (i < 5);
```

### Функции

```javascript
// Function Declaration - объявляются через function, доступны до объявления (всплытие).
function sum(a, b) {
    return a + b;
}
console.log(sum(5, 3)); // 8

// Function Expression (анонимная функция) - функция без имени как значение переменной, создаётся когда доходит поток кода.
const multiply = function(a, b) {
    return a * b;
};
console.log(multiply(5, 3)); // 15

// Стрелочные функции - краткий синтаксис, не имеют своего this и arguments.
const divide = (a, b) => a / b;
console.log(divide(10, 2)); // 5

// Стрелочная с блоком кода (нужен return)
const getMax = (a, b) => {
    if (a > b) return a;
    return b;
};
console.log(getMax(10, 20)); // 20
```

### Параметры и аргументы

* **Параметры** - переменные, указанные при объявлении функции.
* **Аргументы** - значения, переданные при вызове функции.

```javascript
// a и b - параметры
function sum(a, b) {
    return a + b;
}

// 5 и 3 - аргументы
console.log(sum(5, 3)); // 8

// Параметры по умолчанию (ES6)
function greet(name = 'Гость') {
    return `Привет, ${name}!`;
}
console.log(greet());        // Привет, Гость!
console.log(greet('Тим'));   // Привет, Тим!

// arguments (псевдомассив, только в обычных функциях)
function showAll() {
    console.log(arguments[0]);     // яблоко
    console.log(arguments[1]);     // банан
    console.log(arguments.length); // 3
}
showAll('яблоко', 'банан', 'апельсин');
```

### Вложенные функции

```javascript
// Вложенная функция (функция внутри другой функции)
function outer(a, b) {
    function inner() {
        return a + b; // имеет доступ к a и b
    }
    return inner();
}
console.log(outer(5, 3)); // 8

// Замыкание (closure) - внутренняя функция имеет доступ к переменным внешней функции
function createCounter() {
    let count = 0;
    return function() {
        count++;
        return count;
    };
}
const counter = createCounter();
console.log(counter()); // 1
console.log(counter()); // 2

// Функция возвращает функцию
function multiplyBy(n) {
    return function(x) {
        return x * n;
    };
}
const double = multiplyBy(2);
console.log(double(5)); // 10
console.log(double(10)); // 20
```

### Функции высшего порядка

Функция, которая принимает другую функцию как аргумент (колбэк) или возвращает функцию.

```javascript
// Принимает функцию (колбэк)
function greet(name, callback) {
    const message = `Привет, ${name}!`;
    callback(message);
}

// Возвращает функцию
function createMultiplier(n) {
    return function(x) {
        return x * n;
    };
}
```

### Массивы

```javascript
const numbers = [1, 2, 3, 4, 5];
const mixed = [1, 'текст', true, null, { name: 'Tim' }];
const empty = [];

// Доступ к элементам (индексация с 0)
console.log(numbers[0]); // 1
console.log(numbers[2]); // 3
numbers[1] = 10;
console.log(numbers); // [1, 10, 3, 4, 5]

// Длина массива
console.log(numbers.length); // 5

// Поиск элементов
console.log(fruits.indexOf('банан')); // 1
console.log(fruits.includes('яблоко')); // true

// Перебор массива
const nums = [1, 2, 3];
for (let i = 0; i < nums.length; i++) {
    console.log(nums[i]); // 1, 2, 3
}

// for...of
for (let num of nums) {
    console.log(num); // 1, 2, 3
}

// for...in (перебирает индексы)
const nums = [10, 20, 30];
for (let index in nums) {
    console.log(index);       // 0, 1, 2 (индексы)
    console.log(nums[index]); // 10, 20, 30 (значения)
}

// forEach
nums.forEach(function(num) {
    console.log(num); // 1, 2, 3
});
```

### Методы массивов

```javascript
// Методы для добавления/удаления
const fruits = ['яблоко', 'банан'];
fruits.push('апельсин');    // добавить в конец
console.log(fruits);        // ['яблоко', 'банан', 'апельсин']
fruits.pop();               // удалить с конца
console.log(fruits);        // ['яблоко', 'банан']
fruits.unshift('груша');    // добавить в начало
console.log(fruits);        // ['груша', 'яблоко', 'банан']
fruits.shift();             // удалить с начала
console.log(fruits);        // ['яблоко', 'банан']

// slice (начало, конец) - не изменяет исходный
const arr = [1, 2, 3, 4, 5];
console.log(arr.slice(1, 4));    // [2, 3, 4]
console.log(arr.slice(2));       // [3, 4, 5]
console.log(arr.slice(-2));      // [4, 5] (отрицательные индексы)

// splice (с какого индекса, сколько удалить, добавить) - изменяет исходный
const arr2 = [1, 2, 3, 4, 5];
console.log(arr2.splice(1, 2));   // [2, 3] (удаленные элементы)
console.log(arr2);                // [1, 4, 5] - исходный изменился

const arr3 = [1, 2, 3, 4, 5];
arr3.splice(2, 0, 'a', 'b');      // вставить без удаления
console.log(arr3);                // [1, 2, 'a', 'b', 3, 4, 5]
arr3.splice(3, 1, 'x');           // заменить
console.log(arr3);                // [1, 2, 'a', 'x', 3, 4, 5]

// concat - объединение массивов (новый массив)
const a = [1, 2];
const b = [3, 4];
const c = a.concat(b);
console.log(c);                    // [1, 2, 3, 4]
// Можно добавлять значения
console.log(a.concat(5, 6));       // [1, 2, 5, 6]

// reverse - переворот массива (изменяет исходный)
const d = [1, 2, 3];
console.log(d.reverse());          // [3, 2, 1]
console.log(d);                    // [3, 2, 1] - исходный изменился

// some - проверяет, удовлетворяет ли хотя бы один элемент условию (возвращает true/false)
// every - проверяет, удовлетворяют ли все элементы условию (возвращает true/false)
const e = [1, 2, 3];
// хотя бы один четный?
console.log(e.some(i => i % 2 === 0));   // true
// все четные?
console.log(e.every(i => i % 2 === 0));  // false

// reduce - сворачивает массив в одно значение (сумма, произведение, объект и т.д.).
const j = [1, 2, 3, 4, 5];
const sum = nums.reduce((acc, num) => acc + num, 0);
//acc - accumulator (накопитель). Переменная, которая накапливает результат на каждой итерации.
console.log(sum); // 15
```

### Сортировка массива

```javascript
const c = ['b', 'c', 'a'];
const n = [-2, 0, -1, 2, 1];

console.log(c.sort());  // [ 'a', 'b', 'c' ]
console.log(n.sort());  // [ -1, -2, 0, 1, 2 ]

// Сортировка по возрастанию
console.log(n.sort((a, b) => a - b));  // [ -2, -1, 0, 1, 2 ]

// Сортировка по убыванию
console.log(n.sort((a, b) => b - a));  // [ 2, 1, 0, -1, -2 ]
```

### Rest-оператор (...)

```javascript
// Rest в функции (собирает аргументы)
function sum(...numbers) {
    return numbers.reduce((total, num) => total + num, 0);
}
console.log(sum(1, 2, 3, 4, 5)); // 15

// Rest с обычными параметрами
function show(first, second, ...rest) {
    console.log(first);  // 1
    console.log(second); // 2
    console.log(rest);   // [3, 4, 5]
}
show(1, 2, 3, 4, 5);

// Rest в деструктуризации массивов
const nums = [1, 2, 3, 4, 5];
const [a, b, ...rest] = nums;
console.log(a);    // 1
console.log(b);    // 2
console.log(rest); // [3, 4, 5]

// Rest в деструктуризации объектов
const user = { name: 'Tim', age: 25, city: 'Moscow' };
const { name, ...other } = user;
console.log(name);  // Tim
console.log(other); // { age: 25, city: 'Moscow' }
```

### Методы split и join

* **split** - преобразует строку в массив по разделителю.
* **join** - преобразует массив в строку с разделителем.

```javascript
const text = 'яблоко,банан,апельсин';
const fruits = text.split(',');
console.log(fruits); // ['яблоко', 'банан', 'апельсин']
console.log('hello'.split(''));  // ['h', 'e', 'l', 'l', 'o']

const colors = ['red', 'green', 'blue'];
console.log(colors.join('-'));  // red-green-blue
console.log(colors.join());     // red,green,blue (по умолчанию запятая)
```

### map

`map` - создает новый массив из результатов вызова функции для каждого элемента (для преобразования данных).

```javascript
const nums = [1, 2, 3];

const numsPow = nums.map((v) => v**2);
console.log(numsPow);  // [ 1, 4, 9 ]

function pow(n) {
    return n**2
}

const nPow = nums.map(v => pow(v));
console.log(nPow);  // [ 1, 4, 9 ]
```

### Объекты 

```javascript
const userInfo = {
    login: 'admin',
    password: '1234',
};

// Доступ к свойствам
console.log(userInfo);              // { login: 'admin', password: '1234' }
console.log(userInfo.login);        // admin (через точку - рекомендуется)
console.log(userInfo['login']);     // admin (через квадратные скобки)

// Добавление и изменение
userInfo.isAdmin = true;            // Добавили новое свойство
userInfo.password = 'a1b2';         // Изменили существующее
console.log(userInfo);              // { login: 'admin', password: 'a1b2', isAdmin: true }

// Удаление свойства
delete userInfo.isAdmin;
console.log(userInfo);              // { login: 'admin', password: 'a1b2' }

// Доступ через переменную
const key = 'login';
console.log(userInfo[key]);         // admin (когда ключ в переменной)
```



















---

### Методы объектов

```javascript
const user = {
    login: 'user',
    domain: '@example.com',
    createEmail: function () {
        console.log(this);  // {login: 'user', domain: '@example.com', createEmail: [Function: createEmail]}
        return this.login + this.domain  // this ссылается на текущий объект (user)
    },
};

console.log(user.createEmail());  // user@example.com
```

---

### Итерирование по объекту

```javascript
const obj = {
    objNum1: {num1: 10, num2: 20},
    objNum2: {num1: 100, num2: 200}
};

let objList = Object.keys(obj);  // Object.keys() выведет список ключей объекта
console.log(objList);            // [ 'objNum1', 'objNum2' ]
console.log(objList.length);     // 2 - количество ключей в объекте

// Вариант 1. Через in
// let sum = 0;
// for (k in obj) {
//     sum += obj[k].num1;
//     sum += obj[k].num2;
// }
// console.log(sum);   // 330 (сумма всех чисел в объекте)

// Вариант 2. Через Object.keys()
let sum = 0;
for (k of Object.keys(obj)) {
    sum += obj[k].num1;
    sum += obj[k].num2;
}
console.log(sum);   // 330 (сумма всех чисел в объекте)
```

---

### Деструктуризация, rest и spread

```javascript
// Деструктуризация массива
const nums = [5, 10, 15];
const [a, b, c] = nums;
console.log(b);  // 10

// Деструктуризация объекта
const user = {
    login: 'Admin',
    role: 'administrator',
    password: '1234',
};
const {login, password} = user;
console.log(login);     // Admin
console.log(password);  // 1234

// rest (сбор остатка) оператор
let userInfo = {
    name: 'Tim',
    age: 25,
    city: 'Moscow',
    email: 'tim@example.com'
};
const {email, ...userAbout} = userInfo;  // ... - rest оператор
console.log(email);      // tim@example.com
console.log(userAbout);  // { name: 'Tim', age: 25, city: 'Moscow' }

//spread (разворот) оператор
const skilsData = {
    skils: ['Python', 'JS'],
    exp: 2
};
console.log(userInfo);
userInfo = {
    ...user,
    ...skilsData
};
console.log(userInfo);
/*
{
  login: 'Admin',
  role: 'administrator',
  password: '1234',
  skils: [ 'Python', 'JS' ],
  exp: 2
}
*/
```

---

### Optional chaining

```javascript
const users = {                         // Корневой объект users - Уровень вложенности: 0
    tim_777: {                          // Свойство tim_777 - Уровень вложенности: 1
        auth: {                         // Свойство auth - Уровень вложенности: 2
            email: 'tim@example.com',   // Свойства email и password - Уровень вложенности: 3
            password: '1234'
        }
    },
    usr_583: {

    }
};
// console.log(users.tim_777.auth.email);  // tim@example.com
// console.log(users.usr_583.auth);        // undefined
// console.log(users.usr_583.auth.email);  // Ошибка TypeError

// (?.) Опциональное построение цепочки / Optional chaining
console.log(users?.tim_777?.auth?.email);  // tim@example.com
console.log(users?.usr_583?.auth);         // undefined (usr_583 - есть, auth - отсутствует)
console.log(users?.usr_583?.auth?.email);  // undefined (usr_583 - есть, auth и email - отсутствуют)
console.log(users?.gst_125?.auth?.email);  // undefined (gst_125, auth и email - отсутствуют)
```

---

## Стек и Куча

* **Call Stack (Стек вызовов)** - это структура данных, которая работает по принципу LIFO (Last In, First Out - последним пришел, первым ушел). Он хранит в оперативной памяти контексты выполнения функций (и глобальный контекст). Стек управляется автоматически (при вызове функции память выделяется, при возврате - очищается). Это очень быстро.
* **Куча (Heap)** - это хранилище в оперативной памяти для объектов. Здесь хранятся сложные, динамические структуры данных. Размер кучи ограничен только объемом доступной оперативной памяти. Память выделяется под объекты, а когда они становятся не нужны, то Garbage Collector (сборщик мусора) находит и очищает их. Это нужно, потому что в куче память может фрагментироваться, и за ней нужно следить, чтобы не закончилось место.

---

### Call Stack (стек)

```javascript
let a = 5;
let b = a;
b = 3;
console.log(a);  // 5
console.log(b);  // 3
```

**Шаг 1:** `let a = 5;`

```text
┌───────────┬──────────┬─────────┐
│ Переменная│ Адрес    │ Значение│
├───────────┼──────────┼─────────┤
│ a         │ 0xFF1    │ 5       │
└───────────┴──────────┴─────────┘
```

**Шаг 2:** `let b = a;`

```text
┌───────────┬──────────┬──────────┐
│ Переменная│ Адрес    │ Значение │
├───────────┼──────────┼──────────┤
│ a         │ 0xFF1    │ 5        │
│ b         │ 0xFF2    │ 5 (копия)│ ← копирование значения
└───────────┴──────────┴──────────┘
```

**Шаг 3:** `b = 3;`

```text
┌───────────┬──────────┬─────────┐
│ Переменная│ Адрес    │ Значение│
├───────────┼──────────┼─────────┤
│ a         │ 0xFF1    │ 5       │ ← не изменилось
│ b         │ 0xFF2    │ 3       │ ← изменилось только b
└───────────┴──────────┴─────────┘
```

---

### Heap (куча)

```javascript
const a = {num: 5};
const b = a;
b.num = 3;
console.log(a.num);  // 3
console.log(b.num);  // 3
```

**Шаг 1:** `const a = {num: 5};`

```text
Стек                                 Куча
┌───────────┬──────────┬─────────┐   ┌──────────┬──────────┐
│ Переменная│ Адрес    │ Значение│   │ Адрес    │ Значение │
├───────────┼──────────┼─────────┤   ├──────────┼──────────┤
│ a         │ 0xFF1    │ 0x001   │ ─>│ 0x001    │ {num: 5} │
└───────────┴──────────┴─────────┘   └──────────┴──────────┘
```

**Шаг 2:** `const b = a;` (копирование ссылки)

```text
Стек                                 Куча
┌───────────┬──────────┬─────────┐   ┌─────────┬──────────┐
│ Переменная│ Адрес    │ Значение│   │ Адрес   │ Значение │
├───────────┼──────────┼─────────┤   ├─────────┼──────────┤
│ a         │ 0xFF1    │ 0x001   │ ─┐│ 0x001   │ {num: 5} │
│ b         │ 0xFF2    │ 0x001   │ ─┴────┘     │          │
└───────────┴──────────┴─────────┘   └─────────┴──────────┘
```

**Шаг 3:** `b.num = 3;` (изменение объекта по ссылке)

```text
Стек                                 Куча
┌───────────┬──────────┬─────────┐   ┌─────────┬──────────┐
│ Переменная│ Адрес    │ Значение│   │ Адрес   │ Значение │
├───────────┼──────────┼─────────┤   ├─────────┼──────────┤
│ a         │ 0xFF1    │ 0x001   │ ─┐│ 0x001   │ {num: 3} │ ← изменилось!
│ b         │ 0xFF2    │ 0x001   │ ─┴────┘     │ 5 → 3    │
└───────────┴──────────┴─────────┘   └─────────┴──────────┘
```

Обе переменные указывают на ОДИН объект в куче. Поэтому изменение видно через обе:

```javascript
console.log(a);  // 5
console.log(b);  // 3
```

---

### Heap (куча) + Object.assign() / spread-оператор

**Object.assign()**

```javascript
const a = {num: 5};
const b = Object.assign({}, a);
b.num = 3;
console.log(a.num);  // 5
console.log(b.num);  // 3
```

**Шаг 1:** `const a = {num: 5};`

```text
Стек                                 Куча
┌───────────┬──────────┬─────────┐   ┌──────────┬──────────┐
│ Переменная│ Адрес    │ Значение│   │ Адрес    │ Значение │
├───────────┼──────────┼─────────┤   ├──────────┼──────────┤
│ a         │ 0xFF1    │ 0x001   │ ─>│ 0x001    │ {num: 5} │
└───────────┴──────────┴─────────┘   └──────────┴──────────┘
```

**Шаг 2:** `const b = Object.assign({}, a);` (создание копии объекта)

```text
Стек                                 Куча
┌───────────┬──────────┬─────────┐   ┌─────────┬──────────┐
│ Переменная│ Адрес    │ Значение│   │ Адрес   │ Значение │
├───────────┼──────────┼─────────┤   ├─────────┼──────────┤
│ a         │ 0xFF1    │ 0x001   │   │ 0x001   │ {num: 5} │
│ b         │ 0xFF2    │ 0x002   │   │ 0x002   │ {num: 5} │ (копия)
└───────────┴──────────┴─────────┘   └─────────┴──────────┘
```

**Шаг 3:** `b.num = 3;` (изменение копии объекта)

```text
Стек                                 Куча
┌───────────┬──────────┬─────────┐   ┌─────────┬──────────┐
│ Переменная│ Адрес    │ Значение│   │ Адрес   │ Значение │
├───────────┼──────────┼─────────┤   ├─────────┼──────────┤
│ a         │ 0xFF1    │ 0x001   │   │ 0x001   │ {num: 5} │ ← не изменилось!
│ b         │ 0xFF2    │ 0x002   │   │ 0x002   │ {num: 3} │ ← изменилось!
└───────────┴──────────┴─────────┘   └─────────┴──────────┘
```

**spread-оператор**

```javascript
const a = {num: 5};
const b = {...a};
b.num = 3;
console.log(a.num);  // 5
console.log(b.num);  // 3
```

---

## Область видимости (Scope chain)

В JavaScript используется лексическая область видимости (lexical scoping) (иногда называемая статической). Это означает, что область видимости переменной определяется тем, где в коде она была объявлена, а не тем, откуда вызывается функция. Переменная, объявленная внутри функции, помещается в локальную область видимости (scope) этой функции. Эта переменная доступна только внутри тела этой функции и во вложенных в нее функциях. Снаружи функции она недоступна.

```javascript
const a = 5;       // Глобальный scope

function func() {
    const a = 10;    // Scope функции
}

if (true) {
    const a = 15;    // Блочный scope
}
```

---

### Strict mode

**Strict mode** (`'use strict'`) включает более строгий синтаксис и безопасный код.


```javascript
'use strict';      // Включение Strict mode
// Запрещает объявлять переменные без ключевого слова.
num = 5;           // Выводит ошибку ReferenceError: num is not defined
```


```javascript
'use strict';
// Функции в блоках видны только внутри этого блока (не всплывают).
if (true) {
    function test() {
        console.log('test');
    }
    test();  // 'test'
}
test();  // ReferenceError: test is not defined
```


```javascript
'use strict';
// Запрет на зарезервированные переменные
const interface = 5;  // SyntaxError: Unexpected strict mode reserved word
```

```javascript
'use strict';
// Запрет дублирующих пааметров
function func(a, a) {  // SyntaxError: Duplicate parameter name not allowed in this context
    console.log(a);
}
```

---

### Поднятие

Возможность использовать переменные до их объявления.

```javascript
'use strict';

console.log(func(5));  // 25
console.log(a);        // undefined
console.log(b);        // ReferenceError: Cannot access 'b' before initialization
console.log(c);        // ReferenceError: Cannot access 'c' before initialization

function func(num) {
    return num**2
}

var a = 1;
let b = 2;
const c = 3;
```

---

### this

```javascript
const user = {
    login: 'guest',
    password: '1234',
    email: 'guest@mail.com',
    getInfo: function () {
        console.log(`${this.login} - ${this.email}`);  // guest - guest@mail.com
        const getPass = () => {
            console.log(this.password);                // 1234
        }
        getPass();
    },
    usrInfo: () => {
        console.log(`${this.login} - ${this.email}`);  // undefined - undefined
    }
}
```

---

### Arguments

```javascript
function sum(a, b) {
    console.log(arguments);                        // [Arguments] { '0': 3, '1': 5, '2': 7 }
    console.log(arguments[0]);                     // 3
    console.log(arguments['0']);                   // 3
    console.log(arguments['0'] + arguments['2']);  // 10
    console.log(a + b);                            // 8
}

sum(3, 5, 7);
```

---

## Управление this

---

### Сокращенный синтаксис методов (Enhanced Object Literals)

```javascript
'use strict';

const num = 5;
const dict = {
    num,  // num вместо num: num
    getNum: function () {
        return this.num;
    },
    getNumAlt() {  // getNumAlt() вместо getNumAlt: function()
        return this.num;
    }
}

console.log(dict.getNum());     // 5
console.log(dict.getNumAlt());  // 5
```

---

### Call, apply

**call()** и **apply()** - позволяют вызвать функцию так, как будто она является методом указанного объекта.

```javascript
'use strict';

const phone = {
    model: 'iPhone 13',
    defects: [],
    addDefects(part, extent) {
        this.defects.push({
            part,
            extent
        });
        console.log(this.defects);
    }
};

phone.addDefects('диплей', 'трещина');  // [ { part: 'диплей', extent: 'трещина' } ]

const laptop = {
    model: 'MacBook',
    defects: [],
};

// Вариант 1: Присваивание метода (копирование ссылки)
// laptop.addDefects = phone.addDefects;  // копируем ссылку на метод
// laptop.addDefects('клавиатура', 'залипает');  // [ { part: 'клавиатура', extent: 'залипает' } ]

const addDefectsFunc = phone.addDefects;

// Вариант 2: call() - передаем аргументы через запятую
// addDefectsFunc.call(laptop, 'клавиатура', 'залипает');  // [ { part: 'клавиатура', extent: 'залипает' } ]

// Вариант 3: apply() - передаем аргументы массивом
addDefectsFunc.apply(laptop, ['АКБ', 'Не держит заряд']);  // [ { part: 'АКБ', extent: 'Не держит заряд' } ]
```

---

### Bind

bind() - создает новую функцию, которая навсегда привязывает указанный объект как this, и позволяет вызывать эту функцию позже (сразу или с дополнительными аргументами).

```javascript
'use strict';

const phone = {
    model: 'iPhone 13',
    defects: [],
};

const productsManipulation = {
    addDefects(part, extent) {
        this.defects.push({ part, extent });
        console.log(`Дефект для ${this.model} добавлен.`);
    }
};

// Вариант 1: Частичное применение - сразу привязали phone и первый аргумент 'дисплей'
// const addDefectsPhoneDisplay = productsManipulation.addDefects.bind(phone, 'дисплей');
// addDefectsPhoneDisplay('царапины');  // Дефект для iPhone 13 добавлен.
// console.log(phone.defects);   // [ { part: 'дисплей', extent: 'царапины' } ]

// Вариант 2: Привязали только объект, аргументы передаем при вызове
const addDefectsPhone = productsManipulation.addDefects.bind(phone);
addDefectsPhone('дисплей', 'царапины');  // Дефект для iPhone 13 добавлен.
console.log(phone.defects);  // [ { part: 'дисплей', extent: 'царапины' } ]
```

```javascript
'use strict';

const user = { login: 'admin', password: '1234' };
console.log(`Логин: "${user.login}" Пароль: "${user.password}"`);  // Логин: "admin" Пароль: "1234"

function rmPass(res) {
    if (res) { this.password = undefined };
};

const userRmPass = rmPass.bind(user);  // bind(user) создает новую функцию, где this навсегда привязан к объекту user
userRmPass(true);  // функция rmPass выполняется с this = user
console.log(`Логин: "${user.login}" Пароль: "${user.password}"`);  // Логин: "admin" Пароль: "undefined"
```

---

### IIFE

```javascript
function  init() { console.log('Инициализация'); }
init();  // Инициализация
init();  // Инициализация (логичекая ошибка, допускаем инициализацию 2 раза подряд)

(function() { console.log('Инициализация (IIFE)'); })();  // Такая функция будет вызвана только 1 раз
```

---

### Замыкания

```javascript
'use strict';

function balanceChange() {
    let balance = 0;
    return function(n) {
        balance += n;
        console.log(`На счету: ${balance}`);
    }
}

const balance = balanceChange();  // создали счет №1 (balance = 0)
const newBalance = balanceChange();  // создали счет №2 (balance = 0)

balance(1000);  // счет №1: 0 + 1000 = 1000
balance(-600);  // счет №1: 1000 - 600 = 400  
newBalance(2000);  // счет №2: 0 + 2000 = 2000
newBalance(-300);  // счет №2: 2000 - 300 = 1700

// Каждая функция хранит свою копию переменной balance в своем замыкании.
```

Замыкание - это способность функции запоминать и иметь доступ к переменным из места своего создания, даже после того как внешняя функция завершила работу.
