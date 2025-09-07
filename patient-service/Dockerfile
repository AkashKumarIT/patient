##FROM maven:3.8.5-openjdk-17-slim AS build
#
#FROM maven:3.9.9-eclipse-temurin-17 AS builder
#
#WORKDIR /app
#
#COPY pom.xml .
#
#RUN mvn dependency:go-offline -B
#
#COPY src ./src
#
#RUN mvn clean package
#
#FROM openjdk:17-jdk AS runner
#
#WORKDIR /app
#
#COPY --from=builder ./app/target/patient-service-0.0.1-SNAPSHOT.jar ./patient-service.jar
#
#EXPOSE 4000
#
#ENTRYPOINT ["java","-jar","patient-service.jar"]


# Stage 1: Build with Maven
FROM maven:3.9.4-eclipse-temurin-17 AS builder

WORKDIR /app

# Copy pom.xml and download dependencies
COPY pom.xml .
RUN mvn dependency:go-offline -B

# Copy source code and build
COPY src ./src
RUN mvn clean package -DskipTests

# Stage 2: Run with Java only
FROM eclipse-temurin:17-jdk-alpine

WORKDIR /app

# Copy jar from builder stage
COPY --from=builder /app/target/patient-service-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 4000

CMD ["java", "-jar", "app.jar"]


