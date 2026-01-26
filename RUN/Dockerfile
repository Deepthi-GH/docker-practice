FROM almalinux:9
RUN dnf install nginx -y # we are installing nginx on alamalinux:9
RUN echo "welcome to nginx" > /usr/share/nginx/html/index.html
CMD ["nginx","-g","daemon off;"]