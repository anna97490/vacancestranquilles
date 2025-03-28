# Étape 1 : Builder l’application Angular
FROM node:18-alpine AS build

WORKDIR /app

# Copier uniquement package.json et package-lock.json pour optimiser le cache
COPY package*.json ./
RUN npm install

# Copier le reste du code et exécuter le build
COPY . .
RUN npm run build --prod

# Étape 2 : Servir l’application avec Nginx
FROM nginx:alpine

# Supprimer la configuration par défaut de Nginx
RUN rm -rf /usr/share/nginx/html/*

# Copier les fichiers Angular buildés vers le dossier Nginx
COPY --from=build /app/dist/frontend /usr/share/nginx/html

# Exposer le port HTTP de Nginx
EXPOSE 80

# Démarrer Nginx
CMD ["nginx", "-g", "daemon off;"]
