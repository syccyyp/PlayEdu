# 构建阶段
FROM maven:3.8-openjdk-17 AS builder
WORKDIR /app

# 复制整个项目到容器
COPY . .

# 只构建 playedu-api 子模块，并使用阿里云镜像加速
RUN mvn clean package -DskipTests -pl playedu-api -am -Dmaven.repo.remote=https://maven.aliyun.com/repository/public

# 运行阶段
FROM openjdk:17-jdk-slim
WORKDIR /app

# 从构建阶段复制构建好的 Jar 包
COPY --from=builder /app/playedu-api/target/playedu.jar .

# 启动命令
CMD ["java", "-jar", "playedu.jar"]
