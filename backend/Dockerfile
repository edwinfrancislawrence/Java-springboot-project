
# ## Optimizing image example ##
# # Stage 1 — Build JAR
# FROM maven:3.9.9-amazoncorretto-11 AS builder
# WORKDIR /app
# COPY . /app
# RUN mvn clean package -Dspring.profiles.active=build -DskipTests

# # Stage 2 — Run JAR
# FROM amazoncorretto:11-alpine-jdk
# WORKDIR /app

# # Copy the built JAR from the builder stage
# COPY --from=builder /app/target/*.jar app.jar

# # Set default environment variables (can be overridden at runtime)
# # ENV SPRING_DATASOURCE_URL="jdbc:mysql://database-1.ckjyc24s4jgb.us-east-1.rds.amazonaws.com:3306/datastore?createDatabaseIfNotExist=true"
# # ENV SPRING_DATASOURCE_USERNAME="admin"
# # ENV SPRING_DATASOURCE_PASSWORD="Cloud123"
# # ENV SPRING_JPA_HIBERNATE_DDL_AUTO="update"
# # ENV SERVER_PORT=8084

# # Expose the port (optional)
# EXPOSE 8084

# # Start the application
# CMD ["java", "-jar", "app.jar"]




# ### large image example ####

# # FROM maven:3.9.9-amazoncorretto-11

# # WORKDIR /app

# # # Copy project files
# # COPY . .

# # # Build the JAR and rename it to a fixed name
# # RUN mvn clean package -Dspring.profiles.active=build -DskipTests \
# #  && cp target/*.jar app.jar

# # # Environment variables
# # ENV SPRING_DATASOURCE_URL="jdbc:mysql://database-1.c0jsiw6iwv14.us-east-1.rds.amazonaws.com/datastore?createDatabaseIfNotExist=true"
# # ENV SPRING_DATASOURCE_USERNAME="admin"
# # ENV SPRING_DATASOURCE_PASSWORD="Cloud123"
# # ENV SPRING_JPA_HIBERNATE_DDL_AUTO="update"
# # ENV SERVER_PORT=8084

# # # Expose port
# # EXPOSE 8084

# # # Run application
# # CMD ["java", "-jar", "app.jar"]

# ## Optimizing image example ##
# # Stage 1 — Build JAR
# FROM maven:3.9.9-amazoncorretto-11 AS builder
# WORKDIR /app
# COPY . /app
# RUN mvn clean package -Dspring.profiles.active=build -DskipTests

# # Stage 2 — Run JAR
# FROM amazoncorretto:11-alpine-jdk
# WORKDIR /app

# # 1. Create a secure, non-root system group and user in Alpine Linux
# RUN addgroup -g 10001 appgroup && \
#     adduser -u 10001 -G appgroup -h /home/appuser -s /sbin/nologin -D appuser

# # 2. Copy the built JAR from the builder stage AND assign ownership to appuser
# COPY --from=builder --chown=appuser:appgroup /app/target/*.jar app.jar

# # Set default environment variables (can be overridden at runtime)
# # ENV SPRING_DATASOURCE_URL="jdbc:mysql://database-1.ckjyc24s4jgb.us-east-1.rds.amazonaws.com:3306/datastore?createDatabaseIfNotExist=true"
# # ENV SPRING_DATASOURCE_USERNAME="admin"
# # ENV SPRING_DATASOURCE_PASSWORD="Cloud123"
# # ENV SPRING_JPA_HIBERNATE_DDL_AUTO="update"
# # ENV SERVER_PORT=8084

# # Expose the port
# EXPOSE 8084

# # 3. Switch execution context from root to the restricted user
# USER appuser

# # Start the application
# CMD ["java", "-jar", "app.jar"]

# ==========================================
# NON ROOT USER
# ==========================================
## Optimizing image example ##
# Stage 1 — Build JAR
FROM maven:3.9.9-amazoncorretto-11 AS builder
WORKDIR /app
COPY . /app
RUN mvn clean package -Dspring.profiles.active=build -DskipTests

# Stage 2 — Run JAR
FROM amazoncorretto:11-alpine-jdk
WORKDIR /app

# 1. Create a secure, non-root system group and user in Alpine Linux
RUN addgroup -g 10001 appgroup && \
    adduser -u 10001 -G appgroup -h /home/appuser -s /sbin/nologin -D appuser

# 2. Copy the built JAR from the builder stage AND assign ownership to appuser
COPY --from=builder --chown=appuser:appgroup /app/target/*.jar app.jar

# Set default environment variables (can be overridden at runtime)
ENV SPRING_DATASOURCE_URL="jdbc:mysql://database-1.cna8om0cwk7x.us-west-2.rds.amazonaws.com:3306/datastore?createDatabaseIfNotExist=true"
ENV SPRING_DATASOURCE_USERNAME="admin"
ENV SPRING_DATASOURCE_PASSWORD="Edwin123"
ENV SPRING_JPA_HIBERNATE_DDL_AUTO="update"
ENV SERVER_PORT=8084

# Expose the port
EXPOSE 8084

# 3. Switch execution context from root to the restricted user
USER appuser

# Start the application
CMD ["java", "-jar", "app.jar"]
