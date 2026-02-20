## Основы

### Комментарии

```javascript
// Однострочный комментарий

/*
Многострочный
комментарий
*/
```

### Переменные и значения

```javascript
let num = 5;       // let - ключевое слово при объявлении переменной
num = 10;
console.log(num);  // 10

const pi = 3.14;   // const - ключевое слово для константы
// pi = 1.2; - попытка перезаписать выведет ошибку TypeError: Assignment to constant variable.
console.log(pi);
```

### Оператор
(Функция в JS)
- Операторы присваивания ( =, +=, -=, *=, /= → let x = 5; x += 2; )
- Операторы сравнения ( ==, ===, !=, !==, >, <, >=, <= → 5 === '5' )
- Арифметические операторы ( +, -, *, /, %, ** → 2 + 3, 5 % 2 )
- Битовые операторы ( &, |, ^, ~, <<, >>, >>> → 5 & 1 )
- Логические операторы ( &&, ||, ! → true && false )
- Строковые операторы ( + (конкатенация), += → 'Hello' + ' World' )
- Тернарный оператор ( condition ? a : b → age > 18 ? 'adult' : 'child' )
- Оператор запятая ( , → (x = 1, y = 2) )
- Унарные операторы ( +, -, ++, --, typeof, delete → ++i, typeof x )
- Операторы отношения ( in, instanceof → 'x' in obj, arr instanceof Array )

Арифметические операторы (+, -, *, /, %, **)

```javascript
const a = 5;
const b = 3;
console.log(a + b);   // Сложение: 8
console.log(a - b);   // Вычитание: 2
console.log(a / b);   // Деление: 1.6666666666666667
console.log(a % b);   // Остаток от деления: 2
console.log(a ** b);  // Возведение в степень: 125
```

Строковые операторы (+, +=)

```javascript
let a = 'Hello';
let b = 'World!';
console.log(a + ' ' + b);     // Hello World!
a += ' JavaScript!';
console.log(a);               // Hello JavaScript!
console.log('Number: ' + 1);  // Number: 1
```

Операторы присваивания (=, +=, -=, *=, /=)

```javascript
let age = 18;           // Присваивание переменной age знаения 18
console.log(age += 2);  // Сложение с присваиванием: 20
console.log(age -= 2);  // Вычитание с присваиванием: 18
console.log(age *= 2);  // Умножение с присваиванием: 36
console.log(age /= 2);  // Деление с присваиванием: 18
```

Операторы сравнения (==, ===, !=, !==, >, <, >=, <=)

`==` - Нестрогое равенство (Абстрактное равенство, cравнение с приведением типов). Проверяет равенство значений, допуская преобразование типов.
`===` - Строгое равенство (Идентичность). Проверяет равенство значений и типов данных без преобразования.
`!=` - Нестрогое неравенство.
`!==` - Строгое неравенство.
`>` - Больше.
`<` - Меньше.
`>=` - Больше или равно.
`<=` - Меньше или равно.

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

Важно! Переменная не имеет определенный тип. Тип имеет значение, которые мы присваиваем переменной.


### Шаблонные строки
Backtick (`) - обратная кавычка. Аналог f-строки в Python.

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

###Преобразование типов

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
