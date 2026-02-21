# 使用带 Maven 的基础镜像进行构建
FROM maven:3.8.4-openjdk-11-slim AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# 使用轻量级 JRE 镜像运行
FROM openjdk:11-jre-slim
WORKDIR /app
COPY --from=build /app/target/my-app-1.0-SNAPSHOT.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]