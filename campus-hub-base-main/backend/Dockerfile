# Stage 1: build ung dung bang Gradle (JDK 21, khop toolchain trong build.gradle)
FROM eclipse-temurin:21-jdk-jammy AS build
WORKDIR /app

# Copy cau hinh Gradle truoc de tan dung layer cache
COPY gradlew gradlew.bat settings.gradle build.gradle ./
COPY gradle ./gradle
RUN chmod +x gradlew

# Copy source va build jar (bo qua test vi da chay o local)
COPY src ./src
RUN ./gradlew bootJar --no-daemon -x test

# Stage 2: chay ung dung (chi can JRE 21, image gon nhe)
FROM eclipse-temurin:21-jre-jammy
WORKDIR /app
COPY --from=build /app/build/libs/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
