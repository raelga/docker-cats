FROM nginx:alpine

EXPOSE 80

ADD --chown=nginx index.html /usr/share/nginx/html/index.html

ARG img
ADD --chown=nginx ${img} /usr/share/nginx/html/image.jpg