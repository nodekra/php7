# PHP7-FPM
PHP7 docker image with useful extensions: 
- zip
- intl
- soap
- mysqli
- pd0 pdo_mysql pdo_pgsql
- gd
- mcrypt
- iconv
- gmp
- redis
- apcu
- xdebug

Tags & Dockerfiles:  
based on `php:7-fpm` (debian based php image):  
- `latest` - (`~275MB`) [(Dockerfile)](https://github.com/m2sh/php7/blob/master/Dockerfile)
- `light`  - (`~275MB`) - [(light/Dockerfile)](https://github.com/m2sh/php7/blob/master/light/Dockerfile)   

based on `php:7-fpm-alpine` (alpine based php image):  
- `alpine` - (`~52MB`) [(alpine/Dockerfile)](https://github.com/m2sh/php7/blob/master/alpine/Dockerfile)
