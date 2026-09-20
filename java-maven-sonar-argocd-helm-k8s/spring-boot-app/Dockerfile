# syntax=docker/dockerfile:1

# Build the Spring Boot executable JAR with Maven 3.9 and Temurin JDK 21.
# The project targets Java 17, which is supported by JDK 21.
FROM maven:3.9-eclipse-temurin-21 AS build

WORKDIR /workspace

# Copy the Maven descriptor first so dependency downloads are cached between builds.
COPY pom.xml ./
RUN mvn --batch-mode --no-transfer-progress dependency:go-offline

# Copy application sources and create the executable Spring Boot JAR.
COPY src ./src
RUN mvn --batch-mode --no-transfer-progress clean package -DskipTests

# Run only the built application; Maven and the source code are excluded from the final image.
FROM eclipse-temurin:21-jre

WORKDIR /app

RUN useradd --system --uid 10001 --create-home spring
COPY --from=build /workspace/target/spring-boot-web.jar app.jar

USER spring

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "/app/app.jar"]
