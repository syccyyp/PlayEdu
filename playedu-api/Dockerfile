# 使用华为云的 Maven+JDK17 镜像，彻底解决海外拉取失败
FROM swr.cn-north-4.myhuaweicloud.com/opensourceway/maven:3.8-openjdk-17

WORKDIR /app

COPY . .

# 构建子模块，用阿里云镜像加速
RUN mvn clean package -DskipTests -pl playedu-api -am -Dmaven.repo.remote=https://maven.aliyun.com/repository/public

# 启动命令（路径精准匹配）
CMD ["java", "-jar", "playedu-api/target/playedu.jar"]
