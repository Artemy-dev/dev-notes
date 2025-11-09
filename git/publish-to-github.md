# Полная инструкция: как опубликовать проект на GitHub

## Подготовь структуру проекта

```text
project/ 
├── venv/ 
├── .gitignore 
├── main.py 
├── README.md 
└── requirements.txt 
```

## Создай `.gitignore` (это говорит, что не нужно отслеживать)

В корне проекта создай файл **.gitignore** и добавь туда:

```text
# Игнорировать виртуальное окружение
venv/

# Кеш и временные файлы
__pycache__/
*.pyc
*.pyo
*.log
*.tmp

# IDE-шные файлы
.vscode/
.idea/

# Операционная система
.DS_Store
```

## Инициализируй Git (терминал)

```bash
cd путь/до/проекта

git init
```

## Добавь файлы и сделай первый коммит

```bash
git add .

git commit -m "Initial commit"
```

## Создай репозиторий на GitHub

* Перейди на [GitHub](https://github.com)
* Нажми **New repository**
* Введи название, например: **my-repository**
* Нажми **Create repository**

## Свяжи локальный проект с GitHub

```bash
git remote add origin https://github.com/ЛОГИН/ИМЯ_РЕПОЗИТОРИЯ.git
```

## Сгенерируй персональный токен (PAT)

1. Перейди по ссылке: [GitHub Tokens](https://github.com/settings/tokens)
2. Нажми **Generate new token (classic)**
3. Укажи:
   * **Note:** Git from terminal
   * **Expiration:** No expiration (или выбери срок)
4. Отметь галочку:
   * **repo** — доступ к репозиториям
5. Нажми **Generate token**

*Скопируй токен сразу - он будет виден только один раз!*

## Запушь проект на GitHub

```bash
git branch -M master
git push -u origin master
```

Когда спросят логин/пароль:

* Введи логин
* В поле пароля вставь токен, а не обычный пароль

## Дополнительно

### Обновить проект

```bash
git add .
git commit -m "Описание изменений"
git push
```

### Посмотреть статус

```bash
git status
```
