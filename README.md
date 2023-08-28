# Kittygram
## __Описание__
Kittygram - социальная сеть для обмена фотографиями любимых питомцев.

Хозяева могут добавлять, обновлять и удалять информацию о своих котиках.

Смотреть информацию о котиках и управлять карточками собственных котиков могут только авторизованные пользователи.

## __Возможности Kittygram__
* Регистрация и авторизация пользователя.
* Создание/обновление/удаление карточки питомца: загрузка фотографии (в формате JPG), указание имени кота, цвета, года рождения, а также достижения питомца.
* Просмотр карточек чужих питомцев.

## __Установка на локальном компьютере__
1. Клонируйте репозиторий
```
> git clone https://github.com/Lozhkin-pa/kittygram_final.git
```
2. Установите и активируйте виртуальное окружение
```
> python -m venv venv
> source venv/Scripts/activate  - для Windows
> source venv/bin/activate - для Linux
```
3. Установите зависимости
```
> python -m pip install --upgrade pip
> pip install -r requirements.txt
```
4. Перейдите в папку backend и выполните миграции
```
> cd backend
> python manage.py migrate
```
5. Создайте суперпользователя
```
> python manage.py createsuperuser
```
6. Запустите проект
```
> python manage.py runserver
```

## __Развертывание на удаленном сервере__
1. Создайте папку проекта в домашней директории сервера и перейдите в нее
```
> mkdir kittygram
> cd kittygram
```
2. Скопируйте на сервер в папку проекта файл docker-compose.production.yml
3. Скачайте с Docker Hub на сервер образы для контейнеров
```
> sudo docker compose -f docker-compose.production.yml pull
```
4. Запустите контейнеры в режиме демона
```
> sudo docker compose -f docker-compose.production.yml up -d
```
5. Выполните команды для миграций и сборки статики
```
> sudo docker compose -f docker-compose.production.yml exec backend python manage.py migrate
> sudo docker compose -f docker-compose.production.yml exec backend python manage.py collectstatic
> sudo docker compose -f docker-compose.production.yml exec backend cp -r /app/collect_static/. /static_backend/static/
```
6. Создайте суперпользователя
```
> sudo docker compose -f docker-compose.production.yml exec backend python manage.py createsuperuser
```

## __Примеры запросов__
```
> GET kittygram-yap.hopto.org/api/cats/ - получение всех карточек питомцев:

{
    "count": 3,
    "next": null,
    "previous": null,
    "results": [
        {
            "id": 1,
            "name": "Barsik",
            "color": "white",
            "birth_year": 2020,
            "achievements": [],
            "owner": 2,
            "age": 3,
            "image": "http://127.0.0.1:8080/media/cats/images/temp.jpeg",
            "image_url": "/media/cats/images/temp.jpeg"
        },
        {
            "id": 2,
            "name": "Vasya",
            "color": "black",
            "birth_year": 2015,
            "achievements": [],
            "owner": 2,
            "age": 8,
            "image": "http://127.0.0.1:8080/media/cats/images/temp_qlVmcOv.jpeg",
            "image_url": "/media/cats/images/temp_qlVmcOv.jpeg"
        },
        {
            "id": 3,
            "name": "Pushok",
            "color": "white",
            "birth_year": 2018,
            "achievements": [],
            "owner": 2,
            "age": 5,
            "image": "http://127.0.0.1:8080/media/cats/images/temp_soZ2B1D.jpeg",
            "image_url": "/media/cats/images/temp_soZ2B1D.jpeg"
        }
    ]
}
```
```
> GET kittygram-yap.hopto.org/api/cats/1/ - получение конкретной карточки питомца:

{
    "id": 1,
    "name": "Barsik",
    "color": "white",
    "birth_year": 2020,
    "achievements": [],
    "owner": 2,
    "age": 3,
    "image": "http://127.0.0.1:8080/media/cats/images/temp.jpeg",
    "image_url": "/media/cats/images/temp.jpeg"
}
```

## __Технологии__
* [Django 3.2.3](https://docs.djangoproject.com/en/4.2/)
* [Django Rest Framework  3.12.4](https://www.django-rest-framework.org/)
* [Djoser 2.1.0](https://djoser.readthedocs.io/en/latest/getting_started.html)
* [Pillow 9.0.0](https://pypi.org/project/Pillow/9.0.0/)
* [python-dotenv 1.0.0](https://pypi.org/project/python-dotenv/)
* [Gunicorn 20.1.0](https://gunicorn.org/#docs)

## __Авторы__
* [Павел Ложкин](https://github.com/Lozhkin-pa)