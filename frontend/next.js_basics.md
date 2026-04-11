**React** - это фронтенд-библиотека для отрисовки интерфейсов. Работает в браузере пользователя (на клиенте). Его задача - взять данные и нарисовать HTML-элементы, а также обновлять их при изменении данных без перезагрузки страницы.

**Next.js** - это фреймворк, который включает React и многое другое. Работает и на сервере, и на клиенте.

### Создание проекта

```bash
npx create-next-app@latest
```

```text
Need to install the following packages:
create-next-app@16.2.3
Ok to proceed? (y)
```

Нажимаем: `y`

```text
What is your project named? » my-app
```

my-app - имя проекта (оставляем по умолчанию, нажимаем Enter или указываем свое).

```text
? Would you like to use the recommended Next.js defaults? » - Use arrow-keys. Return to submit.  
>   Yes, use recommended defaults
    TypeScript, ESLint, No React Compiler, Tailwind CSS, No src/ directory, App Router, AGENTS.md
    No, customize settings
```

Выбираем: `Yes, use recommended defaults`

### Структура проекта

* `.next/` - служебная папка, создаётся при сборке (next build). Содержит скомпилированные файлы (клиентский и серверный код, кеш). Не редактируется вручную, можно игнорировать в Git (обычно уже в .gitignore).
* `app/` - главная рабочая папка с роутингом App Router. Здесь лежат страницы (page.tsx), лейауты (layout.tsx) и другие специальные файлы. Каждая подпапка создаёт маршрут.
* `node_modules/` - все установленные зависимости (библиотеки). Не трогать и не коммитить (добавлена в .gitignore).
* `public/` - статические файлы, которые отдаются "как есть". Доступны по корневому URL, например /logo.png.
* `.gitignore` - список файлов/папок, которые Git не должен отслеживать.
* `AGENTS.md` / `CLAUDE.md` - файлы для AI-агентов. Содержат инструкции/контекст для ИИ-помощников.
* `eslint.config.mjs` - конфигурация ESLint (линтер) для проверки кода на ошибки и единообразие.
* `next-env.d.ts` - автоматически сгенерированный файл, который подключает типы Next.js к TypeScript. Не редактируется.
* `next.config.ts` - конфигурационный файл Next.js. Здесь настраивают переопределения webpack, редиректы, переменные окружения и т.д.
* `package-lock.json` - точный снимок дерева зависимостей для воспроизводимых установок (автоматически управляется npm).
* `package.json` - манифест проекта: список зависимостей, скрипты (dev, build, start), версия и т.д.
* `postcss.config.mjs` - конфигурация PostCSS, используется Tailwind CSS для обработки стилей.
* `README.md` - файл с описанием проекта (стандарт для GitHub/repo).
* `tsconfig.json` - настройки TypeScript (пути, строгость, target и пр.).

### Запуск проекта

```bash
npm run dev
```

### Установка и настройка Stylelint

Stylelint - это линтер для CSS/SCSS, который помогает поддерживать чистоту и единообразие стилей.

```bash
npm install --save-dev stylelint stylelint-config-standard stylelint-order stylelint-config-recess-order
```

Сокращенный вариант:

```bash
npm i -D stylelint stylelint-config-standard stylelint-order stylelint-config-recess-order
```

* `stylelint` - линтер, проверяет CSS/SCSS на ошибки и нарушения правил.
* `stylelint-config-standard` - базовый набор правил (стандарт), от которого можно отталкиваться.
* `stylelint-order` - плагин, добавляющий правила для сортировки свойств в CSS-блоках (например, порядок `margin`, `padding`, `width`).
* `stylelint-config-recess-order` - готовая конфигурация для плагина `stylelint-order`, которая задаёт общепринятый логичный порядок CSS-свойств (сначала позиционирование, затем размеры, отступы, шрифты, декоративные свойства и т.д.).

Установить официальную конфигурацию `Stylelint` для `Tailwind`:

```bash
npm i -D stylelint-config-tailwindcss
```

Создать файл конфигурации `stylelint.config.js`:

```javascript
module.exports = {
  extends: [
    'stylelint-config-standard',      // базовые правила CSS
    'stylelint-config-recess-order',  // правильный порядок свойств
    'stylelint-config-tailwindcss'    // добавляем поддержку Tailwind
  ],
};
```

Включаем плагин `Stylelint` и отредактируем `package.json`:

```json
"scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "eslint",
    "stylelint": "stylelint \"**/*.css\" --fix"
  },
```

Запуск `Stylelint`.

```bash
npm run stylelint
```

Найдет ошибки, которые есть в текущих .css файлах и исправит их.

### Отладка (VSCode)

Включить плагин `JavaScript Debugger`. В корне проекта создать папку `.vscode` -> внутри создать файл `launch.json`.

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Next.js: debug server-side",
      "type": "node-terminal",
      "request": "launch",
      "command": "npm run dev"
    },
    {
      "name": "Next.js: debug client-side",
      "type": "chrome",
      "request": "launch",
      "url": "http://localhost:3000"
    },
    {
      "name": "Next.js: debug full stack",
      "type": "node",
      "request": "launch",
      "program": "${workspaceFolder}/node_modules/next/dist/bin/next",
      "runtimeArgs": ["--inspect"],
      "skipFiles": ["<node_internals>/**"],
      "serverReadyAction": {
        "action": "debugWithChrome",
        "killOnServerStop": true,
        "pattern": "- Local:.+(https?://.+)",
        "uriFormat": "%s",
        "webRoot": "${workspaceFolder}"
      }
    }
  ]
}
```

Установить пакет `cross-env`, который нормализует задание переменных окружения на любой ОС.

```bash
npm install --save-dev cross-env
```

Отредактировать `"scripts"` в `package.json`:

```json
"scripts": {
    "dev": "next dev",
    "debug": "cross-env NODE_OPTIONS=--inspect next dev",
    "build": "next build",
    "start": "next start",
    "lint": "eslint",
    "stylelint": "stylelint \"**/*.css\" --fix"
  },
```

### Metadata (метаданные)

layout.tsx задаёт базовые метаданные для всего сегмента и его дочерних страниц.

```tsx
export const metadata: Metadata = {
  title: "Create Next App",
  description: "Generated by create next app",
};
```

Добавим метаданные в `page.tsx`:

```tsx
...
import { Metadata } from 'next';

export const metadata: Metadata = {
  title: "Учебный проект",
};

export default function Home() {
...
```

`page.tsx` имеет более высокий приоритет и может переопределить часть полей, оставляя остальные поля из родительского макета без изменений. Таким образом, при загрузке вашей страницы итоговый объект метаданных будет выглядеть так:

```tsx
{
  title: "Учебный проект",                     // из page.tsx
  description: "Generated by create next app"  // из layout.tsx
}
```

### Динамические метаданные

Если нужно подтянуть данные из API, вместо экспорта константы используется функция `generateMetadata`.

```tsx
// export const metadata: Metadata = {
//   title: "Учебный проект",
// };

export async function generateMetadata(): Promise<Metadata> {
  const dataAPI: string = 'API_MetaData';  // ... данные из API
  return {
    title: dataAPI
  }
}
```
