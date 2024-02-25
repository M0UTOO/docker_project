# Créer un Dockerfile pour cette application en mode production

# Utiliser l'image officielle Node.js LTS comme base
FROM node:alpine AS builder

# Définir le répertoire de travail dans l'image
WORKDIR /app

# Copier les fichiers de dépendances
COPY package*.json ./

# Installer les dépendances
RUN npm install

# Copier le reste des fichiers de l'application
COPY / .

# Construire l'application pour la production
RUN npm run build

# Étape de production
FROM node:alpine AS production

# Définir le répertoire de travail pour l'étape de production
WORKDIR /app

# Copier les dépendances et les fichiers de construction depuis l'étape de builder
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/dist ./dist

# Exposer le port sur lequel le serveur backend écoute
EXPOSE 3000

# Définir la commande pour démarrer l'application
CMD ["node", "dist/main.js"]
