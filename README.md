# Дипломный проект по итогам курса "Тестировщик ПО"

## Документация
* [План выполнения работ](https://github.com/KtulhskiyPraynik/BelatedDiploma/blob/master/Documents/Plan.md)
* [Отчет о проведенном тестировании](https://github.com/KtulhskiyPraynik/BelatedDiploma/blob/master/Documents/Report.md)
* [Отчет о проведенной автоматизации](https://github.com/KtulhskiyPraynik/BelatedDiploma/blob/master/Documents/Summary.md)

## О проекте
Приложение представляет из себя веб-сервис.

![Превью](https://user-images.githubusercontent.com/96628961/200314255-c2da75c9-db6e-47d2-bf0e-111e04c227ef.png)

Приложение предлагает купить тур по определённой цене с помощью двух способов:

* Обычная оплата по дебетовой карте
* Уникальная технология: выдача кредита по данным банковской карты

Само приложение не обрабатывает данные по картам, а пересылает их банковским сервисам:

* сервису платежей (далее - Payment Gate)
* кредитному сервису (далее - Credit Gate)

Сервис может взаимодействоватьс СУБД MySql и PostgreSql

База данных хранит информацию о заказах, платежах, статусах карт, способах оплаты.

## Цели проекта
В рамках проекта необходимо автоматизировать тестирование комплексного сервиса покупки тура, взаимодействующего с СУБД и API Банка.# Подготовка к запуску тестов

## Предусловия
Если необходимое ПО уже установлено, то в предусловиях достаточно только открыть проект в IDEA.

* Склонировать себе данный репозиторий командой `git clone`
* Установить и запустить Docker Desktop. Скачать программу можно с официального сайта [по ссылке](https://docs.docker.com/desktop/install/windows-install/). Порядок установки можно прочитать [здесь](https://github.com/netology-code/aqa-homeworks/blob/master/docker/installation.md)
* Установить IntelliJ IDEA (Communicate или Ultimate) версию. Скачать можно с официального сайта [по ссылке](https://www.jetbrains.com/ru-ru/idea/download/#section=windows) 
* Открыть склонированный проект в IDEA

## Запуск контейнеров и SUT
1. Запустить контейнеры докера, поднимающие БД MySQL, PostgreSql и сервис платежей payment-gate на node.js. Для этого в терминале IDEA ввести команду `docker-compose up -d`
2. Запустить SUT в зависимости нужного подключения к БД. Для этого:
* Для подключения к БД MySql в терминале IDEA ввести команду: `java "-Dspring.datasource.url=jdbc:mysql://localhost:3306/app" -jar ./artifacts/aqa-shop.jar`
* Для подключения к БД PostgresSql в терминале IDEA ввести команду: `java "-Dspring.datasource.url=jdbc:postgresql://localhost:5432/app" -jar ./artifacts/aqa-shop.jar`
3. Проверить успешность запуска SUT по адресу http://localhost:8080/

## Запуск тестов и генерация отчета Allure
1. В зависимости от подключенной БД в терминале IDEA в новой вкладке выполнить команду:
* При подключенной БД MySql: `./gradlew clean test -D db.url=jdbc:mysql://localhost:3306/app`
* При подключенной БД PostgreSql: `./gradlew clean test -D db.url=jdbc:postgresql://localhost:5432/app`
2. Сгенерировать отчет Allure, выполнив команду в терминале IDEA: `./gradlew allureServe`
* Если отчет не открывается автоматически в браузере, то выполнить команду: `./gradlew allureReport` и открыть отчет вручную (файл index.html) по адресу: `.\build\reports\allure-report\allureReport`
3. При необходимости изменить подключение к другой БД, необходимо остановить подключения в терминалах черех Ctrl + C в окне терминала
