# Étape 1 : Build Angular
FROM node:18 AS build
WORKDIR /app
COPY . .
RUN npm install && npm run build

# Étape 2 : Serveur Nginx
FROM nginx:alpine
COPY --from=build /app/dist/front-end /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
