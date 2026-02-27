# 基础镜像：使用 Azul Zulu OpenJDK 17
FROM azul/zulu-openjdk:17-latest

# 强制刷新缓存 20260227
WORKDIR /app

# 暴露 Spring Boot 默认端口 8080，告诉 Railway 服务用 8080 端口
EXPOSE 8080

# 复制整个项目到容器内
COPY . .

# 安装 Maven 并构建
RUN apt-get update && apt-get install -y maven
RUN mvn clean package -DskipTests -pl playedu-api -am -Dmaven.repo.remote=https://maven.aliyun.com/repository/public

# 把 Jar 包复制到容器根目录，避免路径问题
RUN cp playedu-api/target/*.jar /app/playedu.jar

# 关键：让 Java 输出详细的启动日志，方便定位问题
ENV JAVA_OPTS="-Xmx512m -Xms256m -Dlogging.level.org.springframework=DEBUG"
CMD ["sh", "-c", "java $JAVA_OPTS -jar playedu.jar"]
