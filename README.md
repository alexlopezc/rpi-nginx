# NGINX on Raspberry Pi

### Image Info
* without PHP
* compare with: https://hub.docker.com/_/nginx/
* http://nginx.org/

### How to use this image
* ``` docker pull tobi312/rpi-nginx ```
* Optional: ``` mkdir -p /home/pi/{.ssl,html} && mkdir -p /home/pi/.config/nginx && cp default.conf /home/pi/.config/nginx/ ```
* Optional (SSL): 
	* ``` openssl genrsa -out ssl.key 4096 ```
	* ``` openssl req -new -key ssl.key -out ssl.csr ```
	* ``` openssl x509 -req -days 1825 -in ssl.csr -signkey ssl.key -out ssl.crt ```
	* ``` mv ssl.* /home/pi/.ssl/ ```
* ``` docker run --name nginx -d -p 80:80 -p 443:443 --link some-container:alias -v /home/pi/.ssl:/etc/nginx/ssl:ro -v /home/pi/.config/nginx:/etc/nginx/conf.d:ro -v /home/pi/html:/var/www/html tobi312/rpi-nginx ``` 

or build it yourself
* ``` git clone https://github.com/TobiasH87Docker/rpi-nginx.git && cd rpi-nginx ```
* Optional: ``` mkdir -p /home/pi/{.ssl,html} && mkdir -p /home/pi/.config/nginx && cp default.conf /home/pi/.config/nginx/ ```
* Optional (SSL)
* ``` docker build -t tobi312/rpi-nginx . ``` 
* ``` docker run --name nginx-proxy -d -p 80:80 -p 443:443 --link some-container:alias -v /home/pi/.ssl:/etc/nginx/ssl:ro -v /home/pi/.config/nginx:/etc/nginx/conf.d:ro -v /home/pi/html:/var/www/html tobi312/rpi-nginx ``` 
* http://localhost 

### This Image on
* [DockerHub](https://hub.docker.com/r/tobi312/rpi-nginx/)
* [GitHub](https://github.com/TobiasH87Docker/rpi-nginx)
