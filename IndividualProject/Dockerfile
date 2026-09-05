FROM eclipse-temurin:17-jdk AS build
WORKDIR /app
COPY .mvn/ .mvn/
COPY mvnw pom.xml checkstyle.xml ./
COPY src ./src
RUN chmod +x mvnw \
    && ./mvnw -B -q package -DskipTests -Dcheckstyle.skip=true

FROM eclipse-temurin:17-jre
WORKDIR /app
COPY --from=build /app/target/taxapi-0.0.1-SNAPSHOT.jar app.jar
EXPOSE 8080
ENTRYPOINT ["sh", "-c", "java -jar /app/app.jar --server.port=${PORT:-8080}"]
