FROM openjdk:17-jdk-slim

WORKDIR /app

# Copier le wrapper Maven et les fichiers de configuration
COPY mvnw .
COPY .mvn .mvn
COPY pom.xml .

# Rendre le wrapper exécutable
RUN chmod +x ./mvnw

# Télécharger les dépendances
RUN ./mvnw dependency:go-offline -B

# Copier le code source
COPY src src

# Construire l'application
RUN ./mvnw clean package -DskipTests

# Exposer le port
EXPOSE 8080

# Lancer l'application
CMD ["java", "-jar", "target/*.jar"]