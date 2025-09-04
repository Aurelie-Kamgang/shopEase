# ===== Build =====
FROM maven:3.9.8-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
RUN mvn -q -DskipTests dependency:go-offline
COPY src ./src
# build + mettre le jar sous un nom fixe
RUN mvn -q -DskipTests package && \
    ls -l target && \
    (cp target/*-SNAPSHOT.jar /app/app.jar || cp target/*.jar /app/app.jar)

# ===== Run (JRE only) =====
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=build /app/app.jar /app/app.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","/app/app.jar"]
