### Обзор языка

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

Для компиляции `test.ts` в `test.js`, в Терминале вводим команду:

```bash
npx tsc
```

В корне проекта создастся файл `test.js`. Команда `npx tsc` без аргументов компилирует все `.ts` файлы. Можно компилировать один файл явно: `npx tsc test.ts`.

```javascript
"use strict";
Object.defineProperty(exports, "__esModule", { value: true });
const n = 5;
//# sourceMappingURL=test.js.map
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
