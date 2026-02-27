# 使用阿里云的 Maven+JDK 镜像，彻底解决拉取失败
FROM registry.cn-hangzhou.aliyuncs.com/aliyun-maven/maven:3.8-openjdk-17

# 设置工作目录
WORKDIR /app

# 复制整个项目到容器
COPY . .

# 构建子模块，用阿里云镜像加速
RUN mvn clean package -DskipTests -pl playedu-api -am -Dmaven.repo.remote=https://maven.aliyun.com/repository/public

# 启动命令（路径精准匹配）
CMD ["java", "-jar", "playedu-api/target/playedu.jar"]
