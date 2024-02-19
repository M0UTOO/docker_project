# Créer un Dockerfile pour cette application en mode production

FROM nginx:latest

COPY nginx.conf /etc/nginx/nginx.conf

WORKDIR /var/www/html

COPY . /var/www/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]