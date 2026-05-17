### Создание проекта (Vite + React + JavaScript)

**Vite** - инструмент сборки, который ускоряет процесс разработки фронтенд-проектов за счёт нативной поддержки ES-модулей (встроенный в браузер способ импортировать файлы без склеивания всего проекта) и использования esbuild для предварительного объединения сторонних библиотек.

**React** - библиотека для создания пользовательских интерфейсов, которая позволяет строить приложение из переиспользуемых компонентов (функций, возвращающих HTML-подобную разметку JSX) и автоматически обновляет страницу при изменении данных благодаря виртуальному DOM.

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

### Очистка проекта (опционально)

**public/**:

* `favicon.svg` - удаляем файл.
* `icons.svg` - удаляем файл.

**src/**:

* `assets/` - удаляем каталог.
* `App.css` - удаляем файл.
* `index.css` - удаляем файл.
* `App.jsx` - очищаем содержимое
* `main.jsx` - очищаем строку `import './index.css'`.

```js
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import App from './App.jsx'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>,
)
```

### Компоненты в React

Компоненты - независимая, переиспользуемая часть пользовательского интерфейса (UI), которая инкапсулирует в себе структуру (разметку), логику и часто стили.

**Создаем React-компонент (RFC).** Файл `App.jsx`:

```js
function App() {

  return (
    <div>
      <Header/> {/* Подключаем компонент */}
      <Catalog/>
      <Footer/>
    </div>
  )
}

// Создаем компонент Header (функция с именем с заглавной буквы)
function Header() {
  // Компонент возвращает ТОЛЬКО один элемент
  return(
    <header>
      <h1>E-Store</h1>
    </header>
  )
}

function Catalog() {
  return (
    <main>
      <ul>
        <Product/> {/* Вкладываем компонент Product в компонент Catalog */}
      </ul>
    </main>
  )
}

function Product() {
  return <li>Product</li>
}

function Footer(params) {
  return <footer>Footer</footer>
}

export default App
```

### JavaScript Syntax Extension (JSX)

`.jsx` - это синтаксическое расширение JavaScript, позволяющее писать разметку, похожую на HTML, прямо в JS-коде.
Фигурные скобки `{}` используются для вставки JavaScript-выражений внутрь JSX-разметки.

```js
const productData = [
  {
    name: "Laptop Pro",
    description: "High-performance laptop for professionals.",
    price: 1200,
    photoName: "/laptop.png",
    soldOut: false,
  },
]

function Product() {
  return <li>
    <img src={productData[0].photoName} alt="" />  // Аналогично: <img src="/laptop.png" alt="" />
  </li>
}
```

### Рендер условий в JSX

```js
function Header() {
  const hour = new Date().getHours();
  const openHour = 8;
  const closeHour = 20;
  
  // let isOpen;
  // if (hour >= openHour && hour < closeHour) {
  //   isOpen = true;
  // } else {
  //   isOpen = false;
  // }
  const isOpen = hour >= openHour && hour < closeHour; // Лаконичная запись

  // Компонент возвращает ТОЛЬКО один элемент
  return(
    <header>
      <h1>E-Store</h1>
      <nav>
        <ul>
          <li><a href="#home">Главная</a></li>
          <li><a href="#catalog">Каталог</a></li>
          <li><a href="#about">О нас</a></li>
          <li><a href="#contacts">Контакты</a></li>
        </ul>
      </nav>
      <div>
        {isOpen ? <p>Мы открыты. Время работы с {openHour}:00 до {closeHour}:00</p> : 
        <p>Мы закрыты. Приходите завтра с {openHour}:00</p>}
      </div>
    </header>
  )
}
```

### Стили в React

**Inline-стили** - стили, которые пишутся прямо внутри JSX-элемента через атрибут style. В React это не строка, а JavaScript-объект, где свойства CSS пишутся в camelCase (например, backgroundColor, а не background-color).

Синтаксис: `<tag style={ { key: "value" } }> ... </tag>`

```js
<header>
  <h1 style={{ color: "blue", fontSize: "3.2rem" }}>E-Store</h1>
