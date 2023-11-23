FROM nginx:latest

USER root

WORKDIR /home

COPY ./nginx/nginx.conf /etc/nginx/nginx.conf
COPY ./server.c /home/server.c
COPY ./script.sh /home/script.sh

EXPOSE 8080

RUN apt-get update ; \
    apt-get install -y gcc spawn-fcgi libfcgi-dev ; \
    chmod 777 script.sh

CMD [ "./script.sh" ]
