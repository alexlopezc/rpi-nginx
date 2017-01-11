#FROM resin/rpi-raspbian:latest
FROM jsurf/rpi-raspbian:latest

MAINTAINER Tobias Hargesheimer <docker@ison.ws>

RUN [ "cross-build-start" ]

ENV NGINX_VERSION 1.10.*

RUN echo "deb http://mirrordirector.raspbian.org/raspbian/ stretch main contrib non-free rpi" >> /etc/apt/sources.list.d/stretch.list && echo 'Package: *\n\
Pin: release n=stretch\n\
Pin-Priority: 400\n'\
>> /etc/apt/preferences.d/stretch-pinning

RUN apt-get update \
	&& apt-get install -y -t stretch ca-certificates nginx=${NGINX_VERSION} \
	&& rm -rf /var/lib/apt/lists/*

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
	&& ln -sf /dev/stderr /var/log/nginx/error.log
	
# fix: *** stack smashing detected ***: nginx: worker process terminated / [alert] 9#9: worker process *process-id* exited on signal 6
RUN sed -i "s/worker_processes auto;/worker_processes 1;/g" /etc/nginx/nginx.conf

RUN [ "cross-build-end" ]
	
EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
