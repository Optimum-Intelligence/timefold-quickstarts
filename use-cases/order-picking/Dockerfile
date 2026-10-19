# Builds the order-picking Quarkus application. The runtime image only starts its HTTP API.
FROM maven:3.9-eclipse-temurin-21 AS build
WORKDIR /build
COPY pom.xml .
COPY src ./src
RUN mvn -B package -DskipTests

FROM eclipse-temurin:21-jre
WORKDIR /deployments
RUN useradd --uid 1001 --create-home app
COPY --from=build --chown=1001:1001 /build/target/quarkus-app/ ./
USER 1001
EXPOSE 8080
ENV QUARKUS_HTTP_HOST=0.0.0.0
ENTRYPOINT ["java", "-jar", "quarkus-run.jar"]
