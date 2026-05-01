### Создание проекта (Vite + React + JavaScript)

**Vite** - инструмент сборки, который ускоряет процесс разработки фронтенд-проектов за счёт нативной поддержки ES-модулей (встроенный в браузер способ импортировать файлы без склеивания всего проекта) и использования esbuild для предварительного объединения сторонних библиотек.

**Установка:**

```
npm create vite
```

* Указываем имя проекта (`Project name`).
* Выбираем фреймворк (`Select a framework: React`).
* Выбираем язык (`Select a variant: JavaScript`)

```bash
PS C:\Users\hello\Documents\JS> npm create vite
Need to install the following packages:
create-vite@9.0.6
Ok to proceed? (y) y

> npx
> create-vite

|
o  Project name:
|  learn-project
|
o  Select a framework:
|  React
|
o  Select a variant:
|  JavaScript
|
o  Install with npm and start now?
|  Yes
|
o  Scaffolding project in C:\Users\hello\Documents\JS\learn-project...
|
o  Installing dependencies with npm...

added 136 packages, and audited 137 packages in 32s

31 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
|
o  Starting dev server...

> learn-project@0.0.0 dev
> vite                       
```

Сообщение после завершения установки:

```
  VITE v8.0.10  ready in 501 ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: use --host to expose
  ➜  press h + enter to show help
```

**Структура проекта:**

```
ProjectName/
├── node_modules/          - все установленные зависимости (библиотеки) проекта
├── public/                - статические файлы (иконки, изображения), которые копируются как есть
│   ├── favicon.svg        - иконка сайта (вкладка браузера)
│   └── icons.svg          - спрайт с иконками
├── src/
│   ├── assets/            - изображения, шрифты, стили, обрабатываемые Vite
│   ├── App.css            - стили главного компонента App
│   ├── App.jsx            - главный компонент React (основная логика и разметка)
│   ├── index.css          - глобальные стили для всего приложения
│   └── main.jsx           - точка входа (рендерит App в DOM)
├── .gitignore             - список файлов/папок, которые Git игнорирует (node_modules и др.)
├── eslint.config.js       - настройки линтера ESLint (проверка кода на ошибки)
├── index.html             - главная HTML-страница (точка входа для браузера)
├── package-lock.json      - точная фиксация версий всех зависимостей
├── package.json           - метаинформация о проекте, список зависимостей, скрипты
├── README.md              - документация/описание проекта
└── vite.config.js         - конфигурация сборщика Vite
```

*Важно: Если `node_modules/` не появилась - необходимо выполнить команду: `npm install` или `npm i`.*

**Запуск проекта:**

```
npm run dev
```

**Остановить проект:** `Ctrl+C`.

**Итоговая последовательность:**

```
npm create vite                 # 1. Создать проект (node_modules нет)
cd my-project                   # 2. Перейти в папку проекта
npm install                     # 3. Установить зависимости (если node_modules не появилась автоматически)
npm run dev                     # 4. Запустить проект
```
