# 使用官方 Golang 镜像作为构建阶段的基础镜像
FROM golang:1.24.1 AS builder

# 设置工作目录
WORKDIR /app

# 将当前目录内容复制到容器的工作目录
COPY . .

# 下载并安装项目依赖
RUN go mod tidy

# 编译 Go 项目
RUN go build -o halalcloud .

FROM python:3.9
RUN useradd -m -u 1000 user

USER user
ENV PATH="/home/user/.local/bin:$PATH"

WORKDIR /app
COPY --from=builder /app/halalcloud /home/user/.local/bin/halalcloud
CMD ["halalcloud"]
EXPOSE 8080