# Пропишем версию
version: '3.3'
# # Перечислим сервисы
services:
    nginx:
# Пропишем какой образ мы хотим использовать
      image: nginx:latest
# Назовем свой контейнер по красивому
      container_name: nginx

# Проброс портов
       ports:
        - "80:80"
        - "443:443"
# Проброс папок
       volumes:
        - ./nginx/core:/etc/nginx/conf.d
        - ./nginx/www:/var/www/
        - ./nginx/logs:/var/log/nginx/
        - ./nginx/html:/usr/share/nginx/html/
# Укажем зависимости
       links:
        - php
        mysql:
         image: mysql:latest
        ports:
         - "3306:3306"
        container_name: mysql
# Пропишем настройки, предлагаю использовать 
# вместо mypassword более сложный пароль, он принадлежит root
        environment:
         - MYSQL_ROOT_PASSWORD=DbrnjhbZ88
         - MYSQL_DATABASE=magento2
         - MYSQL_USER=magento2
         - MYSQL_PASSWORD=magento2
        volumes:
         - ./mysql:/var/lib/mysql
        php:
# Билдим с помощью dockerfile указав директорию где он лежит
        build: ./php
        container_name: php-fpm
        volumes:
        - ./nginx/www:/var/www
        links:
        - mysql
        phpmyadmin:
        image: phpmyadmin/phpmyadmin
        container_name: phpmyadmin
        ports:
        - 8090:80
        links:
        - mysql:db





