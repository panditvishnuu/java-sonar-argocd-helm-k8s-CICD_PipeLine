FROM maven:3.9-eclipse-temurin-17

USER root

# Install Docker CLI
RUN apt-get update \
    && apt-get install -y docker.io git \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Verify everything
RUN java -version \
    && mvn -version \
    && docker --version

USER root