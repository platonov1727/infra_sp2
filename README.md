# Проект студентов Яндекс.Практикум АПИ Yandex Movie Data Base(YaMDB)

## Описание

Сервис Апи для того, чтобы собирать пользовательские оценки и комментарии на произведения различных категорий и жанров.

#### Подробная документация по адресу YOURHOST/redoc/

В redoc описанны все ендпоинты и их возможности с примерами запросов. И ожидаемые ответы.

#### Возможности

- JWT Аутентификация
- возможность ознакомиться с отзывами без аутентификации(но нельзя оставить отзыв и поставить оценку)
- Получение списка всех категорий и жанров, добавление и удаление.
- Пользователи могут самостоятельно зарегистрироваться через идентификацию по email
- Есть возможность назначить администратора, модератора

#### Технологии

- Django==3.2
- django-filter==22.1
- django-import-export==3.0.2
- djangorestframework==3.12.4
- djangorestframework-simplejwt==5.2.2
- PyJWT==2.1.0

со списком всех используемых библиотек можно ознакомиться в файлe requirements.txt

#### Запуск проекта в dev-режиме

```git clone <название репозитория>
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python manage.py migrate
Load test data in django admin panel
python manage.py runserver```

#### Авторы

https://github.com/Shabanov010
https://github.com/platonov1727
https://github.com/mariarozhina
```

### Пример заполнения файла .env

```sh
DB_ENGINE=django.db.backends.postgresql # указываем, что работаем с postgresql
DB_NAME=postgres # имя базы данных\n
POSTGRES_USER=postgres # логин для подключения к базе данных\n
POSTGRES_PASSWORD=postgres # пароль для подключения к БД (установите свой)\n
DB_HOST=db # название сервиса (контейнера)\n
DB_PORT=5432 # порт для подключения к БД\n
```

### Запуск контейнеров

cd infra #перейти в папку с файлом docker-compose.yaml
docker-compose up -d # -d запускает в фоновом режиме # Запустить сборку контейнеров
docker-compose exec web python manage.py migrate # выполнить миграции
docker-compose exec web python manage.py createsuperuser # Создать супер-юзера
docker-compose exec web python manage.py collectstatic --no-input # Собрать статику
http://localhost/admin # Проверить работу

docker-compose down # Остановить работу контейнеров

### Заполнить базу данных

### Заполнить базу данных готовой

```bash
# Закинуть dump.json на сервер через scp и выполнить там

python3 manage.py shell  
# выполнить в открывшемся терминале:
>>> from django.contrib.contenttypes.models import ContentType
>>> ContentType.objects.all().delete()
>>> quit()

python manage.py loaddata dump.json
```

### **Резервное копирование базы данных (бэкапы)**

```bash
sudo -u postgres pg_dump yatube > yatube_backup.dump # Эта команда создаст файл («дамп базы») yatube_backup.dump с бэкапом данных из БД yatube.
sudo -u postgres psql -c 'create database yatube2;' # Создали пустую базу данных с именем yatube2
sudo -u postgres psql -d yatube2 -f yatube_backup.dump # Загрузили в неё данные из дампа
```
