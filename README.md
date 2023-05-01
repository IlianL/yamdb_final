# YaMDb собирает отзывы пользователей на произведения.
![workflow](https://github.com/IlianL/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

## Tech stack:
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)  

![Django](https://img.shields.io/badge/django-%23092E20.svg?style=for-the-badge&logo=django&logoColor=white)
![DjangoREST](https://img.shields.io/badge/DJANGO-REST-ff1709?style=for-the-badge&logo=django&logoColor=white&color=ff1709&labelColor=gray)
![JWT](https://img.shields.io/badge/JWT-black?style=for-the-badge&logo=JSON%20web%20tokens)
![Postgres](https://img.shields.io/badge/postgres-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white)  

![Nginx](https://img.shields.io/badge/nginx-%23009639.svg?style=for-the-badge&logo=nginx&logoColor=white)
![Gunicorn](https://img.shields.io/badge/gunicorn-%298729.svg?style=for-the-badge&logo=gunicorn&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)  

![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)  

![Yandex.cloud](https://img.shields.io/badge/-yandex.clound-blue?style=for-the-badge&logo=appveyor)  
 

 
## Описание:
Проект YaMDb собирает отзывы пользователей на произведения. Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.
Произведения делятся на категории, такие как «Книги», «Фильмы», «Музыка». Например, в категории «Книги» могут быть произведения «Винни-Пух и все-все-все» и «Марсианские хроники», а в категории «Музыка» — песня «Давеча» группы «Жуки» и вторая сюита Баха. Список категорий может быть расширен (например, можно добавить категорию «Изобразительное искусство» или «Ювелирка»).

Произведению может быть присвоен жанр из списка предустановленных (например, «Сказка», «Рок» или «Артхаус»).

Добавлять произведения, категории и жанры может только администратор.

Благодарные или возмущённые пользователи оставляют к произведениям текстовые отзывы и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — рейтинг (целое число). На одно произведение пользователь может оставить только один отзыв.
Пользователи могут оставлять комментарии к отзывам.

Добавлять отзывы, комментарии и ставить оценки могут только аутентифицированные пользователи.


## Регистрация пользователей:
1. Пользователь отправляет POST-запрос с параметрами username и email на эндпоинт /api/v1/auth/signup/.
2. YaMDB отправляет письмо с кодом подтверждения (confirmation_code) на указанный email адрес.
3. Пользователь отправляет POST-запрос с параметрами email и confirmation_code на эндпоинт /api/v1/auth/token/,
после чего польватель получает JWT token. Для авторизации вы должны передавать ключ в заголовке: \
key - "Authorization", value "Bearer и ваше значение token" 

### Пользователя может создавать администратор.
1. Администратор отправляет POST-запрос с параметрами username и email на эндпоинт /api/v1/users/. \
При создании пользователя не предполагается автоматическая отправка письма пользователю с кодом подтверждения.
2. После этого пользователь должен самостоятельно отправить свой email и username на эндпоинт /api/v1/auth/signup/.
3. YaMDB отправляет письмо с кодом подтверждения (confirmation_code) на указанный email адрес.
4. Далее пользователь отправляет POST-запрос с параметрами username и confirmation_code на эндпоинт /api/v1/auth/token/, в ответе на запрос ему приходит JWT-токен, как и при самостоятельной регистрации.


## Пользовательские роли и права доступа.
- Аноним — может просматривать описания произведений, читать отзывы и комментарии.
- Аутентифицированный пользователь (user) — может читать всё, как и Аноним, может публиковать отзывы и ставить оценки произведениям (фильмам/книгам/песенкам), может комментировать отзывы; может редактировать и удалять свои отзывы и комментарии, редактировать свои оценки произведений. Эта роль присваивается по умолчанию каждому новому пользователю.
- Модератор (moderator) — те же права, что и у Аутентифицированного пользователя, плюс право удалять и редактировать любые отзывы и комментарии.
- Администратор (admin) — полные права на управление всем контентом проекта. Может создавать и удалять произведения, категории и жанры. Может назначать роли пользователям.
- Суперюзер Django обладает правами администратора, пользователя с правами admin. 

## Ресурсы API YaMDb
* Ресурс auth: аутентификация.
* Ресурс users: пользователи.
* Ресурс titles: произведения, к которым пишут отзывы (определённый фильм, книга или песенка).
* Ресурс categories: категории (типы) произведений («Фильмы», «Книги», «Музыка»). Одно произведение может быть привязано только к одной категории.
* Ресурс genres: жанры произведений.
* Ресурс reviews: отзывы на произведения.
* Ресурс comments: комментарии к отзывам.
 
 ## Подготовка и запуск проекта на сервере.
 
 Скачайте проект
 ```
 # Нам нужна только папка infra
 git@github.com:IlianL/yamdb_final.git
 ```
Подключитесь к своему серверу
```
ssh your_login@your_ip
```
Обновляем список пакетов и обновляем сами пакеты.
```
sudo apt update
sudo apt upgrade -y 
```
Устанавливаем докер и докер компоуз.
```
sudo apt install docker.io
sudo apt install docker-compose
# Если у вас не ubuntu, воспользуйтесь этой инструкцией для установки docker-compose:
# https://docs.docker.com/compose/install/
```
Проверяем успешность установки.
```
docker --version
docker-compose --version
```
Создайте на сервере директорию для проекта.
```
mkdir yamdb && cd yamdb/
```
Создайте и заполните .env файл по примеру.
```
nano .env
DB_ENGINE=django.db.backends.postgresql # указываем, что работаем с postgresql
DB_NAME=postgres # имя базы данных
POSTGRES_USER=example_login # логин для подключения к базе данных
POSTGRES_PASSWORD=example_pwd # пароль для подключения к БД
DB_HOST=db # название сервиса (контейнера)
DB_PORT=5432 # порт для подключения к БД 
```
Отредактируйте файл infra/nginx/default.conf.
```
# Замените этот адрес на адрес вашего сервера.
server_name 127.0.0.1;
```
Скопируйте файлы из папки infra на ваш сервер.
```
# В момент выполнения команды нужно находиться на уровень выше папки infra
scp -r infra/*  <username>@<server IP>:/home/<server user>/yamdb/
```
Запустите контейнеры.
```
sudo docker-compose up -d
# Сайт запущен и доступен по адресу:  http://[ваш сервер]/api/v1/.
```
После успешной сборки выполнить эти команды:
```
# Делаем миграции.
sudo docker-compose exec -T web python manage.py makemigrations
sudo docker-compose exec -T web python manage.py migrate
# Собирем статику.
sudo docker-compose exec -T web python manage.py collectstatic --no-input
# Создаём администратора.
sudo docker-compose exec web python manage.py createsuperuser
```
Остановка и повторный запуск проекта.
```
# Отсанавлием контейнеры без удаления.
sudo docker-compose stop
# Запускаем остановленные контейнеры.
sudo docker-compose start
# Останавливаем и удаляем контейнеры, ключ -v удаляет тома.
sudo docker-compose down -v
```


## Документация API YaMDb
 
Документация доступна по эндпойнту: http://[ваш сервер]/redoc/

## Авторы:
- [Илиан Ляпота Тимлид, Python-разработчик](https://github.com/IlianL)
- [Юлия Доманова Python-разработчик](https://github.com/StrekozJulia)
- [Александр Рассыхаев Python-разработчик](https://github.com/Leenominai)
