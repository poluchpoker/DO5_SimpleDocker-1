FROM nginx:latest

ARG USERNAME=nginx

USER root


COPY ./nginx/nginx.conf /etc/nginx/nginx.conf
COPY ./script.sh /home/$USERNAME/script.sh

WORKDIR /home/$USERNAME

RUN usermod -aG adm,root,nginx $USERNAME ; \
    chown -R $USERNAME:$USERNAME /var/cache/nginx/ ; \
    chown -R $USERNAME:$USERNAME /var/run/ ; \
    chown -R $USERNAME:$USERNAME /home/$USERNAME/ ; \
    chmod +x /home/$USERNAME/script.sh

USER $USERNAME

HEALTHCHECK --interval=5s --timeout=10s --retries=3 CMD curl -sS 127.0.0.1 || exit 1

CMD [ "./script.sh" ]
