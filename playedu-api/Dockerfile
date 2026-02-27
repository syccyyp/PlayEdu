FROM azul/zulu-openjdk:17-latest

WORKDIR /app

# 复制整个项目
COPY . .

# 安装 Maven 并构建
RUN apt-get update && apt-get install -y maven
RUN mvn clean package -DskipTests -pl playedu-api -am -Dmaven.repo.remote=https://maven.aliyun.com/repository/public

# 关键：把 Jar 包复制到容器根目录，避免路径问题
RUN cp playedu-api/target/*.jar /app/playedu.jar

# 启动命令（直接从根目录找 Jar 包）
CMD ["java", "-jar", "playedu.jar"]
