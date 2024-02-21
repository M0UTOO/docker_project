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

CMD ["node", "build/index.js"]