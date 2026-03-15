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

Вариант 1.

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
