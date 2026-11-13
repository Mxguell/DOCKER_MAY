FROM php:8.5-apache

RUN apt-get update && apt-get install -y nano git && rm -rf /var/lib/apt/lists/*

RUN echo "HOLA SOY Mxguell" > /var/www/html/index.html

RUN echo "^<?php phpinfo(); ?>" > /var/www/html/info.php
