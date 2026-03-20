## DOM (Document Object Model)

**DOM (Document Object Model)** - это программный интерфейс (прослойка), который представляет HTML-документ в виде дерева объектов, с которыми JavaScript может взаимодействовать: читать, изменять, удалять существующие элементы и создавать новые. DOM - это мост, который позволяет JS "видеть" и "менять" HTML-страницу. Пример работы DOM:

* **Из HTML в JS:** JS находит элемент, например кнопку (<button>) через DOM и "вешает" на нее обработчик клика
* **Логика в JS:** при клике происхоит событие, например, увеличивается переменная-счетчик
* **Из JS в HTML:** JS обновляет содержимое страницы через DOM, и пользователь видит новое значение на странице

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
# СТРУКТУРА DOM (дерево узлов)
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

---

### Выбор и манипуляции с элементами

index.html:

```html
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>app.js</title>
    <script src="./app.js" defer></script>  <!-- Скрипт выполнится после парсинга HTML -->
</head>
<body style="text-align: center;">
    <div class="panel">JavaScript</div>
    <input class="input">
    <button class="button">Change</button>
</body>
</html>
```

app.js:

```javascript
'use strict';

console.log(document.querySelector('.button'));
```

В консоле index.html страницы будет выведено:

```html
<button class="button">Change</button>
```

**document.querySelector()** - это метод, который находит первый элемент на странице, соответствующий указанному CSS-селектору, чтобы мы могли с ним взаимодействовать. Пример взаимодействия после поиска:

```javascript
const button = document.querySelector('.button');
button.textContent = 'Нажми меня';  // меняем текст
button.style.backgroundColor = 'red';  // меняем цвет
button.addEventListener('click', () => {  // вешаем событие
    alert('Клик!');
});
```

---

### Обработка нажатий

Вариант 1. Рекомендуется

```javascript
'use strict';

document.querySelector('.button').addEventListener('click', () => {
    const input = document.querySelector('.input').value;
    const panelText = document.querySelector('.panel')
    panelText.textContent = input;
    document.querySelector('.input').value = '';  // Очищает поле ввода
});

// querySelector() - находит первый элемент на странице, соответствующий CSS-селектору
// addEventListener() - назначает функцию-обработчик для указанного события на элементе
// 'click' - событие, возникающее при клике мышью по элементу
// .value - свойство, которое содержит текущее значение элемента формы (input, select, textarea)
// .textContent - свойство, которое содержит текстовое содержимое элемента (без HTML-тегов)
```

Вариант 2.

```javascript
'use strict';

function changeClick() {
    const input = document.querySelector('.input').value;
    const panelText = document.querySelector('.panel')
    panelText.textContent = input;
    document.querySelector('.input').value = '';
}
```

В файле index.html заменить переписать `<button class="button">Change</button>`:

```html
<button class="button" onclick="changeClick()">Change</button>
```

---

### Обработка событий клавиатуры

```html
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>app.js</title>
    <script src="./app.js" defer></script>  <!-- Скрипт выполнится после парсинга HTML -->
</head>
<body style="text-align: center;">
    <div class="panel">JavaScript</div>
    <input class="input">
    <button class="button">Change</button>
</body>
</html>
```

```javascript
'use strict';

function changeClick() {
    const input = document.querySelector('.input').value;
    const panelText = document.querySelector('.panel')
    panelText.textContent = input;
    document.querySelector('.input').value = '';
}

// Обработка кнопки <button class="button">Change</button>
document.querySelector('.button').addEventListener('click', changeClick);  // changeClick - без скобок (ожидает события)

// Обработка нажатия кнопки 'Enter' на клавиатуре
document.querySelector('.input').addEventListener('keydown', (e) => {
    if (e.code === 'Enter') {
        changeClick();
    }
});

// 'keydown' - событие, возникающее при нажатии клавиши на клавиатуре
// e (event) - объект события, содержащий информацию о произошедшем событии (какая клавиша, координаты и т.д.)
// e.code - свойство, содержащее физический код клавиши (например 'Enter', 'KeyA', 'Digit1')
```

---

### Работа со стилями и классами

```html
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>app.js</title>
    <link rel="stylesheet" href="./styles.css">
    <script src="./app.js" defer></script>  <!-- Скрипт выполнится после парсинга HTML -->
</head>
<body style="text-align: center;">
    <div class="panel">JavaScript</div>
    <input class="input">
    <button class="button">Change</button>
    <div class="notfication">Changed!</div>
</body>
</html> 
```

Вариант 1 (прямое изменение style).

