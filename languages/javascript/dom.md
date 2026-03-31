### Что такое DOM (Document Object Model)

**DOM (Document Object Model)** - это программный интерфейс (прослойка), который представляет HTML-документ в виде дерева объектов, с которыми JavaScript может взаимодействовать: читать, изменять, удалять существующие элементы и создавать новые. DOM - это мост, который позволяет JS "видеть" и "менять" HTML-страницу. Пример работы DOM:

* **Из HTML в JS:** JS находит элемент, например кнопку (<button>) через DOM и "вешает" на нее обработчик клика
* **Логика в JS:** при клике происхоит событие, например, увеличивается переменная-счетчик
* **Из JS в HTML:** JS обновляет содержимое страницы через DOM, и пользователь видит новое значение на странице

### Структура DOM

```html
<!-- HTML-КОД (исходная разметка) -->
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Заголовок страницы</title>
    <script src="./script.js"></script>
</head>
<body>
    <header></header>
    <main></main>
    <footer></footer>
</body>
</html>
```

```text
# Дерево узлов
Document
├── DOCTYPE
└── html
    ├── head
    │   ├── meta
    │   ├── meta
    │   ├── title
    │   │   └── text node
    │   └── script
    └── body
        ├── header
        ├── main
        └── footer
```

### Базовый HTML и CSS

```html
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <title>DOM</title>
    <link rel="stylesheet" href="styles.css">
    <script src="script.js" defer></script>
</head>
<body>
    <div class="panel">JavaScript</div>
    <input class="input" placeholder="Введите текст">
    <button class="button">Изменить</button>
    <div class="message"></div>

    <ul id="todoList" class="todo-list">
        <li>Задача 1</li>
        <li>Задача 2</li>
        <li>Задача 3</li>
    </ul>
    <div class="list-controls">
        <input type="text" id="newTodo" placeholder="Новая задача">
        <button id="addTodo">Добавить</button>
        <button id="removeLastTodo">Удалить последнюю</button>
    </div>

    <form id="testForm">
        <input type="text" id="formInput" placeholder="Введите что-то">
        <button type="submit">Отправить</button>
        <div class="form-message"></div>
    </form>

    <div id="testHtml" class="test-block">Текст с <strong>HTML-тегом</strong></div>
    <div class="html-demo-buttons">
        <button id="showTextContent">textContent</button>
        <button id="showInnerText">innerText</button>
        <button id="showInnerHTML">innerHTML</button>
    </div>

    <div class="panel" data-id="123" data-role="main-panel">Панель с data-атрибутами</div>
</body>
</html>
```

```html
<!-- 
class="panel"        - основной блок для отображения текста
class="input"        - поле ввода текста
class="button"       - кнопка для отправки
class="message"      - блок для вывода сообщений

id="todoList"        - список ul для работы с элементами
class="todo-list li" - элементы списка (для делегирования событий)
id="newTodo"         - поле ввода новой задачи
id="addTodo"         - кнопка добавить
id="removeLastTodo"  - кнопка удалить последнюю

id="testForm"        - форма для submit
id="formInput"       - поле ввода в форме
class="form-message" - блок для вывода сообщений формы

id="testHtml"        - блок с HTML-тегом внутри
id="showTextContent" - кнопка для textContent
id="showInnerText"   - кнопка для innerText
id="showInnerHTML"   - кнопка для innerHTML

class="panel"        - панель с data-id="123" и data-role="main-panel"

defer                - скрипт выполняется после полной загрузки HTML
class                - класс для CSS и JS (через точку)
id                   - уникальный идентификатор (через #)
data-*               - пользовательские атрибуты для хранения данных
placeholder          - подсказка в поле ввода
type="submit"        - кнопка отправки формы
-->
```

```css
.panel {
    background: #4CAF50;
    color: white;
    padding: 20px;
    width: 300px;
    text-align: center;
    margin: 10px auto;
}

.input {
    display: block;
    width: 280px;
    padding: 10px;
    margin: 10px auto;
}

.button {
    background: #4CAF50;
    color: white;
    padding: 10px 20px;
    border: none;
    cursor: pointer;
    margin: 10px auto;
    display: block;
}

.message {
    text-align: center;
    margin: 10px auto;
    font-size: 14px;
}

.hidden {
    display: none;
}

.highlight {
    background: orange;
    color: black;
}

.todo-list {
    width: 300px;
    margin: 20px auto;
    padding: 0;
    list-style: none;
}

.todo-list li {
    background: #f0f0f0;
    padding: 10px;
    margin: 5px 0;
    cursor: pointer;
    border-radius: 4px;
    transition: background 0.2s;
}

.todo-list li:hover {
    background: #e0e0e0;
}

.list-controls {
    text-align: center;
    margin: 10px auto;
}

.list-controls input {
    padding: 8px;
    width: 200px;
}

.list-controls button {
    padding: 8px 12px;
    margin: 0 5px;
    cursor: pointer;
}

#testForm {
    width: 300px;
    margin: 20px auto;
    text-align: center;
    padding: 15px;
    border: 1px solid #ddd;
    border-radius: 8px;
}

#testForm input {
    width: 100%;
    padding: 8px;
    margin-bottom: 10px;
    box-sizing: border-box;
}

#testForm button {
    padding: 8px 20px;
    cursor: pointer;
}

.form-message {
    margin-top: 10px;
    font-size: 14px;
    color: #666;
}

.test-block {
    width: 300px;
    margin: 20px auto;
    padding: 10px;
    border: 1px solid #ccc;
    background: #f9f9f9;
    text-align: center;
}

.html-demo-buttons {
    text-align: center;
    margin: 10px auto;
}

.html-demo-buttons button {
    padding: 5px 10px;
    margin: 0 5px;
    cursor: pointer;
}
```

