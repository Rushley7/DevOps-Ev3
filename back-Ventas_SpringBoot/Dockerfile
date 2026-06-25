FROM maven:3.8.5-openjdk-17-slim AS build
WORKDIR /app


COPY pom.xml .
RUN mvn dependency:go-offline -B

COPY src src
RUN mvn clean package -DskipTests

FROM eclipse-temurin:17-jre-alpine
WORKDIR /app

RUN addgroup -S spring && adduser -S spring -G spring
COPY --from=build /app/target/*.jar app.jar
RUN chown spring:spring app.jar

USER spring
EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
