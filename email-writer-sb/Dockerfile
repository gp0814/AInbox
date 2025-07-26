# Stage 1: Build with Maven using JDK 24
FROM maven:3.9.9-eclipse-temurin-24 AS build
WORKDIR /app

# Copy only pom.xml first for dependency caching
COPY pom.xml .
RUN mvn -B dependency:go-offline

# Now copy source code
COPY src ./src
RUN mvn clean package -DskipTests -Dmaven.test.skip=true

# Stage 2: Minimal runtime image with JDK 24
FROM eclipse-temurin:24-jre-alpine
WORKDIR /app

# Copy built jar from previous stage
COPY --from=build /app/target/*.jar app.jar

ENTRYPOINT ["java", "-jar", "app.jar"]
