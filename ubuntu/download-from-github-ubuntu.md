# Как скачать файл с GitHub на Ubuntu сервер

## Способ 1. wget

*Подходит для скачивания одного файла из публичного репозитория.*

- Обновите пакеты и установите wget (если его нет)

```bash
sudo apt update
sudo apt install -y wget  
```

- Измените ссылку на файл (с github.com на raw.githubusercontent.com)

```txt
Замените:   https://github.com/username/test/main/main.py 
На:         https://raw.githubusercontent.com/username/test/main/main.py
```

- Скачайте файл командой wget

```bash
wget https://raw.githubusercontent.com/username/test/main/main.py
```

## Способ 2. git clone

*Подходит для скачивания всего репозитория, включая приватные.*

### Для публичных репозиториев (Public)

- Обновите пакеты и установите git (если его нет)

```bash
sudo apt update
sudo apt install -y git
```

- Клонируйте репозиторий

```bash
git clone https://github.com/username/test.git
```

### Для приватных репозиториев (Private)

*Требуется SSH-ключ или токен доступа.*

- Проверить существующие ключи (если есть, переходим к п.4):

```bash
cat ~/.ssh/id_rsa.pub
```

- Если ключа нет, создаем новый:

```bash
ssh-keygen
```

- Жмем Enter 3 раза, чтобы не ставить пароль.

- Проверить существующие ключи:

```bash
cat ~/.ssh/id_rsa.pub
```

- Перейдите в GitHub -> Se ngs -> SSH and GPG Keys -> New SSH Key

- Вставьте ключ и сохраните.

- Клонирование приватного репозитория:

```bash
git clone git@github.com:username/test.git
```
