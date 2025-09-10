# Use official Java 17 image (good for Spring Boot 3.x)
FROM openjdk:17-jdk-slim

# Set working directory
WORKDIR /app

# Copy Maven wrapper & pom.xml first (better caching)
COPY mvnw .
COPY .mvn .mvn
COPY pom.xml .

# Download dependencies (so they are cached unless pom.xml changes)
RUN ./mvnw dependency:go-offline -B

# Copy source code
COPY src src

# Package the app
RUN ./mvnw clean package -DskipTests

# Run the JAR (note: use Render's PORT env variable)
CMD ["java", "-jar", "app.jar"]
