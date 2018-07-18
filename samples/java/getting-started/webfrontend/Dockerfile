FROM maven:3.5-jdk-8-slim AS build
WORKDIR /usr/src/app
COPY pom.xml .
RUN ["/usr/local/bin/mvn-entrypoint.sh", "mvn", "verify", "clean", "--fail-never"]
COPY . .
RUN ["mvn", "package"]

FROM openjdk:8-jre-slim AS final
WORKDIR /usr/src/app
COPY --from=build /usr/src/app/target .
EXPOSE 8080
CMD ["java", "-jar", "webfrontend-0.1.0.jar"]