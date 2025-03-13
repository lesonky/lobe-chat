# MacoChat - 基于 LobeChat 的定制版本

MacoChat 是基于 [LobeChat](https://github.com/lobehub/lobe-chat) 的定制版本，专为 macOS 用户优化，默认使用 Google Vertex AI 的 Gemini 模型。

## 特点

- 默认使用 Google Vertex AI 的 Gemini 模型
- 简化的用户界面，移除了不必要的设置选项
- 使用 Docker 容器化部署，简单易用

## 快速开始

### 前提条件

- 安装 [Docker](https://www.docker.com/products/docker-desktop/)
- 获取 Google Vertex AI 的凭证和项目 ID

### 使用 Docker Compose 部署

1. 克隆仓库：

```bash
# git clone https://github.com/yourusername/macochat.git
# cd macochat
```

2. 编辑 `docker-compose.macochat.yml` 文件，填入您的 Vertex AI 凭证和项目 ID：

```yaml
# VertexAI 设置
- VERTEXAI_CREDENTIALS=your_credentials_here # 填入您的 VertexAI 凭证
- VERTEXAI_PROJECT=your_project_id_here # 填入您的 VertexAI 项目 ID
```

3. 构建并启动容器：

```bash
docker-compose -f docker-compose.macochat.yml up -d
```

4. 访问 MacoChat：

在浏览器中打开 `http://localhost:3210`

## 配置选项

### 设置访问密码

编辑 `docker-compose.macochat.yml` 文件中的 `ACCESS_CODE` 环境变量：

```yaml
- ACCESS_CODE=your_password_here # 设置访问密码
```

### 使用代理

如果需要使用代理，编辑 `docker-compose.macochat.yml` 文件中的 `PROXY_URL` 环境变量：

```yaml
- PROXY_URL=http://username:password@host:port # HTTP 代理
# 或
- PROXY_URL=socks5://username:password@host:port # SOCKS5 代理
```

### 启用其他 AI 模型提供商

MacoChat 默认使用 Google Vertex AI 的 Gemini 模型，但您也可以启用其他模型提供商。例如，启用 OpenAI：

```yaml
# OpenAI 设置
- ENABLED_OPENAI=1
- OPENAI_API_KEY=your_openai_api_key_here
```

## 从源码构建

如果您想从源码构建 MacoChat，可以使用以下命令：

```bash
# 构建 Docker 镜像
docker build -f Dockerfile.macochat -t macochat .

# 运行容器
docker run -d -p 3210:3210 \
  -e VERTEXAI_CREDENTIALS=your_credentials_here \
  -e VERTEXAI_PROJECT=your_project_id_here \
  --name macochat macochat
```

## 常见问题

### 如何获取 Google Vertex AI 凭证？

1. 访问 [Google Cloud Console](https://console.cloud.google.com/)
2. 创建一个新项目或选择现有项目
3. 启用 Vertex AI API
4. 创建服务账号并下载 JSON 凭证文件
5. 将 JSON 文件内容作为 `VERTEXAI_CREDENTIALS` 环境变量的值

### 如何更新 MacoChat？

```bash
# 停止并删除旧容器
docker-compose -f docker-compose.macochat.yml down

# 拉取最新代码
git pull

# 重新构建并启动容器
docker-compose -f docker-compose.macochat.yml up -d --build
```

## 许可证

MacoChat 继承了 LobeChat 的 MIT 许可证。详情请参阅 [LICENSE](LICENSE) 文件。
