# 基础镜像：使用 Azul Zulu OpenJDK 17
FROM azul/zulu-openjdk:17-latest

# 强制刷新缓存 20260227
WORKDIR /app

# 暴露 Spring Boot 默认端口 8080
EXPOSE 8080

# 复制整个项目到容器内
COPY . .

# 安装 Maven 并更新源（解决依赖下载慢的问题）
RUN apt-get update && apt-get install -y maven && rm -rf /var/lib/apt/lists/*

# 关键：输出详细的 Maven 构建日志，强制生成 Jar 包
RUN echo "开始构建项目..." && \
    mvn clean package -DskipTests -pl playedu-api -am -Dmaven.repo.remote=https://maven.aliyun.com/repository/public -X && \
    echo "构建完成，查看生成的 Jar 包：" && \
    ls -la playedu-api/target/

# 验证 Jar 包是否存在，不存在则报错
RUN if [ ! -f "playedu-api/target/*.jar" ]; then \
    echo "错误：Jar 包未生成！" && exit 1; \
fi

# 复制 Jar 包到容器根目录
RUN cp playedu-api/target/*.jar /app/playedu.jar

# 验证复制后的 Jar 包是否存在
RUN if [ ! -f "/app/playedu.jar" ]; then \
    echo "错误：Jar 包复制失败！" && exit 1; \
fi

# 添加调试参数，启动服务
ENV JAVA_OPTS="-Xmx512m -Xms256m -Dlogging.level.org.springframework=DEBUG"
CMD ["sh", "-c", "echo '启动服务...' && java $JAVA_OPTS -jar playedu.jar"]
