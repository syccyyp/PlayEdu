FROM azul/zulu-openjdk:17-latest
# 强制刷新缓存 20260227
WORKDIR /app
EXPOSE 8080  # <-- 新增这一行，告诉 Railway 服务用 8080 端口
COPY . .
# ... 以下内容保持不变
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
FROM azul/zulu-openjdk:17-latest
# 强制刷新缓存 20260227  # 这行是新增的注释，随便写点内容就行
WORKDIR /app
