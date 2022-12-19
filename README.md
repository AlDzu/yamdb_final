
# Проект YamDB  
![badge](https://github.com/aldzu/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)
  
Проект позволяет собирать отзывы о различных произведениях (фильмы, книги, музыки)  
  
## Описание проекта  
  
Проект аккумулирует отзывы пользователей о произведениях.  
Произведения в свою очередь делятся на категории, жанры.  
У пользователей есть разные уровни доступа:  
администратор, модератор, аутентифицированный пользователь, посетитель.

Проект доступен по адресу: http://158.160.4.80/
Доступ к панели администратора: http://158.160.4.80/admin/
redoc: 1http://58.160.4.80/redoc/

### Регистрация пользователя  
- Пользователь отправляет запрос с параметрами email и username на **/auth/email/**.  
- YaMDB отправляет письмо с кодом подтверждения (confirmation_code) на адрес email . 
- Пользователь отправляет запрос с параметрами email и confirmation_code на **/auth/token/**, в ответе на запрос ему приходит token (JWT-токен).  

### Отзывы и комментарии к ним 
Через эндпоинт **/api/v1/titles/{title_id}/reviews/**
Зарегистрированные пользователи могут оставить к произведениям отзывы с оценкой в диапазоне от одного до десяти. На одно произведение пользователь может оставить только один отзыв. С помощью пользовательских оценок формируется усреднённая оценка произведения. Читать отзывы могут все посетители. 

Через эндпоинт **/api/v1/titles/{title_id}/reviews/{review_id}/comments/**
Зарегистрированные пользователи на отзывы могут оставлять комментарии. Читать комментарии могут все посетители.
 

## Технологии  
  
- проект написан Python с помощью фреймворка Django REST Framework  
- аутентификация реализована с помощью Simple JWT.  

## Запуск проекта

https://github.com/AlDzu/yamdb_final
https://hub.docker.com/r/aldzu/yamdb

◾ Клонируйте репозиторий и перейти в него

◾ Создайте в директории infra_sp2\infra .env файл с параметрами:

ALLOWED_HOSTS=*  # Разрешенные хосты
SECRET_KEY=NewKey123  # Секретный ключ
DB_ENGINE=django.db.backends.postgresql  # указываем, что работаем с postgresql
DB_NAME=postgres  # имя базы данных
POSTGRES_USER=postgres  # логин для подключения к базе данных
POSTGRES_PASSWORD=postgres  # пароль для подключения к БД (установите свой)
DB_HOST=db  # название сервиса (контейнера)
DB_PORT=5432   # порт для подключения к БД

## Запуск ерез виртуальное окружение:
◾ Установите и активируйте виртуальное окружение

◾ Установите зависимости из файла requirements.txt :
```
pip install -r requirements.txt
```
◾ В папке с файлом manage.py выполните миграции:
```
python manage.py migrate
```
◾ Запустите проект:
```
python manage.py runserver
```
## Запуск через Doker:

Установите и настройте [Doker](https://www.docker.com/products/docker-desktop/).

◾ Запустите docker-compose:
```
docker-compose up -d --build
```
◾ Выполните миграции создав предварительно модели пользователей, создайте суперпользователя и соберите файлы статики командами:
```
docker-compose exec web python manage.py makemigrations reviews users
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py createsuperuser
docker-compose exec web python manage.py collectstatic --no-input
```
◾ Остановить проект возможно командой:
```
docker-compose down -v
```

## Автор
Проект выполнен в рамках командной работы на Яндекс Практикум.

- **[Александр Дзюба](https://github.com/AlDzu)**
