# Créer un Dockerfile pour cette application en mode production

# Etape 1: Construire l'application avec Node.js
FROM node:alpine AS build

# Définir le répertoire de travail
WORKDIR /app

# Copier les fichiers de dépendances
COPY package*.json ./

# Installer les dépendances
RUN npm install

# Copier les sources de l'application
COPY / .

# Récupérer l'URL de l'API à partir du docker-compose
ARG API_BASE_URL
ENV API_BASE_URL=${API_BASE_URL}

# Construire l'application
RUN npm run build

CMD ["node", "build/index.js"]