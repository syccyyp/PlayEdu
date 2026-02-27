# 构建阶段：使用阿里云 Maven 镜像（含 JDK17，构建更稳定）
FROM registry.cn-hangzhou.aliyuncs.com/aliyun-openjdk/openjdk:17-maven AS builder
WORKDIR /app

# 复制项目文件
COPY . .

# 构建子模块（保留阿里云镜像加速，避免依赖下载失败）
RUN mvn clean package -DskipTests -pl playedu-api -am -Dmaven.repo.remote=https://maven.aliyun.com/repository/public

# 运行阶段：使用阿里云 OpenJDK 镜像（替代官方镜像，解决拉取失败）
FROM registry.cn-hangzhou.aliyuncs.com/aliyun-openjdk/openjdk:17-slim
WORKDIR /app

# 精准复制 Jar 包
COPY --from=builder /app/playedu-api/target/playedu.jar ./playedu.jar

# 启动命令
CMD ["java", "-jar", "playedu.jar"]
