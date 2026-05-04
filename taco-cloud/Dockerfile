# Step 1：使用 Java 17 作為基底映像
FROM eclipse-temurin:17-jdk

# Step 2：在容器內建立工作目錄
WORKDIR /app

# Step 3：把 Maven wrapper 和 pom.xml 複製進去
COPY mvnw .
RUN chmod +x mvnw
COPY .mvn .mvn
COPY pom.xml .

# Step 4：下載相依套件（利用快取加速）
RUN ./mvnw dependency:go-offline

# Step 5：複製所有程式碼
COPY src src

# Step 6：編譯並打包成 JAR 檔
RUN ./mvnw package -DskipTests

# Step 7：執行應用程式
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "-Dspring.profiles.active=docker", "target/taco-cloud-0.0.1-SNAPSHOT.jar"]