# NGINX on Raspberry Pi

### Image Info
* without PHP
* compare with: https://hub.docker.com/_/nginx/
* http://nginx.org/

### How to use this image
* ``` docker pull tobi312/rpi-nginx ```
* Optional: ``` mkdir -p /home/pi/{.ssl,html} && mkdir -p /home/pi/.config/nginx && touch /home/pi/.config/nginx/default.conf ```
* Optional (SSL): 
	* ``` openssl req -x509 -newkey rsa:4086 -subj "/C=/ST=/L=/O=/CN=localhost" -keyout "ssl.key" -out "ssl.crt" -days 3650 -nodes -sha256 ```
	* ``` mv ssl.* /home/pi/.ssl/ ```
* ``` docker run --name nginx -d -p 80:80 -p 443:443 --link some-php-fpm-container:phphost -v /home/pi/.ssl:/etc/nginx/ssl:ro -v /home/pi/.config/nginx:/etc/nginx/conf.d:ro -v /home/pi/html:/var/www/html tobi312/rpi-nginx ``` 

or build it yourself
* ``` git clone https://github.com/TobiasH87Docker/rpi-nginx.git && cd rpi-nginx ```
* Optional: ``` mkdir -p /home/pi/{.ssl,html} && mkdir -p /home/pi/.config/nginx && touch /home/pi/.config/nginx/default.conf ```
* Optional (SSL)
* ``` docker build -t tobi312/rpi-nginx . ``` 
* ``` docker run --name nginx -d -p 80:80 -p 443:443 --link some-php-fpm-container:phphost -v /home/pi/.ssl:/etc/nginx/ssl:ro -v /home/pi/.config/nginx:/etc/nginx/conf.d:ro -v /home/pi/html:/var/www/html tobi312/rpi-nginx ``` 
* http://localhost 

### You need PHP (PHP-FPM)?, see here: 
* [DockerHub](https://hub.docker.com/r/tobi312/rpi-php/)
* [GitHub](https://github.com/TobiasH87Docker/rpi-php)

### This Image on
* [DockerHub](https://hub.docker.com/r/tobi312/rpi-nginx/)
* [GitHub](https://github.com/TobiasH87Docker/rpi-nginx)
