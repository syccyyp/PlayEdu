# 使用一个公开、无需认证的基础镜像
FROM azul/zulu-openjdk:17-latest

# 设置工作目录
WORKDIR /app

# 复制整个项目到容器
COPY . .

# 直接下载 Maven 并构建（彻底绕开镜像拉取问题）
RUN apt-get update && apt-get install -y maven
RUN mvn clean package -DskipTests -pl playedu-api -am -Dmaven.repo.remote=https://maven.aliyun.com/repository/public

# 启动命令（路径精准匹配）
CMD ["java", "-jar", "target/playedu.jar"]
