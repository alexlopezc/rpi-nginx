# NGINX on Raspberry Pi / armhf

Based on the work from [Tob1asDocker](https://github.com/Tob1asDocker/rpi-nginx)

### Supported tags and respective `Dockerfile` links
-	[`1.14-alpine` (*Dockerfile*)](https://github.com/alexlopezc/rpi-nginx/blob/master/Dockerfile) ([current Version: 1.14](https://pkgs.alpinelinux.org/package/v3.8/main/armhf/nginx) on AlpineLinux) 

### What is Nginx?
Nginx (pronounced "engine-x") is an open source reverse proxy server for HTTP, HTTPS, SMTP, POP3, and IMAP protocols, as well as a load balancer, HTTP cache, and a web server (origin server). The nginx project started with a strong focus on high concurrency, high performance and low memory usage. It is licensed under the 2-clause BSD-like license and it runs on Linux, BSD variants, Mac OS X, Solaris, AIX, HP-UX, as well as on other *nix flavors. It also has a proof of concept port for Microsoft Windows.
> [wikipedia.org/wiki/Nginx](https://en.wikipedia.org/wiki/Nginx) and [Nginx.org](http://nginx.org/en/)

![logo](https://raw.githubusercontent.com/docker-library/docs/master/nginx/logo.png)

### How to use this image

* compare with: https://hub.docker.com/_/nginx/

* ``` $ docker pull alexlopezc/rpi-nginx ```
* Optional: ``` $ mkdir -p /home/pi/{.ssl,html} && mkdir -p /home/pi/.config/nginx && touch /home/pi/.config/nginx/default.conf ``` and edit [default.conf](https://github.com/alexlopezc/rpi-nginx/blob/master/default.conf)
* Optional (SSL): 
	* ``` $ openssl req -x509 -newkey rsa:4086 -subj "/C=/ST=/L=/O=/CN=localhost" -keyout "ssl.key" -out "ssl.crt" -days 3650 -nodes -sha256 ```
	* ``` $ mv ssl.* /home/pi/.ssl/ ```
* ``` $ docker run --name nginx -d -p 80:80 -p 443:443 --link some-php-fpm-container:phphost -v /home/pi/.ssl:/etc/nginx/ssl:ro -v /home/pi/.config/nginx:/etc/nginx/conf.d:ro -v /home/pi/html:/var/www/html alexlopezc/rpi-nginx ``` 

or build it yourself
* ``` $ git clone https://github.com/alexlopezc/rpi-nginx.git && cd rpi-nginx ```
* ``` $ docker build -t alexlopezc/rpi-nginx ./VERSION/ ``` 
* Optional: ``` $  mkdir -p /home/pi/{.ssl,html} && mkdir -p /home/pi/.config/nginx && touch /home/pi/.config/nginx/default.conf ``` and edit [default.conf](https://github.com/alexlopezc/rpi-nginx/blob/master/default.conf)
* Optional (SSL)
* ``` $ docker run --name nginx -d -p 80:80 -p 443:443 --link some-php-fpm-container:phphost -v /home/pi/.ssl:/etc/nginx/ssl:ro -v /home/pi/.config/nginx:/etc/nginx/conf.d:ro -v /home/pi/html:/var/www/html alexlopezc/rpi-nginx ``` 

* http://localhost or https://localhost

### This Image on
* [DockerHub](https://hub.docker.com/r/alexlopezc/rpi-nginx/)
* [GitHub](https://github.com/alexlopezc/rpi-nginx)
