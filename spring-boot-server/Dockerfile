# Utiliser une image de base OpenJDK pour exécuter l'application Spring Boot
FROM openjdk:17-jdk-slim

# Spécifier le répertoire de travail
WORKDIR /app

# Copier le fichier JAR du backend dans le container
COPY target/*.jar backend-app.jar

# Exposer le port utilisé par Spring Boot
EXPOSE 8080

# Exécuter l'application Spring Boot
ENTRYPOINT ["java", "-jar", "backend-app.jar"]
