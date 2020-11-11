# Технология разработки программного обеспечения 
# Лабораторная работа №1: создание микросервиса на Spring Boot с базой данных
# Ходырева Ирина Альбертовна, группа 3mac2001
# Цель лабораторной работы: 
Знакомство с проектированием многослойной архитектуры Web-API (веб-приложений, микро-сервисов).

1) Клонирование репозитория.

- Для клонирования репозитория выполнить команду git clone https://github.com/git 

- Скачать zip архив и распаковать его.

2) Cборка приложения в Maven.
Система сборки автоматическая,

- Выполнить команду из командной строки mvn package -Dmaven.test.skip=true (с пропуском тестирования, команда выполняется в корневой директории);

- После выполнения команды появится папка target, в ней скомпилированный файл apilab-1.0.jar.

3) Сборка docker-образа.

- Выполнить команду: docker build -t apilab:v1 (находясь в директории проекта с Dockerfile)

4) Запуск docker-контейнера из docker-образа с указанием мапинга портов.

- Выполниить команду: docker run -p 8080:8080 apilab:v1 (первый это порт локальной системы, второй порт это Docker)

5) Curl к ендпоинтам приложения.

- Получить список книг:

curl -X GET http://127.0.0.1:8080/api/v1/books

- Получить соотвествующую запись по id:

curl -X GET http://127.0.0.1:8080/api/v1/books{id}

- Добавить запись:

curl -X POST http://127.0.0.1:8080/api/v1/books -d

- Удалить запись:

curl -i -X DELETE http://127.0.0.1:8080/api/v1/books/del/{id}

- Приложение возвращает значение hostname:

curl -X GET http://127.0.0.1:8080/api/v1/status



# Лабораторная работа №3: CI/CD и деплой приложения в Heroku
# Целью лабораторной работы: 
Знакомство с CI/CD и его реализацией на примере Travis CI и Heroku.
