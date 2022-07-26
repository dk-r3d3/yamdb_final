# CI и CD проекта API_YAMDB
[![Django-app workflow](https://github.com/dk-r3d3/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)](https://github.com/dk-r3d3/yamdb_final/actions/workflows/yamdb_workflow.yml)

### Проект на сервере/админка:
http://130.193.34.205/api/v1/

http://130.193.34.205/admin/login/?next=/admin/

### Документация API_YAMDB:
http://130.193.34.205/redoc/

### В данном проекте реализованы:

- автоматический запуск тестов;
- обновление образов на Docker Hub;
- автоматический деплой на боевой сервер при пуше в главную ветку main;
- оповещение в Telegram об ошибках в процессе работы алгоритма действий или об успешном деплое.

### Подготовка для запуска workflow

Создайте и активируйте виртуальное окружение:

```
python -m venv venv
. venv/Scripts/activate
```

Запустите автотесты:

```
pytest
```

Отредактируйте файл `nginx/default.conf` и в строке `server_name` впишите IP виртуальной машины (сервера).
Скопируйте подготовленные файлы `docker-compose.yaml` и `nginx/default.conf` из вашего проекта на сервер:

```
scp [файл, который хотите скопировать] [name@public_id:/путь к файлу на сервере/]
```

Зайдите в репозиторий на локальной машине и отправьте файлы на сервер.

В репозитории GitHub добавьте данные в `Actions secrets`:

```
DOCKER_USERNAME - имя пользователя в DockerHub
DOCKER_PASSWORD - пароль пользователя в DockerHub
HOST - ip-адрес сервера
USER - имя пользователя
SSH_KEY - приватный ssh-ключ
PASSPHRASE - кодовая фраза для ssh-ключа
DB_ENGINE - django.db.backends.postgresql
DB_HOST - db
DB_PORT - 5432
SECRET_KEY - ключ приложения django (`cat ~/.ssh/id_rsa`)
TELEGRAM_TO - id своего телеграм-аккаунта (можно узнать у @userinfobot)
TELEGRAM_TOKEN - токен бота (получить токен можно у @BotFather)
DB_NAME - postgres (по умолчанию)
POSTGRES_USER - postgres (по умолчанию)
POSTGRES_PASSWORD - postgres (по умолчанию)
```

## Запуск проекта на сервере:

Установите Docker:
```
sudo apt install docker.io
```
Установите Docker-compose(Инструкция для Ubuntu):

https://docs.docker.com/engine/install/ubuntu/

### Деплой проекта на сервер:
```
git add .
git commit -m "..."
git push
```
команда `git push` запустит блок команд yamdb_workflow.yaml

### После успешного деплоя:

Создайте суперпользователя:
```
docker-compose exec web python manage.py createsuperuser

```

### Работу с API осуществлять согласно документации:

http://130.193.34.205/redoc/

### Автор: 

Copyright © 2022 Dmitry Koroteev. All rights reserved.
