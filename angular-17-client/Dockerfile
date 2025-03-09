# Utiliser une image Node.js pour installer Angular
FROM node:20

# Spécifier le répertoire de travail
WORKDIR /app

# Copier les fichiers package.json et package-lock.json
COPY package*.json ./

# Installer les dépendances
RUN npm install

# Copier le code source de l'application Angular
COPY . .

# Construire l'application Angular
RUN npm run build --prod

# Exposer le port pour Angular (par défaut 4200)
EXPOSE 4200

# Lancer le serveur Angular
CMD ["npm", "start"]