</header>
```

*Глобальные стили** - стили, описанные в отдельном .css-файле, которые действуют на всё приложение целиком.

В каталоге `src/` создаем файл `index.css` и прописываем в нем стили. Пример:

```css
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;700&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  font-size: 62.5%;
}

body {
  font-family: "Montserrat", sans-serif;
  color: #1e1e1e;
  background-color: #ffffff;
  min-height: 100vh;
  padding: 4rem;
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Header */
.header {
  align-self: stretch;
  text-align: center;
  padding: 1.5rem 0;
  background-color: #41546a;
  color: #ffffff;
  border-radius: 0.5rem;
  margin-bottom: 2rem;
}
```

Импортируем в `App.jsx`:

```js
import "./index.css";
```

Применение классов через атрибут `className`:

```js
<header className="header">
  <h1>E-Store</h1>
</header>
```

### Относительные и абсолютные пути в React (Vite)

**Относительный пути** - путь, который строится от текущего файла. Начинается с `./` или `../`.

```js
import "./index.css" // './' - в текущем каталоге
import "../public/icon.svg" // '../' - на уровень выше
```

**Абсолютный путь (рекомендуется)** - путь от корня проекта (папки `src`). Начинается с `/` или `@/` (если настроен алиас).

```js
import "/src/index.css"
```

### Модули. Export / Import

Каждый файл JS - **модуль**. Пример модулей: `App.jsx`, `index.css`, `main.jsx`.

**Export** - отправка части кода.

**Экспорт по умоланию (export default)**

```js
function App() {
  return (
    <div>
      <Header/>
      <Catalog/>
      <Footer/>
    </div>
  )
}

export default App

// Альтернативный вариант записи:

// export default function App() {
//   return (
//     <div>
//       <Header/>
//       <Catalog/>
//       <Footer/>
//     </div>
//   )
// }
```

**export default** - экспорт по умолчанию, когда из модуля экспортируется одно основное значение (функция, класс, объект, переменная). 
Может быть только один `export default` на файл.
При импорте имя может быть любым (не обязательно совпадать с оригинальным).

**Import** - получение части кода из другого модуля.

```js
// main.jsx
import App from './App.jsx' // Импортируем объект App из App.jsx в main.jsx
// import MyApp from './App.jsx' // Работает так же (имя может быть любым)
```

**Именованный экспорт (export)**

```js
// App.jsx:

export function Header() {
  const hour = new Date().getHours();
  const openHour = 8;
  const closeHour = 20;
  const isOpen = hour >= openHour && hour < closeHour;

// main.jsx:

import { Header } from './App.jsx'
// import { Header as HeaderComponent } from './App.jsx'
// import * as AppModule from './App.jsx' // Затем использовать: AppModule.Header(), AppModule.Footer()
```

**export** - именованный экспорт, когда из модуля экспортируется несколько значений с конкретными именами.
Может быть сколько угодно именованных экспортов в одном файле.
При импорте имя должно совпадать с именем экспорта (обязательно в фигурных скобках).
Можно переименовывать при импорте через `as`.

### Props

**Props** - входные параметры компонента, передаваемые ему при рендеринге. Props всегда передаются в виде объекта и доступны как первый аргумент функции компонента.

```js
const productData = [
  {
    name: "Laptop Pro",
    description: "High-performance laptop for professionals.",
    price: 1200,
    photoName: "/laptop.png",
  },
  {
    name: "Smartphone X",
    description: "Latest model with stunning display.",
    price: 800,
    photoName: "/smartphone.png",
  }
]

function Catalog() {
  return (
    <main className="calalog">
      <ul className="products">
        {/* Вкладываем компонент Product в компонент Catalog */}
        <Product
          photoName = "/laptop.png"
          name="Laptop Pro"
          description="High-performance laptop for professionals."
          price={1200} // price="1200" - строка, price={1200} - число
        />
        <Product
          photoName = "/smartphone.png"
          name="Smartphone X"
          description="Latest model with stunning display."
          price={800}
        />
      </ul>
    </main>
  )
}

function Product(props) {
  console.log(props);
  return <li className="product">
    <img src={props.photoName} alt={props.name} />
    <div>
      <h3>{props.name}</h3>
      <p>{props.description}</p>
      <span>{props.price}</span>
    </div>
  </li>
}
```

* Ключи - имена атрибутов из JSX (`photoName`, `name`, `description`, `price`)
* Значения - переданные значения (`"/laptop.png"`, `"Laptop Pro"` и т.д.)

`console.log(props);` выведет в консоль:

```js
{
    "photoName": "/laptop.png",
    "name": "Laptop Pro",
    "description": "High-performance laptop for professionals.",
    "price": 1200
}
```

### Рендер компонентов. Props + map()

```js
// Тестовые данные
const productData = [
  {
    name: "Laptop Pro",
    description: "High-performance laptop for professionals.",
    price: 1200,
    photoName: "/laptop.png",
    soldOut: false,
  },
  {
    name: "Smartphone X",
    description: "Latest model with stunning display.",
    price: 800,
    photoName: "/smartphone.png",
    soldOut: false,
  },
  {
    name: "Wireless Headphones",
    description: "Noise-cancelling headphones with great sound quality.",
    price: 200,
    photoName: "/headphones.png",
    soldOut: false,
  },
  {
    name: "Smartwatch Z",
    description: "Stylish smartwatch with fitness tracking features.",
    price: 150,
    photoName: "/smartwatch.png",
    soldOut: false,
  },
  {
    name: "Gaming Console",
    description: "Powerful gaming console for endless fun.",
    price: 400,
    photoName: "/console.png",
    soldOut: true,
  },
  {
    name: "4K TV",
    description: "Ultra HD television with vibrant colors.",
    price: 1000,
    photoName: "/tv.png",
    soldOut: false,
  },
];

function App() {
  return (
    <div>
      <Catalog/>
    </div>
  )
}

// Вариант 1 (отдельные пропы). Предпочтительнее
function Catalog() {
  return (
    <main className="catalog">
      <ul className="products">
        {productData.map(product => 
        <Product 
          name={product.name}
          description={product.description}
          price={product.price}
          photoName={product.photoName}
        />)}
      </ul>
    </main>
  )
}

function Product(props) {
  return <li className="product">
    <img src={props.photoName} alt={props.name} />
    <div>
      <h3>{props.name}</h3>
      <p>{props.description}</p>
      <span>{props.price}</span>
    </div>
  </li>
}
```

Вариант 2 (передача всего объекта)

```js

function Catalog() {
  return (
    <main className="catalog">
      <ul className="products">
        {productData.map(product => 
        <Product productObj={product}/>)}
      </ul>
    </main>
  )
}

function Product(props) {
  return <li className="product">
    <img src={props.productObj.photoName} alt={props.productObj.name} />
    <div>
      <h3>{props.productObj.name}</h3>
      <p>{props.productObj.description}</p>
      <span>{props.productObj.price}</span>
    </div>
  </li>
}
```

Объяснение:
* Массив `productData` содержит тестовые данные (объекты товаров).
* В компоненте `Catalog` перебираем массив с помощью метода `map()`.
* Метод `map()` на каждой итерации передает текущий объект товара в функцию.
* В варианте 1: объект называется `product`, и каждый его параметр передается отдельным пропом.
* В варианте 2: объект называется `productObj` и передается целиком как один проп.
* Дочерний компонент `Product` получает пропы и отрисовывает данные.

### Деструктуризация

```js
function Product({productObj}) { // Передаем {productObj}, вместо props
  return <li className="product">
    <img src={productObj.photoName} alt={productObj.name} />
    <div>
      <h3>{productObj.name}</h3>
      <p>{productObj.description}</p>
      <span>{productObj.price}</span>
    </div>
  </li>
}
```
