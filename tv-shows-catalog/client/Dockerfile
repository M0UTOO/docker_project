# Créer un Dockerfile pour cette application en mode production

# Etape 1: Construire l'application avec Node.js
FROM node:lts AS build

# Définir le répertoire de travail
WORKDIR /app

# Copier les fichiers de dépendances
COPY client/package*.json ./

# Installer les dépendances
RUN npm install

# Copier les sources de l'application
COPY client/ .

# Récupérer l'URL de l'API à partir du docker-compose
ARG API_BASE_URL
ENV API_BASE_URL=${API_BASE_URL}

# Construire l'application
RUN npm run build

# Etape 2: Configurer Nginx pour servir l'application
FROM nginx:stable-alpine AS production

# Copier les fichiers construits depuis l'étape de construction vers le répertoire de travail de Nginx
COPY --from=build /app/build /usr/share/nginx/html

# (Optionnel) Copier une configuration Nginx person<<nalisée si nécessaire
# COPY path/to/your/nginx.conf /etc/nginx/nginx.conf

# Exposer le port (Nginx écoute sur le port 80 par défaut)
EXPOSE 80

# Lancer Nginx; pas besoin de commande CMD car l'image de base Nginx en a déjà une pour démarrer le serveur.
