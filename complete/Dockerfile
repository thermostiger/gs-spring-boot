# 第一阶段：使用 Java 17 的 Maven 镜像进行编译打包
FROM maven:3.9-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# 第二阶段：使用 Java 17 的轻量级 JRE 镜像运行
FROM eclipse-temurin:17-jre
WORKDIR /app
# Spring Boot 打包出来通常在 target 目录下
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
