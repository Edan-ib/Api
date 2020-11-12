# Технология разработки программного обеспечения 
# Лабораторная работа №1: создание микросервиса на Spring Boot с базой данных
# Ходырева Ирина Альбертовна, группа 3mac2001
# Цель лабораторной работы: 
Знакомство с проектированием многослойной архитектуры Web-API (веб-приложений, микро-сервисов). 

Это веб-приложение, которое обращается к базе данных книг (База данных postgres). В ней реализованы ендпоинты, которые позволяют выполнять CRUD-запросы.
________________________________________________________________________________________________________________________________________________________
Необходимо заранее подготовить Базу Данных и Docker:

- Скачать Docker Desktop и установить (Docker версии 18 и выше; docker compose 1.24 и выше, curl, свободный порт);

- Установить и запустить postgrsql в Docker, в терминале Docker: docker run -e POSTGRES_PASSWORD=root -p 5432:5432 postgres (где соотвественно user=postgres password=root);

- В файле ./src/main/resources/application.properties указать имя пользователя для доступа к базе данных: spring.datasource.username = postgres и в spring.datasource.password = root (пароль для доступа к базе);

- В параметре spring.datasource.url = <указать адрес для доступа к базе данных> :
Для базы данных запущенной на локальном машине: jdbc:postgresql://localhost:5432/postgresql;
Для базы данных запущенной в docker на локальной машине: jdbc:postgresql://172.17.0.1:5432/postgresql;
Для того чтобы узнать IP виртуальной машины Docker, в терминале Docker: docker-machine ip default;

- Настройка самой базы данных осуществляется с помощью ./src/main/resources/schema.sql. Выполнить команду: psql -h <адрес_БД> -p <порт_БД> -U <имя_пользователя> -d public -f "schema.sql";

- Данные для базы данных находятся в ./src/main/resources/data.sql. Выполнить команду: psql -h <адрес_БД> -p <порт_БД> -U <имя_пользователя> -d public -f "data.sql"

________________________________________________________________________________________________________________________________________________________
1) Клонирование репозитория.

- Для клонирования репозитория выполнить команду: git clone https://github.com/Edan-ib/simApi.git

- Либо скачать zip архив и распаковать его.

2) Cборка приложения в Maven.

Система сборки автоматическая.

- Выполнить команду из командной строки: mvn package -Dmaven.test.skip=true (с пропуском тестирования, команда выполняется в корневой директории);

- После выполнения команды в папке target будет готовой скомпилированный файл simapi-1.0.jar.

3) Сборка docker-образа.

- Выполнить команду в терминале IJ: docker build -t myapi:v1 (находясь в директории проекта с Dockerfile)

4) Запуск docker-контейнера из docker-образа с указанием мапинга портов.

- Выполнить команду в терминале: docker run -p 8080:8080 myapi:v1 (первым указывается порт локальной системы, вторым порт Docker)

5) Curl к ендпоинтам приложения.

- Получить список книг:

curl -X GET http://127.0.0.1:8080/api/v1/books [{
    "id": 1,
    "name": "Гарри Поттер и философский камень",
    "brand": "Джоан Роулинг",
    "price": 320,
    "quantity": 7
  },
  {
    "id": 2,
    "name": "Гарри Поттер и Тайная комната",
    "brand": "Джоан Роулинг",
    "price": 360,
    "quantity": 6
  },
  {
    "id": 3,
    "name": "Гарри Поттер и узник Азкабана",
    "brand": "Джоан Роулинг",
    "price": 400,
    "quantity": 2
  },
  {
    "id": 4,
    "name": "Гарри Поттер и Кубок огня",
    "brand": "Джоан Роулинг",
    "price": 350,
    "quantity": 4
  },
  {
    "id": 5,
    "name": "Гарри Поттер и Орден Феникса",
    "brand": "Джоан Роулинг",
    "price": 380,
    "quantity": 10
  }
]

- Получить соотвествующую запись по id:

curl -X GET http://127.0.0.1:8080/api/v1/book/{id} {
  "id": 1,
  "name": "Гарри Поттер и философский камень",
  "brand": "Джоан Роулинг",
  "price": 320,
  "quantity": 7
}

- Добавить запись:

curl -X POST http://127.0.0.1:8080/api/v1/books -d  {
  "id": 10,
  "name": "Новая книга",
  "brand": "Новый автор",
  "price": 100,
  "quantity": 7
} -H "Content-Type:application/json"

- Удалить запись:

curl -i -X DELETE http://127.0.0.1:8080/api/v1/books/del/{id} В ответе будет получен статус 204 No Content.

- Приложение возвращает значение hostname:

curl -X GET http://127.0.0.1:8080/api/v1/status ______{"hostname": "LAPTOP-3IRCU5BM"}



# Лабораторная работа №3: CI/CD и деплой приложения в Heroku
# Целью лабораторной работы: 
Знакомство с CI/CD и его реализацией на примере Travis CI и Heroku.