```css
/* 
background  - цвет фона
color       - цвет текста
padding     - внутренний отступ (от содержимого до границы)
margin      - внешний отступ (от границы до соседних элементов)
width       - ширина элемента
text-align  - выравнивание текста (left, center, right)
display     - тип отображения (block - блочный, none - скрыть, flex - гибкий)
border      - рамка (толщина тип цвет, например 1px solid red)
cursor      - вид курсора (pointer - рука, default - стрелка)
font-size   - размер шрифта (px, rem, em)
list-style  - стиль маркеров списка (none - убрать точки)
border-radius - скругление углов (px, %)
transition  - плавное изменение свойств (например background 0.2s)
box-sizing  - как считается ширина (border-box - включает padding и border)
margin-top / margin-right / margin-bottom / margin-left - отступ с конкретной стороны

:hover  - стиль при наведении мыши
:focus  - стиль когда элемент в фокусе
:active - стиль в момент нажатия

px  - пиксели (фиксированный размер)
%   - процент от родительского элемента
auto - автоматический расчет (часто для центрирования)

block    - элемент занимает всю ширину, перенос строки
none     - полностью скрывает элемент
pointer  - курсор в виде руки
center   - выравнивание по центру
solid    - сплошная линия (для border)
border-box - ширина включает padding и border, не выходит за пределы
*/
```

### Поиск элементов

```javascript
// document.querySelector() - возвращает первый найденный элемент
const panel = document.querySelector('.panel');

// document.querySelectorAll() - возвращает все элементы (NodeList)
const allPanels = document.querySelectorAll('.panel');        // С точкой ищет по классу
const allButtons = document.querySelectorAll('button');       // Без точки/хештега ищет по тегу <button>
const todoItems = document.querySelectorAll('#todoList li');  // Ищет ВСЕ <li> ВНУТРИ элемента с id="todoList"

// document.getElementById() - поиск по id
const todoListElement = document.getElementById('todoList');

// Примеры использования (DevTools - Клавиша F12 в браузере -> Console)
console.log(panel);            // Первый .panel
console.log(allPanels);        // Все .panel
console.log(todoListElement);  // Элемент с id="todoList"
```

### Работа с содержимым

```javascript
// element.textContent - Работает с чистым текстом (без тегов). Берёт весь текст из DOM, включая скрытые элементы (display: none)
// Взять текст
const block = document.querySelector('#testHtml');
console.log(block.textContent); // "Текст с HTML-тегом HIDDEN" (тег <strong> исчез)
// Записать текст (теги не сработают, станут простым текстом)
const messageDiv = document.querySelector('.panel');
messageDiv.textContent = '<button>Кликни меня</button>'; // Пользователь увидит строку <button>Кликни меня</button>

// element.innerText - Берёт только видимый текст, учитывает CSS и переносы строк
// Взять текст
console.log(block.innerText);  // "Текст с HTML-тегом"
// Записать текст
messageDiv.innerText = 'Новый текст';

// element.innerHTML - Работает с HTML-разметкой (риск XSS-атаки)
// Взять текст
console.log(block.innerHTML); // "Текст с <strong>HTML-тегом</strong> <span style=\"display:none\">HIDDEN</span>"
// Записать текст
messageDiv.innerHTML = '<button>Кликни меня</button>'; // На странице появится кнопка в панели
// XSS-атака
// const userInput = '<img src=x onerror=alert(1)>';
// messageDiv.innerHTML = userInput;
```

### Работа с атрибутами

```javascript
const panels = document.querySelectorAll('.panel');
const firstPanel = panels[0];  // без data-атрибутов <div class="panel">JavaScript</div>
const secondPanel = panels[1]; // с data-атрибутами <div class="panel" data-id="123" data-role="main-panel">
const input = document.querySelector('.input');

// Получить атрибут - getAttribute()
console.log(secondPanel.getAttribute('data-id'));  // "123"
console.log(input.getAttribute('placeholder'));    // "Введите текст"

// Изменить или добавить атрибут - setAttribute()
secondPanel.setAttribute('data-id', '999');
console.log(secondPanel.getAttribute('data-id'));  // "999"
input.setAttribute('placeholder', 'Новый текст');
console.log(input.getAttribute('placeholder'));    // "Новый текст"

// Проверить наличие - hasAttribute()
console.log(secondPanel.hasAttribute('data-role')); // true
console.log(secondPanel.hasAttribute('title'));     // false

// Удалить атрибут removeAttribute()
secondPanel.removeAttribute('data-role');
console.log(secondPanel);  // <div class="panel" data-id="999">

// Работа с data- (dataset)*
secondPanel.dataset.id = '555';
secondPanel.dataset.newValue = '1';
console.log(secondPanel);  // <div class="panel" data-id="555" data-new-value="1">

// Удаление через dataset
delete secondPanel.dataset.newValue;  // удалит data-new-value="1"
console.log(secondPanel);             // <div class="panel" data-id="555">
```

### Работа со стилями и классами

```javascript

```

### События

```javascript

```

### Управление событиями

```javascript

```

### Создание и удаление элементов

```javascript

```

### Жизненный цикл

```javascript

```
