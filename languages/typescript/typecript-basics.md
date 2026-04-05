### Обзор языка

TypeScript - строго типизированное надмножество JavaScript, которое компилируется (транспилируется) в чистый JavaScript. Любой корректный JS-код является валидным TS-кодом, но TS добавляет статическую проверку типов.

* **Статическая типизация** - Типы переменных, параметров и возвращаемых значений проверяются на этапе компиляции, а не во время выполнения. Это позволяет отловить ошибки до запуска программы.
* * **Строгая (опциональная) типизация** - Можно использовать any или не указывать типы — TS будет выводить их автоматически (type inference), но лучше указывать явно.
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

Установка TypeScript.

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

Для компиляции `test.ts` в `test.js`, в терминале вводим команду:

```bash
npx tsc
```

Команда `npx tsc` без аргументов компилирует все `.ts` файлы. Можно компилировать один файл явно: `npx tsc test.ts`. В корне проекта создастся файл `test.js`:

```javascript
"use strict";
Object.defineProperty(exports, "__esModule", { value: true });
const n = 5;
//# sourceMappingURL=test.js.map
```

### Компиляция и запуск

```bash
tsc script.ts          # компилирует в script.js
node script.js         # запуск скомпилированного JS
# Или с помощью ts-node (без явной компиляции):
ts-node script.ts
```

Настройка `tsc --watch`

```bash
npx tsc --watch
```

`--watch` пересобирает `.ts` в `.js` автоматически при изменениях. Компилятор переходит в режим наблюдения (**watch mode**) и блокирует терминал для ввода, потому что сам следит за изменениями файлов.

Запуск кода (новый Терминал)

```bash
node test.js
```

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
