# LAMP bitrix

* PHP 7.2
* Apache 2.4
* MySQL 5.7


Виртуальные хосты в `./config/vhosts`. 

Настройки окружения в `.env` пример в `sample.env`

Базы данных в `./data/mysql`

Сайты в `./www`

Логи в `./logs`

## Запуск сервера 
docker-compose up -d

`http://localhost`


## Зайти на сервер 
docker-compose exec webserver bash 


#### Расширения apache2

* rewrite
* headers


#### Расширения php

* mysqli
* mbstring
* zip
* intl
* mcrypt
* curl
* json
* iconv
* xml
* xmlrpc
* gd
