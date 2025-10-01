# Build stage
FROM maven:3.9.6-eclipse-temurin-17 AS build
WORKDIR /usr/src/app

# Pull deps first (better caching)
COPY pom.xml .
RUN mvn -B -DskipTests dependency:go-offline

# Build
COPY src ./src
RUN mvn -B -DskipTests clean package

# Runtime stage
FROM eclipse-temurin:17-jre
WORKDIR /app
COPY --from=build /usr/src/app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","/app/app.jar"]
