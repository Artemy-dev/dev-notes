## Старт

---

### Необходимый софт

**VS Code** - редактор кода [скачать с официального сайта](https://code.visualstudio.com/).
<br>**Node.js** - среда выполнения JavaScript на компьютере [скачать с официального сайта](https://nodejs.org/en/download).

---

### Проверка установки Node.js
Открыть терминал (командную строку) и выполнить:

```bash
node -v   # Покажет версию Node.js (например, v24.13.1)
npm -v    # Покажет версию менеджера пакетов npm (например, 11.8.0)
```
На **Windows** может возникнуть ошибка политики выполнения PowerShell. Запусти PowerShell от имени администратора и выполни:

```bash
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

---

### Создание и запуск первого файла

- В VS Code создать папку проекта (`File` → `Open Folder`).
- Создать новый файл с расширением `.js` (например, `script.js`).
- Написать код:

```javascript
console.log('Hello, World!');
```

Открыть терминал в VS Code (`Terminal` → `New Terminal`). Запустить файл командой:

```bash
node script.js
```

Выведет: Hello, World!

---

## Основы

---

### Комментарии

```javascript
// Однострочный комментарий

/*
Многострочный
комментарий
*/
```

---

### Переменные и значения

```javascript
let num = 5;       // let - ключевое слово при объявлении переменной
num = 10;
console.log(num);  // 10

const pi = 3.14;   // const - ключевое слово для константы
// pi = 1.2; - попытка перезаписать выведет ошибку TypeError: Assignment to constant variable.
console.log(pi);
```

---

### Операторы
*(Функция в JS)*
- **Операторы присваивания** ( `=`, `+=`, `-=`, `*=`, `/=` )
- **Операторы сравнения** ( `==`, `===`, `!=`, `!==`, `>`, `<`, `>=`, `<=` )
- **Арифметические операторы** ( `+`, `-`, `*`, `/`, `%`, `**` )
- **Битовые операторы** ( `&`, `|`, `^`, `~`, `<<`, `>>`, `>>>` )
- **Логические операторы** ( `&&`, `||`, `!` )
- **Строковые операторы** ( `+` (конкатенация), `+=` )
- **Тернарный оператор** ( `ondition ? a : b` )
- **Оператор запятая** ( `,` )
- **Унарные операторы** ( `+`, `-`, `++`, `--`, `typeof`, `delete` )
- **Операторы отношения** ( `in`, `instanceof` )

**Арифметические операторы**

```javascript
const a = 5;
const b = 3;
console.log(a + b);   // Сложение: 8
console.log(a - b);   // Вычитание: 2
console.log(a / b);   // Деление: 1.6666666666666667
console.log(a % b);   // Остаток от деления: 2
console.log(a ** b);  // Возведение в степень: 125
```

**Строковые операторы**

```javascript
let a = 'Hello';
let b = 'World!';
console.log(a + ' ' + b);     // Hello World!
a += ' JavaScript!';
console.log(a);               // Hello JavaScript!
console.log('Number: ' + 1);  // Number: 1
```

**Операторы присваивания**

```javascript
let age = 18;           // Присваивание переменной age знаения 18
console.log(age += 2);  // Сложение с присваиванием: 20
console.log(age -= 2);  // Вычитание с присваиванием: 18
console.log(age *= 2);  // Умножение с присваиванием: 36
console.log(age /= 2);  // Деление с присваиванием: 18
```

**Операторы сравнения**

`==` - Нестрогое равенство (Абстрактное равенство, cравнение с приведением типов). Проверяет равенство значений, допуская преобразование типов.
<br>`===` - Строгое равенство (Идентичность). Проверяет равенство значений и типов данных без преобразования. **Рекомендуется.**
<br>`!=` - Нестрогое неравенство.
<br>`!==` - Строгое неравенство.
<br>`>` - Больше.
<br>`<` - Меньше.
<br>`>=` - Больше или равно.
<br>`<=` - Меньше или равно.

```javascript
console.log(5 == '5');   // true
console.log(5 === '5');  // false
console.log(5 != '5');   // false
console.log(5 !== '5');  // true
console.log(5 > 3);      // true
console.log(5 < 3);      // false
console.log(3 < '5');    // true
console.log(5 <= '5');   // true
console.log(5 >= '5');   // true
```

---

### Типы данных
- Объекты.
- Примитивы.

Примитивыные типы:
```javascript
let age = 25;           // Число (number).
let pi = 3.14;          // Число (number).
let name = 'Tim';       // Строка (string).
let text1 = "abc";      // Строка (string).
let text2 = `abc`;      // Строка (string).
let isAdmin = true;     // Булевый (логический) тип (boolean).
let info;               // Не заданное значение (undefined). Переменная объявлена, но значение не было задано.
let about = undefined;  // Не заданное значение (undefined).
let data = null;        // Пустое знаение (object).
console.log(info);    // undefined
console.log(about);   // undefined
console.log(data);    // null
const bigNum = BigInt(999999999999999);  // Для работы с большим числами (bigint).
console.log(bigNum);  // 999999999999999n
const str = Symbol('text');  // Уникальное неизменное значене (symbol).

console.log(typeof name);    // typeof - оператор для определения типа.
```

*Важно! Переменная не имеет определенный тип. Тип имеет значение, которые мы присваиваем переменной.*

---

### Шаблонные строки
**Backtick (`)** - обратная кавычка. Аналог f-строки в Python.

```javascript
const project = 'Интернет-магаин';
const developer = 'Tim';
const price = 5000;

// Обычная строка
const res = developer + ' выполнил проект: ' + project + ' за ' + price + ' денег.';
console.log(res);  // Tim выполнил проект: Интернет-магаин за 5000 денег.

// Шаблонная строка
const res2 = `${developer} выполнил проект: ${project} за ${price} денег.`;
console.log(res2);  // Tim выполнил проект: Интернет-магаин за 5000 денег.

console.log(`Проект: ${project}
Разработчик: ${developer}
Цена: ${price}`);
/* 
Выведет:
Проект: Интернет-магаин
Разработчик: Tim
Цена: 5000 
*/
```

---

### Преобразование типов

```javascript
console.log('5' + 3);          // 53
console.log(Number('5') + 3);  // 8
console.log('5' - 3);          // 2 (JS автоматически переконвертировал строку в число для вычитания)
console.log(Boolean(0));       // false
console.log(Boolean(''));      // false
console.log(Boolean(1));       // true
console.log(Boolean(15));      // true
console.log(Boolean(-7));      // true
console.log(Boolean("a"));     // true
console.log(true + 5)          // 6 (JS автоматически переконвертировал true в 1 для сложения)
console.log(true / 2)          // 0.5
```

---

## Управление потоком

---

### if / else if / else

```javascript
const num = 15;

if (num == 0) {
    console.log(`Число ноль`);
} else if (num % 2 == 0) {
    console.log(`Число ${num} четное`);
} else {
    console.log(`Число ${num} нечетное`);
}  // Выведет: Число 15 нечетное
```

---

### Switch

```javascript
let role = 'admin';

switch (role) {
    case 'guest':
        console.log('Гость');
        break;
    case 'user':
        console.log('Пользователь');
        break;
    case 'admin':
    case 'administrator':
        console.log('Администратор');
        break;
    default:
        console.log('Ошибка');
}

// Вывод: Администратор
```

```javascript
let num = -7;

switch (true) {
    case num === 0:  // true === (num === 0)
        console.log('Ноль');
        break;
    case num > 0:
        console.log('Положительное число');
        break;
    case num < 0:
        console.log('Отрицательное число');
        break;
}

// Вывод: Отрицательное число
```

---

### Тернарный оператор ( условие ? a : b; )

Вариант 1.
```javascript
let balance = 500;
let price = 300;
balance > price ? console.log('Message: Покупка совершена') : console.log('Message: Недостаточно средств');
// Вывод: Message: Покупка совершена
```

Вариант 2.
```javascript
let balance = 500;
let price = 300;
console.log(`Message: ${balance > price ? 'Покупка совершена' : 'Недостаточно средств'}`);
```

Вариант 3.
```javascript
let balance;
let price1 = 300;
let price2 = 100;

balance = 500;
console.log(balance > price1 ? 'Куплен товар 1.' : balance > price2 ? 'Куплен товар 2.' : 'Недостаточно средств');
// Куплен товар 1.

balance = 250;
console.log(balance > price1 ? 'Куплен товар 1.' : balance > price2 ? 'Куплен товар 2.' : 'Недостаточно средств');
// Куплен товар 2.

balance = 50;
console.log(balance > price1 ? 'Куплен товар 1.' : balance > price2 ? 'Куплен товар 2.' : 'Недостаточно средств');
// Недостаточно средств
```

---

## Булева логика (общий раздел математической логики и дискретной математики)

#### AND (И) &&

Истина только если оба операнда (A и B) истинны.

```text
A B | Результат
0 0 | 0
0 1 | 0
1 0 | 0
1 1 | 1
```

#### OR (ИЛИ) ||

Истина если хотя бы один операнд (A или B) истинен.

```text
A B | Результат
0 0 | 0
0 1 | 1
1 0 | 1
1 1 | 1
```

#### NOT (НЕ) !

Инверсия значения.

```text
A | результат
0 | 1
1 | 0
```

Приоритет операций: NOT → AND → OR

#### Примеры:

- 1 AND 0 = 0
- 1 OR 0 = 1
- NOT 1 = 0

---

### Логичесие операторы

```javascript
const a = false;
const b = true;
console.log(`${a} И ${b}: ${a && b}`);    // false И true: false
console.log(`${a} ИЛИ ${b}: ${a || b}`);  // false ИЛИ true: true
console.log(`Инвертируем ${a}: ${!a}`);   // Инвертируем false: true
console.log(`!${a} (false → true) И ${b}: ${!a && b}`);  // !false (false → true) И true: true
```

---

### Операторы с другими типами

```javascript
let a;
let username = a || 'Гость';
console.log(username);  // Гость

a = 'User';
username = a || 'Гость';
console.log(username);  // User
```

```javascript
let password = '1234';
let login = 'admin';
let getLogin = password === '1234' && login;
console.log(getLogin);  // admin
```

```javascript
let password = 'abcd';
let login = 'admin';
let getLogin = password === '1234' && login;
console.log(getLogin);  // false
```

---

### Оператор нулевого слияния ( ?? )

```javascript
let username;

console.log(username || 'Гость');  // Гость

username = '';
console.log(username || 'Гость');  // Гость
username = 0;
console.log(username || 'Гость');  // Гость
username = 'admin';
console.log(username || 'Гость');  // admin

username = '';
console.log(username ?? 'Гость');  // (пустая строка)
username = 0;
console.log(username ?? 'Гость');  // 0
username = 'admin';
console.log(username ?? 'Гость');  // admin
```

---

## Функции

---

### Введение в функции

```javascript
/* 
Функция конвертирует гигабайты в мегабайты.
function - ключевое слово
fromGbToMb - название функции
gb - аргумет функции
return - возвращаемое значение
fromGbToMb() - вызов функции
*/

function fromGbToMb(gb) {
    const mb = gb * 1024;
    return `${gb} Gb = ${mb} Mb`;
}

let res = fromGbToMb(5);
console.log(res);  // 5 Gb = 5120 Mb
console.log(fromGbToMb(1));  // 1 Gb = 1024 Mb
```

---

### Анонимные функции

```javascript
// Записываем фунцию в переменную
const fromGbToMb = function (gb) {
    const mb = gb * 1024;
    return `${gb} Gb = ${mb} Mb`;
}

console.log(fromGbToMb(5));  // 5 Gb = 5120 Mb
```

---

### Стрелочные функции

```javascript
// переменная = параметр => результат;
const fromGbToMb = gb => `${gb} Gb = ${gb * 1024} Mb`;
console.log(fromGbToMb(5));  // 5 Gb = 5120 Mb
console.log(fromGbToMb(2));  // 2 Gb = 2048 Mb

// переменная = (параметры) => {блок кода}
const add = (a, b) => {
    console.log(`Сума чисел ${a} и ${b}:`);
    return a + b;
}
console.log(add(7, 9));
/*
Вывод:
Сума чисел 7 и 9:
16
*/
```

---

### Параметры по умолчанию

```javascript
function pow(n, p=2) {
    return n ** p;
}

console.log(pow(5));     // 25
console.log(pow(5, 3));  // 125
```

---

### Условия в функциях

Вариант 1.

```javascript
function adminPanel(role) {
    if (role === 'admin') {
        return true;
    }
    return false;
}

console.log(adminPanel('user'));   // false
console.log(adminPanel('admin'));  // true
```

Вариант 2.

```javascript
// Стерлочна функция + Тернарный оператор (не рекомендуется из-за плохой читаемости)
const adminPanel = role => role === 'admin' ? true : false;
console.log(adminPanel('user'));   // false
console.log(adminPanel('admin'));  // true
```

---

### Функции в функциях

```javascript
function addition(a, b) {
    return a + b;
}

function subtraction(a, b) {
    return a - b;
}

function calculate(a, b) {
    add = addition(a, b);
    sub = subtraction(a, b);
    return `Сумма чисел: ${add}. Разница чисел: ${sum}.`;
}

console.log(calculate(5, 3));  // Сумма чисел: 8. Разница чисел: 2.
```

---

## Массивы

```javascript
const arr1 = ['a', 'b', 'c']           // Первый способ объявить массив
const arr2 = new Array('a', 'b', 'c')  // Второй способ объявить массив
console.log(arr1)  // [ 'a', 'b', 'c' ]
console.log(arr1)  // [ 'a', 'b', 'c' ]

const list = [25, 'text', true, ['a', 'b', 'c']];

console.log(list);         // [ 25, 'text', true, [ 'a', 'b', 'c' ] ]
console.log(list.length);  // 4 - длина массива

console.log(list[1]);     // text
console.log(list.at(1));  // text

console.log(list[3]);         // [ 'a', 'b', 'c' ]
console.log(list.at(-1));     // [ 'a', 'b', 'c' ]
console.log(list[3][0]);      // a
console.log(list.at(-1)[0]);  // a
```

---

### Управление элементами массива

```javascript
let list = ['a', 'b', 'c'];

// Индексы
list[1] = 5;
console.log(list);  // [ 'a', 5, 'c' ]
list[3] = 'd';
console.log(list);  // [ 'a', 5, 'c', 'd' ]
list[5] = 'text';
console.log(list);  // [ 'a', 5, 'c', 'd', <1 empty item>, 'text' ]

list = [1, 2, 3];

// Методы
list.push(4);          // .push() - добавляет элемент в конец массива
console.log(list);     // [ 1, 2, 3, 4 ]
list.unshift(0);       // .unshift() - добавляет элемент в начало массива
console.log(list);     // [ 0, 1, 2, 3, 4 ]
let a = list.pop();    // .pop() - удаляет последний элемент массива и сохр. его в переменную
console.log(list);     // [ 0, 1, 2, 3 ]
console.log(a);        // 4
let b = list.shift();  // .shift() - удаляет первый элемент массива и сохр. его в переменную
console.log(list);     // [ 1, 2, 3 ]
console.log(b);        // 0
```

---

### Поиск элемента

```javascript
let list = ['a', 'b', 'c'];

console.log(list.indexOf('c'));   // 2 - индекс элемента 'c'
console.log(list.indexOf('e'));   // -1 - если элемента нет в массиве
console.log(list.includes('a'));  // true
```

---

### Slice, splice, concat, reverse

```javascript
let list = ['a', 'b', 'c', 'd', 'e'];

console.log(list.slice(2));     // [ 'c', 'd', 'e' ] - Возвращяет часть массива с указанного индекса
console.log(list.slice(1, 3));  // [ 'b', 'c' ]
console.log(list.slice(-1));    // [ 'e' ]
console.log(list.slice(-2));    // [ 'd', 'e' ]
console.log(list);              // [ 'a', 'b', 'c', 'd', 'e' ] - Исходный массив не изменился
```

```javascript
let list = ['a', 'b', 'c', 'd', 'e'];
console.log(list.splice(2));  // [ 'c', 'd', 'e' ]
console.log(list);            // [ 'a', 'b' ] - Метод .splice() изменяет исхоный массив

let list = ['a', 'b', 'c', 'd', 'e'];
console.log(list.splice(2, 2));  // [ 'c', 'd' ] - Срез со 2 элемента, 2 - элемента
console.log(list);               // [ 'a', 'b', 'e' ]
```

```javascript
let list1 = ['a', 'b', 'c'];
let list2 = ['d', 'e', 'f'];
let newList = list1.concat(list2)

console.log(list1);    // [ 'a', 'b', 'c' ]
console.log(list2);    // [ 'd', 'e', 'f' ]
console.log(newList);  // [ 'a', 'b', 'c', 'd', 'e', 'f' ]
```

```javascript
let list = ['a', 'b', 'c', 'd', 'e'];
list.reverse();
console.log(list);  // [ 'e', 'd', 'c', 'b', 'a' ] - Изменяет исходный массив
```

---

### Из строки в массив и обратно

```javascript
// Строка → Список
const namesString = 'Tim, Bob, John';
const namesList = namesString.split(', ');
console.log(namesList);  // [ 'Tim', 'Bob', 'John' ]

// Список → Строка
const numsList = [1, 2, 3, 4, 5];
const numsString = numsList.join(', ');
console.log(numsString);  // 1, 2, 3, 4, 5
```

---

### Деструктуризация

```javascript
const userInfo = ['Admin', '1234'];
const [login, passwor] = userInfo;  // [login, passwor] - список переменных
console.log(login);    // Admin
console.log(passwor);  // 1234
```

---

### Rest оператор

```javascript
const nums = [1, 2, 3, 4, 5];
const [a, b, ...rest] = nums;
console.log(rest);  // [ 3, 4, 5 ]
```

---

## Циклы

---

### Цикл for

```javascript
for(let i = 1; i < 4; i++) {
    console.log(i);  // Выведет 1, 2, 3 (каждое число на новой строке)
}
```

---

### Break и continue

```javascript
const nums = ['a', 'b', 'c'];

for(let i = 0; i < nums.length; i++) {
    console.log(nums[i]);  // Выведет a, b, c
}

// continue - пропуск итерации
for(let i = 0; i < nums.length; i++) {
    if (nums[i] === 'b') {
        continue;
    }
    console.log(nums[i]);  // Выведет a, c
}

// break - прервать цикл
for(let i = 0; i < nums.length; i++) {
    if (nums[i] === 'c') {
        break;
    }
    console.log(nums[i]);  // Выведет a, b
}
```

---

### Цикл в цикле

Вариант 1.

```javascript
for (let a = 1; a < 3; a++) {
    for(let b = 1; b < 4; b++) {
        console.log(`a = ${a}; b = ${b}`)
    }
}
/*
a = 1; b = 1
a = 1; b = 2
a = 1; b = 3
a = 2; b = 1
a = 2; b = 2
a = 2; b = 3
*/
```

Вариант 2.

```javascript
const list = [ [1, 'Tim'], [2, 'Bob'], [3, 'John'] ]
for(let i = 0; i < list.length; i++) {
    for(let j = 0; j < list[i].length; j++) {
        console.log(list[i][j])
    }
}
/*
1
Tim
2
Bob
3
John
*/
```

---

### Цикл while

Вариант 1.

```javascript
// for(let i = 1; i < 4; i++) {
//     console.log(i);  // Выведет 1, 2, 3 (каждое число на новой строке)
// }

let i = 1;
while (i < 4) {
    console.log(i);  // Выведет 1, 2, 3 (каждое число на новой строке)
    i++;
}
```

Вариант 2.

```javascript
const nums = ['a', 'b', 'c'];

// for(let i = 0; i < nums.length; i++) {
//     if (nums[i] === 'c') {
//         break;
//     }
//     console.log(nums[i]);  // Выведет a, b
// }

let i = 0
while (nums[i] != 'c') {
    console.log(nums[i]);  // Выведет a, b
    i++;
}
```

---

### Цикл do while

```javascript
let i = 1;
do {
    console.log(i);  // Сначала выполниться блок do (минимум один раз)
    i++
} while(i < 0);      // Только потом будет проверка условия
```

---

### Циклы for of и for in

```javascript
const chars = ['a', 'b', 'c'];

// for(let i = 0; i < nums.length; i++) {
//     console.log(nums[i]);  // Выведет a, b, c
// }

for(let i of chars) {       // of - итерируется по значениям массива
    console.log(i);         // Выведет a, b, c
}

for(let i in chars) {       // in - итерируется по индексам массива
    console.log(chars[i]);  // Выведет a, b, c
}
```
Вывод индекса и значения с помощью `.entries()`

```javascript
const chars = ['a', 'b', 'c'];

for (let [i, v] of chars.entries()) {
    console.log(`Индекс: ${i}, значение: ${v}`);
}

/* 
Индекс: 0, значение: a
Индекс: 1, значение: b
Индекс: 2, значение: c 
*/
```

---

## Функции высшего порядка

**Функция первого класса** - это функция, которую можно хранить в переменной.

```javascript
const func = (num) => num++;
```

**Функции высшего порядка** - это функция, которая принимает другие функции как аргумент и возвращает другие функции.

```javascript
function example(func) {  // Принимает функцию func

}
```

```javascript
function example() {
    return func;  // Возвращяет функцию func
}
```

---

### Callback

```javascript
function addition(a, b) {
    return a + b;
}

function subtraction(a, b) {
    return a - b;
}

// функция высшего порядка
function calculate(a, b, callback_func) {
    console.log(callback_func.name);  // .name - возвращяет имя функции
    const result = callback_func(a, b)
    return result
}

console.log(calculate(5, 3, addition));
console.log(calculate(5, 3, subtraction));

/*
Вывод:
addition
8
subtraction
2
*/
```

---

### Возврат функции

Вариант 1.

```javascript
function pow(p) {
    return function (n) {
        return n**p;
    }
}

const power = pow(2);   // Переменная power - это функция, замкнувшая p = 2 (power хранит значение p = 2, хотя pow уже отработала)
console.log(power(5));  // 25

console.log(pow(2)(5)); // 25
/*
pow(2) → возвращает функцию с зафиксированным p = 2
(5) → передает n = 5 в эту функцию
*/
```

Вариант 2.

```javascript
// function pow(p) {
//     return function (n) {
//         return n**p;
//     }
// }

// console.log(pow(2)(5)); // 25

// Стрелочная функция
const pow = p => n => n**p;
console.log(pow(2)(5)); // 25
```

---

## Итерации в массивах

---

### forEach

`forEach` - выполняет переданную функцию для каждого элемента массива без создания нового массива (для побочных действий).

```javascript
const chars = ['a', 'b', 'c']

// for (let [i, v] of chars.entries()) {
//     console.log(`Индекс: ${i}, значение: ${v}`);
// }

chars.forEach((v, i) => {
    console.log(`Индекс: ${i}, значение: ${v}`);
})

/* 
Индекс: 0, значение: a
Индекс: 1, значение: b
Индекс: 2, значение: c 
*/
```

---

### map

`map` - создает новый массив из результатов вызова функции для каждого элемента (для преобразования данных).

```javascript
const nums = [5, 3, -2, 7, -6, 3];

const numsPow = nums.map((v, i) => v**2);
console.log(nums);     // [ 5, 3, -2, 7, -6, 3 ]
console.log(numsPow);  // [ 25, 9, 4, 49, 36, 9 ]
```

---

### filter

`filter` - оставляет элементы, которые удовлетворяют условию.

```javascript
const nums = [5, 3, -2, 7, -6, 3];

const positiveNums = nums.filter(v => v > 0);
console.log(positiveNums);  // [ 5, 3, 7, 3 ] 
```

---

### filter + map

```javascript
const nums = [5, 3, -2, 7, -6, 3];

// const numsPow = nums.map(v => v**2);
// const positiveNums = nums.filter(v => v > 0);
// console.log(numsPow);       // [ 25, 9, 4, 49, 36, 9 ]
// console.log(positiveNums);  // [ 5, 3, 7, 3 ] 

const numsPositivePow = nums
    .filter(v => v > 0)
    .map(v => v**2);

console.log(numsPositivePow);  // [ 25, 9, 49, 9 ]
```

---

### reduce

```javascript
const nums = [5, 3, -2, 7, -6, 3];

// Считаем сумму всех чисел в списке
// let res = 0;
// for (value of nums) {
//     res += value;
// }
// console.log(res);  // 10

const res = nums.reduce((acc, value, i) => {
    console.log(`Итерация: ${i} - acc: ${acc}, value: ${value}`);
    return acc += value;
}, 0);

/*
Итерация: 0 - acc: 0, value: 5
Итерация: 1 - acc: 5, value: 3
Итерация: 2 - acc: 8, value: -2
Итерация: 3 - acc: 6, value: 7
Итерация: 4 - acc: 13, value: -6
Итерация: 5 - acc: 7, value: 3
*/

console.log(res);  // 10
```

---

### find и findIndex

`find` - ищет первый встечающийся элемент в массиве, удовлетворяющий условию.
`findIndex` - ищет первый встечающийся элемент в массиве, удовлетворяющий условию и возвращяет его индекс

```javascript
const nums = [5, 3, -2, 7, -6, 3, 10];

console.log(nums.find(i => i > 5));         // 7
console.log(nums.findIndex(i => i > 5));    // 3 - Индекс элемента 7
console.log(nums.findIndex(i => i === 7));  // 3
console.log(nums.findIndex(i => i === 8));  // -1 (если такого элемента нет в массиве)
```

---

### some

`some` - проверяет массив на наличие элемента.

```javascript
const nums = [5, 3, -2, 7, -6, 3, 10];
const chars = ['a', 'b', 'c'];

console.log(nums.some(i => i === 3));     // true
console.log(nums.some(i => i === 4));     // false
console.log(chars.some(i => i === 'c'));  // true
console.log(chars.some(i => i === 'e'));  // false
```

---

### flat и flatMap

`flat` - превращает многомерный массив в плоский массив. В качестве аргумента передает число уровней вложенности (по умолчанию 1).

```javascript
const matrix = [[1, [2, 2.5]], [3, 4]];

console.log(matrix);                // [ [ 1, [ 2, 2.5 ] ], [ 3, 4 ] ]
console.log(matrix.flat());         // [ 1, [ 2, 2.5 ], 3, 4 ]
console.log(matrix.flat().flat());  // [ 1, 2, 2.5, 3, 4 ]
console.log(matrix.flat(2));        // [ 1, 2, 2.5, 3, 4 ]
```

`flatMat` - сначала преобразуее данные (map), потом превращает многомерный массив в плоский массив (flat).

```javascript
let matrix = [[1, 2], [3, 4]];

// console.log(matrix);                                      // [ [ 1, 2 ], [ 3, 4 ] ]
// console.log(matrix = matrix.map(i => i.concat(i[1]+1)));  // [ [ 1, 2, 3 ], [ 3, 4, 5 ] ]
// console.log(matrix.flat());                               // [ 1, 2, 3, 3, 4, 5 ]

console.log(matrix.flatMap(i => i.concat(i[1]+1)));  // [ 1, 2, 3, 3, 4, 5 ]
```

---

### sort

```javascript
const names = ['Tim', 'Bob', 'Ann'];
names.sort();
const nums = [4, -3, 6, -8, 1, 2];
nums.sort();

console.log(names);  // [ 'Ann', 'Bob', 'Tim' ]
console.log(nums);   // [ -3, -8, 1, 2, 4, 6 ] - сортиует как строки (по умолчанию)

// Сортировка по возрастанию
nums.sort((a, b) => a - b);
console.log(nums);   // [ -8, -3, 1, 2, 4, 6 ]

// Сортировка по убыванию
nums.sort((a, b) => b - a);
console.log(nums);   // [ 6, 4, 2, 1, -3, -8 ]
```

---

### Быстрое создание массива

Вариант 1.

```javascript
const list = new Array(5);
console.log(list);   // [ <5 empty items> ]
// list.fill(1);
// console.log(list);   // [ 1, 1, 1, 1, 1 ]
list.fill(1, 0, 3);  // 1 - элемент для заполнения, 0 - индекс(старт), 3 - колиество элементов
console.log(list);   // [ 1, 1, 1, <2 empty items> ]
```

Вариант 2.

```javascript
const list = Array.from({length: 5}, (c, i) => i + 1);
console.log(list);  // [ 1, 2, 3, 4, 5 ]
```

---