```css
body {  /* Стили для всей страницы */
    font-family: Arial, sans-serif;  /* Шрифт текста */
    background-color: #f5f5f5;     /* Светло-серый фон страницы */
    margin: 50px 0;                  /* Отступ сверху/снизу 50px, по бокам 0 */
}

.panel {  /* Блок с текстом (зеленая панель) */
    background-color: #4CAF50;  /* Зеленый фон */
    color: white;               /* Белый текст */
    padding: 20px;                /* Внутренние отступы со всех сторон */
    margin: 20px auto;            /* Внешние отступы: 20px сверху/снизу, auto по бокам (центрирует) */
    width: 380px;                 /* Ширина блока */
    border-radius: 8px;           /* Скругленные углы */
    font-size: 18px;              /* Размер шрифта */
    box-shadow: 0 2px 5px rgba(0,0,0,0.2);  /* Тень: сдвиг, размытие, прозрачность */
}

.input {  /* Поле ввода */
    width: 270px;                   /* Ширина поля */
    padding: 12px;                  /* Внутренние отступы (делает поле выше) */
    margin: 10px;                   /* Внешние отступы со всех сторон */
    border: 2px solid #ddd;       /* Серая рамка толщиной 2px */
    border-radius: 5px;             /* Скругленные углы */
    font-size: 16px;                /* Размер шрифта */
    transition: border-color 0.3s;  /* Плавное изменение цвета рамки (0.3 секунды) */
}

.input:focus {  /* Состояние поля ввода когда оно в фокусе (кликнули) */
    outline: none;            /* Убирает стандартную обводку браузера */
    border-color: #4CAF50;  /* Рамка становится зеленой */
}

.button {  /* Кнопка */
    background-color: #4CAF50;  /* Зеленый фон */
    color: white;               /* Белый текст */
    padding: 12px 30px;           /* Отступы: 12px сверху/снизу, 30px слева/справа */
    border: none;                 /* Убирает рамку */
    border-radius: 5px;           /* Скругленные углы */
    font-size: 16px;              /* Размер шрифта */
    cursor: pointer;              /* Курсор в виде руки при наведении */
    transition: background-color 0.3s;  /* Плавное изменение цвета фона */
}

.button:hover {  /* Состояние кнопки при наведении мыши */
    background-color: #45a049;   /* Чуть темнее зеленый */
}

.button:active {  /* Состояние кнопки в момент нажатия */
    transform: translateY(1px);  /* Сдвиг вниз на 1px (эффект нажатия) */
}

.notfication {
    font-size: 14px;
    margin: 10px auto;
    display: none;  /* По умолчанию элемент скрыт */
}

/*
.panel, .input, .button - классы (стили для элементов с этими классами)
:focus - псевдокласс (стиль когда элемент в фокусе)
:hover - псевдокласс (стиль при наведении мыши)
:active - псевдокласс (стиль в момент нажатия)
*/
```

```javascript
'use strict';

function changeClick() {
    const input = document.querySelector('.input').value;
    const panelText = document.querySelector('.panel')
    panelText.textContent = input;
    document.querySelector('.notfication').style.display = 'block';  // Меняем display: none; на display: block;
    document.querySelector('.input').value = '';
}

// Обработка кнопки <button class="button">Change</button>
document.querySelector('.button').addEventListener('click', changeClick);
```

Вариант 2 (работа с классами) - Рекомендуется!

В styles.css добавить блок:

```css
.notfication_active {
    display: block;
}
```

```javascript
'use strict';
'use strict';

function changeClick() {
    const input = document.querySelector('.input').value;
    const panelText = document.querySelector('.panel')
    panelText.textContent = input;
    document.querySelector('.notfication').classList.add('notfication_active');
    document.querySelector('.input').value = '';
}

// classList - свойство, которое позволяет работать с классами элемента (добавлять, удалять, проверять наличие)
// .add('класс') - добавляет класс элементу
// .remove('класс') - удаляет класс у элемента
// .toggle('класс') - переключает класс (добавляет если нет, удаляет если есть)
// .contains('класс') - проверяет, есть ли класс у элемента (возвращает true/false)

// Обработка кнопки <button class="button">Change</button>
document.querySelector('.button').addEventListener('click', changeClick);
```

---

### Установка атрибутов

* **getAttribute** - получает значение атрибута
* **setAttribute** - устанавливает значение атрибута

```html
<input class="input">
<button class="button">Change</button>
```

```javascript
// ПОЛУЧЕНИЕ (getAttribute)
const button = document.querySelector('.button');
const buttonClass = button.getAttribute('class'); // получили class="button"
console.log('Класс кнопки:', buttonClass);        // Класс кнопки: button

// УСТАНОВКА (setAttribute)
const input = document.querySelector('.input');
input.setAttribute('placeholder', 'Введите текст'); // добавляем атрибут placeholder

// Устанавливаем свои атрибуты
const panel = document.querySelector('.panel')
panel.setAttribute('data-key', 1);  // <div class="panel" data-key="1">JavaScript</div>
console.log(typeof panel.getAttribute('data-key'));  // string (атрибут всегда строка)
```

Для чего нужны свои атрибуты (data-*):

* **Хранение данных** - привязать id, цену, статус к элементу (data-user-id="123")
* **Состояние UI** - открыт/закрыт модалки, активный таб (data-open="true")
* **CSS-стилизация** - менять стили через атрибут (data-theme="dark", data-status="error")
* **Доступность (ARIA)** - для скринридеров (aria-label, aria-expanded)
* **Тестирование** - data-testid для автотестов (не меняются при рефакторинге)
* **Фреймворки** - внутренняя идентификация компонентов (React, Vue)

```html
<div class="one">A</div>
<div id="two">B</div>
<div data-myKey="3">C</div>
```

```javascript
const a = document.querySelector('.one');  // Точка (.) - ищет по классу
console.log(a.textContent);  // A
const b = document.querySelector('#two');  // Решетка (#) - ищет по id
console.log(b.textContent);  // B
const c = document.querySelector('[data-myKey="3"]');  // Квадратные скобки ([]) - ищут по любому атрибуту
console.log(c.textContent);  // C
console.log(document.querySelector('[id="two"]').textContent);     // B
console.log(document.querySelector('[class="one"]').textContent);  // A
```

**querySelectorAll()** - ищет все элементы, подходящие под селектор, и возвращает список

```html
<div class="one">A</div>
<div class="one">B</div>
```

```javascript
const a = document.querySelectorAll('.one');
console.log(a[0].textContent);  // A
console.log(a[1].textContent);  // B
```

**getElementById()** - ищет элемент по id и возвращает его. (Рекомендуется! Для поиска по ID)

```html
<div id="one">A</div>
```

```javascript
console.log(document.getElementById('one').textContent);  // A
```

---
