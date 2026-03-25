# 智能翻译助手 (Translation AI Agent)

[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5.6-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![Java](https://img.shields.io/badge/Java-21-orange.svg)](https://openjdk.java.net/)
[![Spring AI](https://img.shields.io/badge/Spring%20AI-1.0.0-blue.svg)](https://spring.io/projects/spring-ai)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

🌍 **基于 Spring AI 的多语言智能翻译系统** - 支持文本翻译、文档翻译、实时对话翻译等功能，提供 50+ 种语言的高质量翻译服务。

---

## 📖 目录

- [功能特性](#-功能特性)
- [技术架构](#-技术架构)
- [快速开始](#-快速开始)
- [配置说明](#-配置说明)
- [项目结构](#-项目结构)
- [API 文档](#-api-文档)
- [数据库设计](#-数据库设计)
- [部署指南](#-部署指南)
- [开发指南](#-开发指南)
- [常见问题](#-常见问题)
- [贡献指南](#-贡献指南)
- [许可证](#-许可证)

---

## ✨ 功能特性

### 核心功能

#### 📝 文本翻译
- 支持 50+ 种语言的即时翻译
- 基于通义千问 Qwen3-Max 大模型
- 支持专业术语库匹配
- 翻译历史记录自动保存
- 上下文智能理解

#### 📄 文档翻译
- 支持多种文档格式（PDF、Word、Excel、TXT 等）
- 保持原文档格式不变
- 批量文档翻译
- 文档翻译进度实时跟踪
- MinIO 分布式文件存储

#### 💬 实时对话翻译
- 支持多轮对话翻译
- 聊天会话管理
- 对话记录持久化
- WebSocket 实时通信

#### 📚 术语库管理
- 自定义术语库分类
- 术语条目增删改查
- 术语批量导入导出
- 术语智能推荐
- 多语言术语对照

#### ⭐ 质量评估
- 翻译质量评分系统
- 用户反馈收集
- 质量统计分析
- 改进建议生成

#### 💎 会员系统
- 多级会员等级（普通/VIP/SVIP）
- 会员权益管理
- 积分系统
- 充值续费

#### 💰 支付系统
- 支付宝支付集成
- 微信支付集成
- 订单管理
- 支付回调处理

#### 📊 统计分析
- 使用量统计
- 翻译趋势分析
- 用户行为分析
- 数据可视化报表

### 其他特性

- 🔐 **用户认证**: JWT Token 身份验证
- 🎨 **响应式 UI**: Thymeleaf 模板引擎，适配移动端
- 🚀 **异步处理**: 基于 Spring Async 的异步任务处理
- 💾 **缓存优化**: Redis 分布式缓存
- 🔍 **全文搜索**: Elasticsearch 搜索引擎
- 📢 **消息通知**: WebSocket 实时推送
- 🛡️ **安全防护**: XSS 防护、SQL 注入防护
- 📈 **性能监控**: 完整的日志和统计系统

---

## 🏗️ 技术架构

### 后端技术栈

| 技术 | 版本 | 说明 |
|------|------|------|
| **框架** | Spring Boot 3.5.6 | 核心应用框架 |
| **JDK** | 21 | Java 开发工具包 |
| **AI** | Spring AI 1.0.0 | AI 模型集成框架 |
| **ORM** | Spring Data JPA | 数据持久层 |
| **数据库** | MySQL 8.0+ | 关系型数据库 |
| **缓存** | Redis | 分布式缓存 |
| **搜索** | Elasticsearch | 全文搜索引擎 |
| **文件存储** | MinIO | 对象存储服务 |
| **模板引擎** | Thymeleaf | Web 页面渲染 |
| **WebSocket** | Spring WebSocket | 实时通信 |

### AI 服务

| 服务 | 用途 | 模型/配置 |
|------|------|-----------|
| **通义千问** | 文本翻译 | Qwen3-Max |
| **阿里云翻译** | 专业翻译补充 | mt.cn-hangzhou.aliyuncs.com |

### 支付服务

| 支付方式 | 集成类型 | 场景 |
|----------|----------|------|
| **支付宝** | 当面付 | 扫码支付 |
| **微信支付** | Native 支付 | 扫码支付 |

---

## 🚀 快速开始

### 环境要求

- **JDK**: 21+
- **Maven**: 3.6+
- **MySQL**: 8.0+
- **Redis**: 6.0+
- **Elasticsearch**: 7.x+
- **MinIO**: 8.x+

### 1. 克隆项目

```bash
git clone https://github.com/yourusername/translation-ai-agent.git
cd translation-ai-agent
```

### 2. 安装依赖

```bash
mvn clean install
```

### 3. 数据库初始化

```bash
# 执行 SQL 脚本
mysql -u root -p < database/01_create_tables.sql
mysql -u root -p < database/02_init_data.sql
mysql -u root -p < database/03_create_indexes.sql
```

### 4. 配置环境变量

编辑 `src/main/resources/application.yml`，配置以下必需的环境变量：

```yaml
# 数据库配置
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/translation?useUnicode=true&characterEncoding=utf8
    username: root
    password: your_password
  
  # Redis 配置
  data:
    redis:
      host: localhost
      port: 6379
      password: your_redis_password
  
  # Elasticsearch 配置
  data:
    elasticsearch:
      uris: http://localhost:9200

# AI 服务配置
ai:
  dashscope:
    api-key: your_qwen_api_key
  
  aliyun:
    access-key-id: your_aliyun_access_key_id
    access-key-secret: your_aliyun_access_key_secret

# MinIO 配置
minio:
  endpoint: http://localhost:9000
  accessKey: your_minio_access_key
  secretKey: your_minio_secret_key
```

### 5. 启动应用

```bash
mvn spring-boot:run
```

或运行主类：

```bash
java -jar target/translation-ai-agent-1.0.0.jar
```

### 6. 访问应用

打开浏览器访问：**http://localhost:7002**

默认管理员账号（根据初始化数据）：
- 用户名：`admin`
- 密码：查看 `database/02_init_data.sql`

---

## ⚙️ 配置说明

### 核心配置项

#### 1. 服务器配置

```yaml
server:
  port: 7002              # 应用端口
  servlet:
    context-path: /       # 上下文路径
```

#### 2. AI 模型配置

```yaml
ai:
  dashscope:
    enabled: true
    api-key: ${QWEN_API_KEY}
    chat:
      options:
        model: qwen3-max          # AI 模型
        temperature: 0.7          # 温度参数
```

#### 3. 文件上传配置

```yaml
spring:
  servlet:
    multipart:
      max-file-size: 50MB         # 单文件最大大小
      max-request-size: 100MB     # 请求最大大小
```

#### 4. 应用配置

```yaml
app:
  baseUrl: http://localhost:7002  # 应用基础 URL
  
  translation:
    supported-languages: [...]    # 支持的语言列表
    
  membership:                     # 会员配置
  points:                         # 积分配置
```

### 环境变量

推荐使用环境变量管理敏感信息：

```bash
# Linux/Mac
export QWEN_API_KEY="your_api_key"
export ALIYUN_ACCESS_KEY_ID="your_access_key_id"
export ALIYUN_ACCESS_KEY_SECRET="your_access_key_secret"
export APP_BASE_URL="http://your-domain.com"

# Windows
set QWEN_API_KEY=your_api_key
set ALIYUN_ACCESS_KEY_ID=your_access_key_id
set ALIYUN_ACCESS_KEY_SECRET=your_access_key_secret
set APP_BASE_URL=http://your-domain.com
```

---

## 📁 项目结构

```
translation-ai-agent/
├── database/                          # 数据库相关
│   ├── 01_create_tables.sql          # 建表脚本
│   ├── 02_init_data.sql              # 初始化数据
│   ├── 03_create_indexes.sql         # 索引优化
│   └── PROJECT_SUMMARY.md            # 数据库设计文档
├── src/
│   ├── main/
│   │   ├── java/cn/net/susan/ai/translation/
│   │   │   ├── config/               # 配置类
│   │   │   │   ├── AliyunTranslationConfig.java
│   │   │   │   ├── AsyncConfig.java
│   │   │   │   ├── DashscopeProperties.java
│   │   │   │   ├── MinioConfig.java
│   │   │   │   ├── RedisConfig.java
│   │   │   │   └── WebSocketConfig.java
│   │   │   ├── controller/           # 控制器
│   │   │   │   ├── AuthController.java
│   │   │   │   ├── ChatTranslationController.java
│   │   │   │   ├── DocumentTranslationController.java
│   │   │   │   ├── MembershipController.java
│   │   │   │   ├── OrderPaymentController.java
│   │   │   │   └── TranslationController.java
│   │   │   ├── converter/            # 数据转换器
│   │   │   ├── dto/                  # 数据传输对象
│   │   │   ├── entity/               # 实体类
│   │   │   ├── enums/                # 枚举类型
│   │   │   ├── exception/            # 异常处理
│   │   │   ├── filter/               # 过滤器
│   │   │   ├── handler/              # 全局异常处理器
│   │   │   ├── mq/                   # 消息队列
│   │   │   ├── payment/              # 支付模块
│   │   │   ├── repository/           # 数据访问层
│   │   │   ├── security/             # 安全模块
│   │   │   ├── service/              # 业务逻辑层
│   │   │   ├── util/                 # 工具类
│   │   │   └── TranslationAiAgentApplication.java
│   │   └── resources/
│   │       ├── static/               # 静态资源
│   │       ├── templates/            # Thymeleaf 模板
│   │       │   ├── layout/           # 布局模板
│   │       │   ├── fragments/        # 片段模板
│   │       │   ├── index.html        # 首页
│   │       │   ├── translate.html    # 翻译页
│   │       │   ├── chat.html         # 对话翻译页
│   │       │   ├── document.html     # 文档翻译页
│   │       │   ├── history.html      # 历史记录页
│   │       │   ├── membership.html   # 会员页
│   │       │   └── ...
│   │       └── application.yml       # 应用配置
│   └── test/                         # 测试代码
├── pom.xml                           # Maven 配置
└── README.md                         # 项目文档
```

---

## 📚 API 文档

### RESTful API

#### 认证接口

```http
POST /api/auth/login
Content-Type: application/json

{
  "username": "user@example.com",
  "password": "password123"
}

Response:
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {...}
}
```

#### 文本翻译接口

```http
POST /api/translation/translate
Content-Type: application/json
Authorization: Bearer {token}

{
  "sourceText": "Hello, World!",
  "sourceLang": "en",
  "targetLang": "zh",
  "terminologyId": 1
}

Response:
{
  "translatedText": "你好，世界！",
  "confidence": 0.95,
  "usedPoints": 1
}
```

#### 文档翻译接口

```http
POST /api/document/upload
Content-Type: multipart/form-data
Authorization: Bearer {token}

file: [binary]
sourceLang: en
targetLang: zh

Response:
{
  "documentId": "doc_123456",
  "status": "processing",
  "progress": 0
}
```

#### 对话翻译接口

```http
POST /api/chat/translate
Content-Type: application/json
Authorization: Bearer {token}

{
  "message": "How are you?",
  "sessionId": "session_123",
  "targetLang": "zh"
}

Response:
{
  "translatedMessage": "你好吗？",
  "conversationContext": [...]
}
```

### WebSocket 接口

```javascript
// 连接 WebSocket
const ws = new WebSocket('ws://localhost:7002/ws/notifications');

// 订阅消息
ws.onmessage = (event) => {
  const notification = JSON.parse(event.data);
  console.log('收到通知:', notification);
};
```

详细的 API 文档请参考：`docs/API.md`

---

## 💾 数据库设计

### 核心表结构

| 表名 | 说明 | 主要字段 |
|------|------|----------|
| **users** | 用户表 | id, username, email, password, role, membership_level |
| **user_settings** | 用户配置 | user_id, theme, language, notifications_enabled |
| **translation_records** | 翻译记录 | id, user_id, source_text, translated_text, source_lang, target_lang |
| **chat_sessions** | 聊天会话 | id, user_id, title, created_at, updated_at |
| **chat_messages** | 聊天消息 | session_id, message, translation, role |
| **document_translations** | 文档翻译 | id, user_id, file_path, status, progress |
| **terminology_entries** | 术语条目 | id, category_id, source_term, target_term, language_pair |
| **quality_assessments** | 质量评估 | translation_id, rating, feedback, assessed_by |
| **membership_plans** | 会员计划 | id, name, price, duration, benefits |
| **orders** | 订单表 | id, user_id, amount, status, payment_method |
| **usage_statistics** | 使用统计 | user_id, date, translation_count, word_count |

详细的数据库设计文档请查看：
- [`database/PROJECT_SUMMARY.md`](database/PROJECT_SUMMARY.md) - 数据库设计总结
- [`database/01_create_tables.sql`](database/01_create_tables.sql) - 建表脚本

---

## 🌐 部署指南

### Docker 部署（推荐）

#### 1. 构建 Docker 镜像

```dockerfile
FROM eclipse-temurin:21-jdk-alpine
WORKDIR /app
COPY target/translation-ai-agent-1.0.0.jar app.jar
EXPOSE 7002
ENTRYPOINT ["java","-jar","app.jar"]
```

```bash
docker build -t translation-ai-agent:1.0.0 .
```

#### 2. Docker Compose 部署

创建 `docker-compose.yml`:

```yaml
version: '3.8'

services:
  app:
    image: translation-ai-agent:1.0.0
    ports:
      - "7002:7002"
    environment:
      - SPRING_PROFILES_ACTIVE=prod
      - DB_HOST=mysql
      - REDIS_HOST=redis
      - ES_HOST=elasticsearch
      - MINIO_ENDPOINT=minio:9000
    depends_on:
      - mysql
      - redis
      - elasticsearch
      - minio
  
  mysql:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: your_password
      MYSQL_DATABASE: translation
    volumes:
      - mysql_data:/var/lib/mysql
  
  redis:
    image: redis:7-alpine
    command: redis-server --requirepass your_password
    volumes:
      - redis_data:/data
  
  elasticsearch:
    image: elasticsearch:7.17.0
    environment:
      - discovery.type=single-node
      - ES_JAVA_OPTS=-Xms512m -Xmx512m
    volumes:
      - es_data:/usr/share/elasticsearch/data
  
  minio:
    image: minio/minio
    command: server /data
    environment:
      MINIO_ROOT_USER: your_access_key
      MINIO_ROOT_PASSWORD: your_secret_key
    volumes:
      - minio_data:/data

volumes:
  mysql_data:
  redis_data:
  es_data:
  minio_data:
```

启动服务：

```bash
docker-compose up -d
```

### 生产环境部署

#### 1. Nginx 反向代理配置

```nginx
server {
    listen 80;
    server_name your-domain.com;
    
    location / {
        proxy_pass http://localhost:7002;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
    
    location /ws {
        proxy_pass http://localhost:7002;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}
```

#### 2. HTTPS 配置

```bash
# 使用 Let's Encrypt 获取 SSL 证书
sudo certbot --nginx -d your-domain.com
```

---

## 👨‍💻 开发指南

### 本地开发环境搭建

#### 1. IDE 配置

推荐使用 IntelliJ IDEA：
1. 导入 Maven 项目
2. 配置 JDK 21
3. 安装 Lombok 插件
4. 配置代码格式化模板

#### 2. 数据库初始化

```bash
# 创建数据库
mysql -u root -p -e "CREATE DATABASE translation DEFAULT CHARACTER SET utf8mb4;"

# 执行初始化脚本
mysql -u root -p translation < database/01_create_tables.sql
mysql -u root -p translation < database/02_init_data.sql
mysql -u root -p translation < database/03_create_indexes.sql
```

#### 3. 启动开发服务

```bash
# 启动 Redis
redis-server

# 启动 Elasticsearch
elasticsearch

# 启动 MinIO
minio server ./data
```

### 代码规范

#### 命名规范

- **类名**: 大驼峰命名 (PascalCase)，如 `TranslationController`
- **方法名**: 小驼峰命名 (camelCase)，如 `translateText`
- **变量名**: 小驼峰命名，如 `userId`
- **常量名**: 全大写，下划线分隔，如 `MAX_RETRY_COUNT`
- **包名**: 全小写，点号分隔，如 `cn.net.susan.ai.translation`

#### 注释规范

```java
/**
 * 文本翻译服务类
 * 
 * 提供基于 AI 模型的文本翻译功能
 * 支持术语库匹配和上下文理解
 * 
 * @author 苏三
 * @version 1.0.0
 */
@Service
public class TranslationService {
    
    /**
     * 翻译文本
     * 
     * @param sourceText 源文本
     * @param sourceLang 源语言
     * @param targetLang 目标语言
     * @return 翻译结果
     */
    public String translate(String sourceText, String sourceLang, String targetLang) {
        // ...
    }
}
```

### 测试

#### 运行单元测试

```bash
mvn test
```

#### 运行集成测试

```bash
mvn verify
```

#### 代码覆盖率

```bash
mvn clean test jacoco:report
```

### 构建打包

```bash
# 清理并打包
mvn clean package

# 跳过测试打包
mvn clean package -DskipTests

# 生产环境打包
mvn clean package -Pprod
```

---

## ❓ 常见问题

### 1. 启动失败：数据库连接错误

**问题**: `Could not open JDBC Connection for transaction`

**解决方案**:
- 检查 MySQL 服务是否启动
- 验证数据库用户名密码是否正确
- 确认数据库 `translation` 已创建
- 检查网络连接和防火墙设置

### 2. Redis 连接超时

**问题**: `Unable to connect to Redis`

**解决方案**:
```bash
# 检查 Redis 服务
redis-cli ping

# 如果返回 PONG 则正常，否则重启 Redis
redis-server

# 检查配置文件中的 Redis 密码
```

### 3. AI API 调用失败

**问题**: `Invalid API key` 或 `Quota exceeded`

**解决方案**:
- 检查环境变量 `QWEN_API_KEY` 是否配置
- 登录阿里云控制台验证 API Key 有效性
- 检查账户余额和配额

### 4. 文件上传失败

**问题**: `File size exceeds limit`

**解决方案**:
- 修改 `application.yml` 中的文件大小限制
- 检查 MinIO 服务状态
- 验证桶权限配置

### 5. WebSocket 连接断开

**问题**: WebSocket 连接后立即断开

**解决方案**:
- 检查 Nginx WebSocket 代理配置
- 验证防火墙是否允许 WebSocket 连接
- 查看浏览器控制台错误信息

更多问题请查看 [Issues](https://github.com/yourusername/translation-ai-agent/issues)

---

## 🤝 贡献指南

我们欢迎各种形式的贡献！

### 如何贡献

1. Fork 本项目
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 创建 Pull Request

### 开发流程

```bash
# 1. 克隆项目
git clone https://github.com/yourusername/translation-ai-agent.git

# 2. 创建开发分支
git checkout -b feature/your-feature

# 3. 开发并测试
# ... coding ...

# 4. 提交代码
git add .
git commit -m "feat: add new translation feature"

# 5. 推送分支
git push origin feature/your-feature

# 6. 创建 Pull Request
```

### 提交信息规范

遵循 [Conventional Commits](https://www.conventionalcommits.org/) 规范：

- `feat`: 新功能
- `fix`: 修复 bug
- `docs`: 文档更新
- `style`: 代码格式调整
- `refactor`: 重构代码
- `test`: 测试相关
- `chore`: 构建/工具链相关

示例：
```bash
feat(translator): add terminology support for document translation
fix(api): resolve null pointer exception in chat translation
docs(readme): update installation guide
```

---

## 📄 许可证

本项目采用 MIT 许可证开源 - 查看 [LICENSE](LICENSE) 文件了解详情。

---

## 👥 团队

- **开发者**: 苏三
- **联系**: susan@example.com
- **项目地址**: https://github.com/yourusername/translation-ai-agent

---

## 🙏 致谢

感谢以下开源项目：

- [Spring Boot](https://spring.io/projects/spring-boot)
- [Spring AI](https://spring.io/projects/spring-ai)
- [通义千问](https://www.aliyun.com/product/dashscope)
- [阿里云翻译](https://www.aliyun.com/product/mt)
- [MinIO](https://min.io/)
- [Redis](https://redis.io/)
- [Elasticsearch](https://www.elastic.co/elasticsearch)

---

## 📞 联系方式

如有问题或建议，请通过以下方式联系我们：

- **Email**: susan@example.com
- **Issues**: [GitHub Issues](https://github.com/yourusername/translation-ai-agent/issues)
- **Discussions**: [GitHub Discussions](https://github.com/yourusername/translation-ai-agent/discussions)

---

<div align="center">

**⭐ 如果这个项目对你有帮助，请给一个 Star 支持一下！⭐**

Made with ❤️ by 苏三 | Powered by Spring AI

</div>
