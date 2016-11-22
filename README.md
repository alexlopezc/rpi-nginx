# Dockerfile for NGINX on Raspberry Pi
* https://www.nginx.com/
* http://nginx.org/

Use:
* ``` git clone REPOSITORY && cd rpi-nginx ```
* Optional: ``` mkdir -p /home/pi/{.ssl,html} && mkdir -p /home/pi/.config/nginx && cp default.conf /home/pi/.config/nginx/ ```
* Optional (SSL): 
	* ``` openssl genrsa -out ssl.key 4096 ```
	* ``` openssl req -new -key ssl.key -out ssl.csr ```
	* ``` openssl x509 -req -days 1825 -in ssl.csr -signkey ssl.key -out ssl.crt ```
	* ``` mv ssl.* /home/pi/.ssl/ ```
* ``` docker build -t rpi-nginx . ``` 
* ``` docker run --name nginx-proxy -d -p 80:80 -p 443:443 --link some-container:alias -v /home/pi/.ssl:/etc/nginx/ssl:ro -v /home/pi/.config/nginx:/etc/nginx/conf.d:ro -v /home/pi/html:/var/www/html rpi-nginx ``` 
* http://localhost 