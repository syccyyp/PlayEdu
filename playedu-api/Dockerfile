FROM azul/zulu-openjdk:17-latest

WORKDIR /app

COPY . .

RUN apt-get update && apt-get install -y maven
RUN mvn clean package -DskipTests -pl playedu-api -am -Dmaven.repo.remote=https://maven.aliyun.com/repository/public

# 新增：强制打印所有 Jar 包的绝对路径
RUN find /app -name "*.jar"

# 先注释掉启动命令，避免报错
# CMD ["java", "-jar", "target/playedu.jar"]
