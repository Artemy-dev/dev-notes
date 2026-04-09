### Обзор языка

TypeScript - строго типизированное надмножество JavaScript, которое компилируется (транспилируется) в чистый JavaScript. Любой корректный JS-код является валидным TS-кодом, но TS добавляет статическую проверку типов.

* **Статическая типизация** - Типы переменных, параметров и возвращаемых значений проверяются на этапе компиляции, а не во время выполнения. Это позволяет отловить ошибки до запуска программы.
* **Строгая (опциональная) типизация** - Можно использовать any или не указывать типы — TS будет выводить их автоматически (type inference), но лучше указывать явно.
* **Транспиляция в JS** - Код на TS преобразуется в JS с помощью компилятора tsc. Результат можно запускать в любой JS-среде (браузер, Node.js).
* **Надмножество JS** - Поддерживает все возможности современного JavaScript (ES6+, модули, async/await) и добавляет свой синтаксис для типов.

### Установка необходимого софта

* **VS Code** - редактор кода [скачать с официального сайта](https://code.visualstudio.com/).
* **Node.js** - среда выполнения JavaScript на компьютере [скачать с официального сайта](https://nodejs.org/en/download).

Проверка установки **Node.js**. Открыть термина и выполнить:

```bash
node -v   # Покажет версию Node.js (например, v24.13.1)
npm -v    # Покажет версию менеджера пакетов npm (например, 11.8.0)
```

### Установка TypeScript

```bash
npm i -D typescript
```

Проверка:

```bash
npx tsc --version   # Покажет версию компилятора языка TypeScript (например, Version 6.0.2)
```

В корне проекта появится каталог: `node_modules` и файлы: `package-lock.json`, `package.json`.

### Создание файла конфигурации для компиляции TS в JS

```bash
npx tsc --init
```

В корне проекта создастся файл `tsconfig.json` - позволяет настроить компиляцию: "target", "module", "outDir" и т.д.

### Первая программа

Создадим файл `test.ts`

```typescript
const n: number = 5;
```

### Компиляция и запуск

Базовая компиляция (tsc) `test.ts` в `test.js`.

```bash
npx tsc test.ts
```

Если не указывать имя файла, `npx tsc` скомпилирует все `.ts`-файлы в текущем проекте (по настройкам `tsconfig.json`).

Запуск без явной компиляции (`ts-node`). Утилита `ts-node` выполняет `.ts`-файл на лету, без создания `.js`.

```bash
ts-node test.ts
```

*Важно: ts-node требует предварительной установки (npm i -D ts-node).*

Автоматическая пересборка (`--watch`). Режим наблюдения (`watch mode`) автоматически перекомпилирует файлы при каждом изменении.

```bash
npx tsc --watch
```

Терминал блокируется - компилятор остаётся активным и отслеживает изменения в `.ts`-файлах. При сохранении файла `tsc` тут же пересобирает его в JavaScript. Для запуска необходимо создать новый терминал и выполнить `node test.js`.

### Типы данных

```typescript
let num: number = 5;       // Число
// num = '5'               // Ошибка: Type 'string' is not assignable to type 'number'.
const str1: string = '5';  // Строка
const str2 = 'text';       // Строка (без явного указания - автоматически приводит к нужному типу)
const res = num + str1;    // Строка
console.log(res);          // 55
const isTrue: boolean = true;               // Булевый/логический тип
const list: string[] = ['1', '2', 'text'];  // Массив (список строк)
const u: undefined = undefined;
const n: null = null;

let a: any = 5;  // Переменная с any может принимать любой тип
a = 'text';      // Ошибки нет, TypeScript не проверяет тип
a = true;        // Тоже допустимо

// Типизация функции
function test1(a: string, b?: number): string | number {
    // a: string - параметр `a` должен быть строгого типа string
    // b?: number - необязательный параметр (знак `?`), если передан - должен быть числом
    // string | number - функция может вернуть значение типа string ИЛИ number (union-тип)
    return '';
}

const test2 = (a: number): number => { return a**2; }

// Сужение типа (type narrowing) - позволяет понять, какой именно тип используется корректно работать c ним
function test3(a: number | string) {
    if (typeof a === 'number') {         // Возвести в квадрат для number
        return a**2;
    } else if (typeof a === 'string') {  // Вызвать toUpperCase для string
        return a.toUpperCase;
    }
}

function test4(): void {  // void - функция ничего не возвращает
    console.log('test');
}

// Типизация объекта с помощью interface (используется по умолчанию)
interface User {
    name: string;    // name: string - обязательное поле типа string
    age: number;     // age: number - обязательное поле типа number
    email?: string;  // email?: string - необязательное поле, если есть - должно быть строкой
}

const user: User = {
    name: "Alice",
    age: 30,
    // email можно не указывать, так как поле опциональное
};

// Типизация объекта с помощью type
type Person = { id: number; name: string; };

const person: Person = { id: 1, name: "Bob" };
```

### Interface / Type

В TS внутри `type` и `interface` в качестве разделителя полей можно использовать запятую (`,`), точку с запятой (`;`) или не ставить разделитель, если поля идут с новой строки (не рекомендуется).

**Interface**

```typescript
interface User {
    login: string,
    password: string
};

//extends
interface userAuth extends User {
    email: string
}

const user: userAuth = {
    login: 'admin',
    password: '1234',
    email: 'ext@mail.com'
};

function getLogin(user: User) {
    console.log(user.login)
}

getLogin(user);  // admin

function getEmail(user: userAuth) {
    console.log(user.email)
}

getEmail(user);  // ext@mail.com
```

```typescript
// Объединение деклараций (declaration merging) / Слияние интерфейсов (interface merging)
interface User {
    login: string
};

interface User {
    password: string
};

const user: User = {
    login: 'admin',
    password: '1234'
};

console.log(user);  // { login: 'admin', password: '1234' }
```

**Type**

```typescript
type User = {
    login: string,
    password: string
};

type userAuth = User & {
    email: string
}

const user: userAuth = {
    login: 'admin',
    password: '1234',
    email: 'ext@mail.com'
};

function getLogin(user: User) {
    console.log(user.login)
}

getLogin(user);  // admin

function getEmail(user: userAuth) {
    console.log(user.email)
}

getEmail(user);  // ext@mail.com

// Создание собственного типа
type text = string;
const a: text = 'Hello';
console.log(a);  // Hello
```

### Cast. Приведение типов (type assertion / type casting)

Способ явно указать TS, что значение имеет определённый тип, чтобы компилятор разрешил операции с ним.

```typescript
const a: unknown = 'hello';
// console.log(a.toUpperCase());  // Ошибка! TS не знает, что это строка, и запрещает
const b = a as string;
console.log(b.toUpperCase());  // HELLO

interface User {
    name: string;
    age: number;
}

const userInfo: any = { name: 'Tim', age: 30 };
const user = userInfo as User;
console.log(user);  // { name: 'Tim', age: 30 }
```

### Литеральные типы

```typescript
type moveType = 'w' | 'a' | 's' | 'd';

function movePlayer(action: moveType) {  // action может быть только 'w', 'a', 's' или 'd'
    switch (action) {
        case 'w':
            'Up'
            break;
        case 'a':
            'Left'
            break;
        case 's':
            'Down'
            break;
        case 'd':
            'Right'
            break;
    }
}
```

### Enums

```typescript
// Enum с явными строковыми значениями
enum Move {
    Up = 'w',   // move.Up = 'w'
    Down = 's'  // move.Down = 's'
}

function run(obj: { Up: string }) {
    console.log('Run Up');
}

run(Move);  // Run Up

// Числовой enum с автоинкрементом (после One = 1 следующему Two присваивается 2)
enum numbers {
    One = 1,  // numbers.One = 1 (если не указать явно, по умолчанию = 0)
    Two,      // numbers.Two = 2 (присваевается по умолчанию)
}

// Гетерогенные enum (содержит числа и строки) - не рекомендуют смешивать типы без необходимости
enum isAdmin {
    Admin = 1,
    NotAdmin = 'NOT'
}

// Расчитываемый enum (только числовые)
enum yesOrNo {
    Yes = 1,
    No = calculateE()  // значение No получается из функции
}

function calculateE(): number {
    return 0
}

console.log(yesOrNo.No);  // 0
```

### Tuple (Кортеж)

Кортеж является подтипом массива и наследует все методы (включая push, pop и т.д.).

```typescript
const t: [number, string, string] = [1, 'hello', 'TS'];
t.push(2);       // .push() - добавляет элемент
console.log(t);  // [ 1, 'hello', 'TS', 2 ]
// console.log(t[3]);  // Ошибка!

// Неизменяемый кортеж (readonly)
const t2: readonly [number, string, string] = [1, 'hello', 'TS'];
// t2.push(2);  // Ошибка!

// Деструктуризация кортежа
const [a, b, c] = t;
console.log(b);  // hello

// Rest-оператор
const [d, ...r] = t;
console.log(d);  // 1
console.log(r);  // [ 'hello', 'TS', 2 ]
```

### Generics (Обобщения)

Позволяют использовать функции для разных типов.

```typescript
// Без использования дженериков
function func1(a: number): number {
    console.log(typeof a);
    return a;
}

function func2(a: string): string {
    console.log(typeof a);
    return a;
}

// Generics (<T>)
function func3<T>(a: T): T {
    console.log(typeof a);
    return a;
}

func3<string>('text');  // string
func3<number>(5);       // number
```
