# Usa imagen oficial con tag existente
FROM maven:3.8.7-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:go-offline

# Copiar código fuente vacío
COPY src ./src

# Empaqueta sin ejecutar tests
RUN mvn package -DskipTests

# Imagen final
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=build /app/target/*-jar-with-dependencies.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
