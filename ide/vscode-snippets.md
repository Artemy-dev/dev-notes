## Сниппеты (Snippets) в Visual Studio Code

**Сниппеты** - это шаблоны кода, которые позволяют быстро вставлять часто используемые конструкции (циклы, импорты, объявления функций) по короткому префиксу.

### Как создать свой сниппет

* Открыть **Command Palette** (`Ctrl+Shift+P` или `Cmd+Shift+P`).
* Набрать `Snippets: Configure Snippets`.
* Выбрать язык, для которого создается сниппет (например, `JavaScript`), либо `New Global Snippets file...` (если сниппет нужен для всех языков).

Глобальные сниппеты лежат в папке `%APPDATA%\Code\User\snippets\` (Windows) или `~/Library/Application Support/Code/User/snippets/` (macOS). Их можно синхронизировать через *GitHub Settings Sync*.

**Cинтаксис**

```json
"Имя сниппета": {
    "scope": "язык_1,язык_2,язык_3",
    "prefix": "короткое_слово_для_вызова",
    "body": ["строка_кода_1", "строка_кода_2"],
    "description": "Подсказка при вводе"
}
```

* **scope** (Необязательно) - Список языков через запятую, где работает сниппет. Если не указать, работает везде. 
* **prefix** - комбинация, после набора которой в редакторе появится предложение вставить сниппет.
* **body** - массив строк. Каждый элемент массива — это отдельная строка в итоговом коде. Используйте `\t` для табуляции внутри строки.

*Важно: В JSON объекты разделяются запятыми, но после последнего элемента запятая не ставится, иначе файл станет невалидным.*

Пример файла сниппетов для JS:

```json
{
  "Print to console": {
    "scope": "javascript,typescript,javascriptreact",
    "prefix": "cl",
    "body": ["console.log(${1});"],
    "description": "Log output to console"
  },
  "Print const": {
    "scope": "javascript,typescript,javascriptreact",
    "prefix": "c",
    "body": ["const ${1:variableName} = ${2:value};"],
    "description": "Declare a const variable"
  },
  "importCSSModule": {
    "prefix": "csm",
    "scope": "javascript,typescript,javascriptreact",
    "body": ["import styles from './${TM_FILENAME_BASE}.module.css';"],
    "description": "Import CSS Module as `styles`"
  },
  "Print function": {
    "scope": "javascript,typescript,javascriptreact",
    "prefix": "f",
    "body": ["function ${1:name}(${2:params}) {", "\t${3}", "}"],
    "description": "Insert a function declaration"
  }
}
```

* **${1}** - Позиция первого курсора после вставки. `console.log(${1});` → курсор сразу встает внутри скобок.
* **${2}** - Позиция, на которую перейдет курсор после нажатия Tab. `const ${1} = ${2};`
* **${1:default}** - Поле с плейсхолдером (текстом-заглушкой). `const ${1:name}` → при вставке слово `name` будет выделено, можно сразу печатать.
* **$TM_FILENAME_BASE** - Встроенная переменная **VS Code**. Имя текущего файла без расширения.
* **\t** - Символ табуляции (отступ). `"\t${3}"` → строка с отступом для тела функции.
