## CI и CD проекта API_YAMDB

![example workflow](https://github.com/dk-r3d3/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

# В данном проекте реализованы:

- автоматический запуск тестов;
- обновление образов на Docker Hub;
- автоматический деплой на боевой сервер при пуше в главную ветку main;
- оповещение в Telegram об ошибках в процессе работы алгоритма действий или об успешном деплое.

Подготовка для запуска workflow

Создайте и активируйте виртуальное окружение:

```
python -m venv venv
. venv/Scripts/activate
```

Запустите автотесты:

```
pytest
```

Отредактируйте файл nginx/default.conf и в строке server_name впишите IP виртуальной машины (сервера).
Скопируйте подготовленные файлы docker-compose.yaml и nginx/default.conf из вашего проекта на сервер:

```
scp [файл, который хотите скопировать] [name@public_id:/путь к файлу на сервере/]
```

Зайдите в репозиторий на локальной машине и отправьте файлы на сервер.


В репозитории GitHub добавьте данные в `Actions secrets`:

```
DOCKER_USERNAME - имя пользователя в DockerHub
DOCKER_PASSWORD - пароль пользователя в DockerHub
HOST - ip-адрес сервера
USER - пользователь
SSH_KEY - приватный ssh-ключ (публичный должен быть на сервере)
PASSPHRASE - кодовая фраза для ssh-ключа
DB_ENGINE - django.db.backends.postgresql
DB_HOST - db
DB_PORT - 5432
SECRET_KEY - секретный ключ приложения django (необходимо чтобы были экранированы или отсутствовали скобки)
ALLOWED_HOSTS - список разрешённых адресов
TELEGRAM_TO - id своего телеграм-аккаунта (можно узнать у @userinfobot, команда /start)
TELEGRAM_TOKEN - токен бота (получить токен можно у @BotFather, /token, имя бота)
DB_NAME - postgres (по умолчанию)
POSTGRES_USER - postgres (по умолчанию)
POSTGRES_PASSWORD - postgres (по умолчанию)
```
