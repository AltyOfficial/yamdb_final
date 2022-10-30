# API для проекта Yamdb ![Workflow Badge](https://github.com/Arkellain/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

## Проект расположен по адресу http://178.154.221.106/

Проект позволяет обращаться к базе данных и получать данные в формате JSON

## Следует создать и заполнить файл .env, находящийся в директории "/infra/"
#### Шаблон наполнения env-файла (кавычки убрать)
```sh
DB_ENGINE='DB_ENGINE'
DB_NAME='DB_NAME'
POSTGRES_USER='USER'
POSTGRES_PASSWORD='PASSWORD'
DB_HOST='HOST'
DB_PORT='PORT'
```

## Команды для запуска приложений в контейнерах
#### Клонировать проект 
```sh
git clone https://github.com/Arkellain/infra_sp2.git
```
#### Выполнить команды для запуска контейнеров
```sh
cd /infra/
docker-compose up -d
```
- Команда ```-d``` нужна для фоновой работы контейнера
#### После запуска контейнеров выполнить команды миграции, создания суперпользователя и собирания статики
```sh
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py createsuperuser
docker-compose exec web python manage.py collectstatic --no-input 
```

## Заполнение базы данных
#### Готовая база данных "fixtures.json"находится в директории "/infra/"
#### Перенести файл с базой данных в контейнер
```sh
docker cp fixtures.json infra_web:/app/fixtures.json
```
#### Заполнить базу данных новым файлом
```sh
docker-compose exec web python manage.py loaddata fixtures.json
```