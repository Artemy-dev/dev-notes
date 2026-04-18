## Create React App (CRA)
Официальный шаблон от **React** для быстрого создания одностраничных приложений без ручной настройки сборки. 
Когда вы запускаете команду `npx create-react-app my-app`, вы получаете уже готовое окружение, в котором "под капотом" скрыт настроенный `Webpack`, `Babel`, `ESLint` и другие инструменты.

## Почему CRA - не всегда лучшее решение?
CRA содержит множество настроек и зависимостей, которые могут быть не нужны в конкретном проекте. 
При ручной настройке `Webpack` вы точно знаете, как работает сборка, можете подключить только нужные лоадеры/плагины, оптимизировать бандл под специфические задачи.

## Создание собственной инфраструктуры React-приложения
Инициализация приложения:

```
npm init
```

Создадим в проекте файл с названием `webpack.config.js`:

```js
const path = require('path');  // Импортируем пакет path

module.exports = {
    entry: path.resolve(__dirname, './src/index.js'),  // Точка входа для работы Webpack
    module: {  // Набор правил для работы с различными файлами проекта
        rules: [  // Конкретное правило для определённых типов файлов
            {
                test: /\.(js|jsx)$/,  // Указываем все js- и jsx-файлы
                exclude: /node_modules/,
                use: [],
            },
        ],
    },
    resolve: {  // Способ работы с модулями
        extensions: ['*', '.js', '.jsx'],
    },
    output: {  // Настройка скомпилированного проекта
        path: path.resolve(__dirname, './dist'),  // Путь и название директории, где расположится скомпилированный проект
        filename: 'bundle.js',  // Название бандла. Бандл - скомпилированный JS
    },
    devServer: {  // Локальный сервер для разработки
        static: path.join(__dirname, './dist'),  // директория, из которой код подтягивается на сервер
        compress: true,
        port: 3000,
    },
};
```

## Babel

`Webpack` позволяет собрать все компоненты проекта в один большой JavaScript-файл, а `Babel` пытается говорить с браузером на одном языке. 
`Babel` преобразует новые фичи последних JavaScript-спецификаций в код, понятный всем браузерам. Он нужен и самому **React**. 
По умолчанию JSX-синтаксис и `.jsx` файлы не поддерживаются браузерами. `Babel` же транспилирует весь JSX-код в обычный JavaScript.

Установка:
```
npm install --save-dev @babel/core @babel/preset-env @babel/preset-react babel-loader
```

Создадим в проекте файл конфигурации Babel с названием `.babelrc`:

```js
{
  "presets": [
    "@babel/preset-env",
    "@babel/preset-react"
  ]
} 
```

Babel + Webpack (добавим строку `'babel-loader'` в массиве `use: []` в файле `webpack.config.js`):

```js
const path = require('path');  // Импортируем пакет path

module.exports = {
    entry: path.resolve(__dirname, './src/index.js'),  // Точка входа для работы Webpack
    module: {  // Набор правил для работы с различными файлами проекта
        rules: [  // Конкретное правило для определённых типов файлов
            {
                test: /\.(js|jsx)$/,  // Указываем все js- и jsx-файлы
                exclude: /node_modules/,
                use: ['babel-loader'],  // <- Сообщаем Webpack, что для работы с js-, jsx-файлами следует использовать babel-loader
            },
        ],
    },
```

Структура проекта:

```
dist/
    index.html
node_modules/
src/
    index.js
.babelrc
package-lock.json
package.json
webpack.config.js 
```

## React + Webpack

Установка react и react-dom:

```
npm install --save react react-dom
```

src/index.js:

```js
import React from 'react';
import ReactDOM from 'react-dom/client';

const title = 'React с Webpack и Babel';

const root = ReactDOM.createRoot(document.getElementById('app'));
root.render(<h1>{title}</h1>);
```

dist/index.html:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Hello React</title>
  </head>
  <body>
    <div id="app"></div>
    <script src="./bundle.js"></script>
  </body>
</html>
```

Установка Webpack:

```
npm install --save-dev webpack webpack-cli webpack-dev-server
```

Настройка окружения. В `package.json` добавить в `"scripts": {}` команду `start`:

```json
{
  "name": "react_app",
  "version": "1.0.0",
  "description": "",
  "license": "ISC",
  "author": "",
  "type": "commonjs",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "webpack serve --mode=development"
  },
  "devDependencies": {
    "@babel/core": "^7.29.0",
    "@babel/preset-env": "^7.29.2",
    "@babel/preset-react": "^7.28.5",
    "babel-loader": "^10.1.1",
    "webpack": "^5.106.2",
    "webpack-cli": "^7.0.2",
    "webpack-dev-server": "^5.2.3"
  },
  "dependencies": {
    "react": "^19.2.5",
    "react-dom": "^19.2.5"
  }
}
```

Запуск проекта:

```
npm start
```
