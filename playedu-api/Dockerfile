# 使用包含 Maven 和 JDK17 的基础镜像，避免镜像拉取失败
FROM maven:3.8-openjdk-17

# 设置容器内的工作目录
WORKDIR /app

# 把项目所有文件复制到容器中
COPY . .

# 构建 playedu-api 子模块，用阿里云镜像加速依赖下载
RUN mvn clean package -DskipTests -pl playedu-api -am -Dmaven.repo.remote=https://maven.aliyun.com/repository/public

# 启动 Jar 包（路径精准匹配构建产物）
CMD ["java", "-jar", "playedu-api/target/playedu.jar"]
