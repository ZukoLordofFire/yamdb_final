<h2>YAMDb API</h2>

![API logo](https://i.imgur.com/YamDB.jpg)
<h3>Сервис с рецензиями на произведения</h3>

## Возможности
- Оставляй рецензии на произведения разных категорий и жанров - кино, книги, музыку etc.
- Ставь оценку работам
- Коментируй рецензии других пользователей

## Технологии
[![My Skills](https://skillicons.dev/icons?i=python,django,sqlite,bootstrap&theme=light)](https://skillicons.dev)

![Workflow](https://github.com/zukolordoffire/yamdb_final/actions/workflows/main.yml/badge.svg)

## Наполнение env файла
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres

### Здесь Вам надо указать свой пароль ###
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432

## Запуск проекта в контейнере:
Клонировать образ с DockerHub:
docker pull api_yamdb

Сборка контейнера и его запуск:
docker-compose up -d --build

Выполнение миграций:
docker-compose exec web python manage.py migrate 

Создание суперпользователя:
docker-compose exec web python manage.py createsuperuser

Загрузка статики:
docker-compose exec web python manage.py collectstatic --no-input

## Остановка контейнера:
docker-compose down -v

### Документация:
После запуска на localhost доступна [документация].

## Примеры:

### Регистрация:
* POST: http://127.0.0.1:8000/api/v1/auth/signup/ 
```
{
    "email": "string",
    "username": "string"
}
```
RESPONSE:
```
{
    "email": "string",
    "username": "string"
}
```
На почту придёт код подтвержения.

### Получение токена по коду из письма: 
* POST: http://127.0.0.1:8000/api/v1/auth/token/ 
```
{
    "username": "string",
    "confirmation_code": "string"
}
```
RESPONSE:
```
{
    "token": "string"
}
```

Для добавления/изменения данных через API необходимо добавить в header 
к запросу параметр 'Authorization' со значением 'Bearer TOKEN'.

### Получение произведений (постранично): 
* GET: http://127.0.0.1:8000/api/v1/titles/

RESPONSE:
```
{
  "count": 123,
  "next": "http://example.org/api/v1/titles/?limit=10&offset=10",
  "previous": null,,
  "results": [
    {
        "id": 1,
        "name": "Побег из Шоушенка",
        "year": 1994,
        "rating": 10,
        "description": null,
        "genre": [
            {
                "name": "Драма",
                "slug": "drama"
            }
        ],
        "category": {
            "name": "Фильм",
            "slug": "movie"
        }
    },
    ...
  ]
}
```

### Получение рецензий на произведение по id = title_id (постранично): 
* GET: http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/

RESPONSE:
```
{
    "count": 2,
    "next": null,
    "previous": null,
    "results": [
        {
            "id": 2,
            "text": "Не привыкай\n«Эти стены имеют одно свойство: сначала ты их ненавидишь, потом привыкаешь, а потом не можешь без них жить»",
            "author": "capt_obvious",
            "score": 10,
            "pub_date": "2022-08-12T12:26:24.656621Z"
        },
        ...
    ]
}
```


### Авторы

Валентин Веселов [Telegram](https://t.me/bothat) [GitHub](https://github.com/ZukoLordofFire)

[документация]: <http://127.0.0.1:8000/redoc/>
