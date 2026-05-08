# 企业RAG知识库客服 — Planner 文档

---

## 1. 项目目标（一句话总结）

构建一个融合 RAG 知识库管理与多 Agent 智能客服的企业级系统，支持多格式文档自动解析→向量化存储→语义检索→大模型精准问答，并通过企业微信渠道提供 7×24 自动化客户服务。

---

## 2. 需求拆解（P0/P1/P2 核心功能模块）

### P0 — MVP 核心流程（必须上线）

| 模块 | 功能 | 说明 |
|------|------|------|
| 文档管理 | 多格式文档上传与解析 | PDF / Office / Markdown / TXT，自动转纯文本 + 结构化分段 |
| 文档管理 | 索引管理 | 三种模式：全量刷新 / 增量回填 / 实时监听（文件系统 watch） |
| 向量检索 | Embedding + Milvus 存储 | 文档切片 → Embedding → 存入 Milvus 向量库 |
| 检索增强 | Reranker 精排 | 对初筛结果进行语义重排序，提升 top-k 准确率 |
| 问答引擎 | LLM 生成回答 | 基于检索上下文 + Prompt 模板，生成带引用的回答 |
| 渠道接入 | 企业微信客服接入 | 支持企微消息收发，自动回复 |
| Agent 引擎 | 意图检测 + 主对话图 | LangGraph 主图，识别用户意图并路由到子图或 RAG |

### P1 — 扩展能力（第 2-3 阶段上线）

| 模块 | 功能 | 说明 |
|------|------|------|
| 多 Agent 子图 | 6 个子图场景 | 订单查询、退换货、物流追踪、知识百科、人工转接、闲聊 |
| 结构化输出 | SagtBaseModel | Agent 层 Pydantic 模型约束输出格式，便于前端渲染 |
| 知识库管理 | 知识分类 + 权限 | 多级目录、部门隔离、版本管理 |
| 人工转接 | L0→L1→L2 三级转接 | 机器人无法回答时转人工，保留对话上下文 |
| 对话历史 | 持久化存储与检索 | 用户历史会话可回溯、可分析 |
| 反馈机制 | 点赞/点踩 + 人工修正 | 用户反馈用于 Prompt 优化和索引质量评估 |

### P2 — 远期规划（第 4 阶段及以后）

| 模块 | 功能 | 说明 |
|------|------|------|
| 企业微信侧边栏 | 内嵌客服面板 | 企微聊天窗口右侧展示知识库 / 对话记录 / 快捷回复 |
| BI 数据分析 | 对话漏斗 + 热点统计 | 意图分布、TOP 问题、解决率趋势、Agent 使用率 |
| 模型微调 | LoRA 领域微调 | 针对高频问题场景做轻量微调，降低幻觉率 |
| 多语言 | 英文 / 国际化 | 知识库多语种索引，客服多语言应答 |
| 开放 API | REST / WebSocket | 第三方系统接入（CRM / ERP / 工单系统） |
| 企业微信机器人 | 群聊模式 | 支持在企业微信群中 @机器人 问答 |

---

## 3. 技术选型

### 前端

| 技术 | 选型 | 理由 |
|------|------|------|
| 框架 | React 18 + TypeScript | 生态成熟、招聘市场通用、Ant Design 组件库丰富 |
| UI 组件库 | Ant Design Pro | 企业级后台开箱即用，表格/表单/布局完善 |
| 状态管理 | Zustand | 轻量、TS 友好、无 boilerplate |
| 构建工具 | Vite | HMR 极快，开发体验好 |
| 图表 | ECharts / AntV | BI 数据可视化 |
| 企微 SDK | 企业微信 JS-SDK | 侧边栏、消息推送 |

### 后端

| 技术 | 选型 | 理由 |
|------|------|------|
| 框架 | Python FastAPI | 异步高性能、自动 OpenAPI 文档、与 LangChain/LangGraph 生态无缝对接 |
| 应用层 | LangGraph + LangChain | 多 Agent 编排、Prompt 管理、Chain 复用 |
| 结构化输出 | Pydantic v2 | SagtBaseModel 继承 Pydantic，类型安全 + 自动校验 |
| 文档解析 | python-magic + pdfplumber + python-docx + markdown-it | 覆盖 PDF/Office/MD 格式 |
| 任务队列 | Celery + Redis | 异步文档处理、批量 Embedding 任务 |
| 文件存储 | MinIO (S3 兼容) | 文档原件 + 切片结果存储 |

### 数据库与向量存储

| 技术 | 选型 | 理由 |
|------|------|------|
| 向量数据库 | Milvus (pymilvus) | 企业级向量检索、10 亿级规模、高可用 |
| 关系数据库 | PostgreSQL + pgvector | 元数据存储 + 轻量向量查询备选 |
| 缓存 | Redis | 会话缓存、LLM 响应缓存、限流计数器 |
| 全文搜索 | Elasticsearch (可选) | 关键词混合检索，配合向量检索做 hybrid search |

### Embedding & LLM

| 技术 | 选型 | 理由 |
|------|------|------|
| Embedding 模型 | BAAI/bge-large-zh-v1.5 (本地) 或 通义千问 Embedding API | 中文效果好，支持本地部署 |
| Reranker | BAAI/bge-reranker-large | 精排阶段使用，提升准确率 |
| LLM | 通义千问 qwen-max / DeepSeek V3 | 性价比高，中文能力强；支持阿里云/火山引擎部署 |
| LLM 网关 | LiteLLM | 统一 OpenAI API 格式，支持多模型切换 Fallback |

### 部署与云服务

| 技术 | 选型 |
|------|------|
| 容器化 | Docker + Docker Compose |
| 编排（生产） | Kubernetes (K8s) |
| CI/CD | GitHub Actions |
| 云服务 | 阿里云 ACK / 华为云 CCE / 自建机房 |
| 企业微信 | 企业微信自建应用 + 客服消息 API |

---

## 4. AI/RAG 判断

### 是否需要 LoRA 微调？
- **现阶段：不需要**
- 理由：RAG 系统已通过检索上下文约束 LLM 知识范围，多数场景不需要微调。P2 阶段若发现特定领域（如保险条款、医疗诊断）的准确性不足，可对基座模型做 LoRA 微调。前期重点放在**检索召回率**和**Prompt 工程**上。

### 是否需要 RAG？
- **是，这是项目核心**
- RAG 是知识库问答的根基。文档 → 切片 → Embedding → 向量检索 → Reranker → LLM 生成的管线是必选项。Mildoc 已验证了三种索引模式的有效性。

### 是否需要向量数据库？
- **是，Milvus**
- 文档量从初期千级到后期亿级，Milvus 是唯一支持业务平滑扩展的向量库。pgvector 可在 MVP 阶段作为轻量替代，但生产必须上 Milvus。

### 是否需要多 Agent 架构？
- **是，LangGraph 多 Agent**
- Sagt 的 1 主图 + 6 子图架构为复杂客服场景提供了清晰的解耦方案。意图检测 Agent → 路由到具体子图 → 结构化输出，比单 Chain 方案更可控、可观测、可调试。

### 是否需要 Reranker？
- **是**
- 向量检索初筛后，BGE Reranker 能将 top-30 精排到 top-5，显著提升最终回答质量，降低幻觉率。

---

## 5. 为什么这样选

### 开发速度
- FastAPI + LangChain + LangGraph：Python 技术栈，团队上手快，快速搭建原型
- Ant Design Pro：后台管理页面开箱即用，减少前端工作量
- Docker Compose：本地一键启动所有依赖（Milvus / Redis / PostgreSQL / MinIO）

### 成本
- 开源为主（Milvus / MinIO / PostgreSQL / BGE Embedding），仅在 LLM API 上产生 Token 费用
- MVP 阶段可复用通义千问免费额度，上线后按量计费
- 自建 Milvus 集群比云向量数据库便宜 50%+（超过 1000 万向量规模时）

### 可维护性
- LangGraph 有向图可视化，Agent 链路清晰可见
- Pydantic 结构化输出，前后端契约明确，减少联调 Bug
- Celery 异步队列，文档处理不阻塞 API 响应

### 扩展性
- 多 Agent 解耦，新增子图不影响主图
- Milvus 水平扩展，支持分片 + 副本
- LiteLLM 统一网关，切换模型零改动

### 招聘市场通用性
- React + FastAPI + PostgreSQL 是最通用的全栈组合
- LangChain/LangGraph 是国内 AI 应用开发的核心技能
- Milvus 经验在 AI 时代是加分项

---

## 6. 项目结构

```
corp-rag-cs/
├── backend/
│   ├── app/
│   │   ├── main.py                  # FastAPI 入口
│   │   ├── config.py                # 配置中心（环境变量 + yaml）
│   │   ├── api/
│   │   │   ├── v1/
│   │   │   │   ├── __init__.py
│   │   │   │   ├── document.py      # 文档 CRUD API
│   │   │   │   ├── knowledge.py     # 知识库管理 API
│   │   │   │   ├── chat.py          # 对话 API
│   │   │   │   ├── agent.py         # Agent 调试/监控 API
│   │   │   │   └── wecom.py         # 企业微信回调 API
│   │   ├── core/
│   │   │   ├── document_parser.py   # 文档解析（PDF/Office/MD）
│   │   │   ├── chunker.py           # 文本切片策略
│   │   │   ├── embedding.py         # Embedding 调用封装
│   │   │   ├── retriever.py         # 检索器（向量 + 关键词）
│   │   │   ├── reranker.py          # BGE Reranker
│   │   │   └── indexer.py           # 索引管理（三种模式）
│   │   ├── agent/
│   │   │   ├── graph.py             # LangGraph 主图定义
│   │   │   ├── state.py             # Agent 状态定义（SagtBaseModel）
│   │   │   ├── intent.py            # 意图检测 Agent
│   │   │   ├── subgraphs/
│   │   │   │   ├── order.py         # 订单查询子图
│   │   │   │   ├── return_exchange.py # 退换货子图
│   │   │   │   ├── logistics.py     # 物流追踪子图
│   │   │   │   ├── knowledge.py     # 知识百科子图
│   │   │   │   ├── transfer.py      # 人工转接子图
│   │   │   │   └── smalltalk.py     # 闲聊子图
│   │   │   └── tools/
│   │   │       ├── rag_tool.py      # RAG 检索工具
│   │   │       ├── weather_tool.py  # 天气查询工具（示例）
│   │   │       └── ...              # 更多工具
│   │   ├── schemas/                 # Pydantic 模型（SagtBaseModel）
│   │   │   ├── document.py
│   │   │   ├── chat.py
│   │   │   └── agent.py
│   │   ├── models/                  # SQLAlchemy ORM 模型
│   │   │   ├── document.py
│   │   │   ├── knowledge_base.py
│   │   │   └── conversation.py
│   │   ├── services/
│   │   │   ├── wecom.py             # 企业微信消息服务
│   │   │   └── llm_gateway.py       # LiteLLM 封装
│   │   └── tasks/                   # Celery 异步任务
│   │       ├── document_processing.py
│   │       └── embedding_batch.py
│   ├── tests/
│   ├── alembic/                     # 数据库迁移
│   ├── Dockerfile
│   ├── requirements.txt
│   └── pyproject.toml
├── frontend/
│   ├── src/
│   │   ├── pages/
│   │   │   ├── Dashboard/           # 总览面板
│   │   │   ├── KnowledgeBase/       # 知识库管理
│   │   │   ├── Documents/           # 文档管理
│   │   │   ├── ChatDebug/           # 对话调试
│   │   │   ├── AgentMonitor/        # Agent 监控
│   │   │   ├── Settings/            # 系统设置
│   │   │   └── Wecom/               # 企微配置
│   │   ├── components/              # 通用组件
│   │   ├── hooks/                   # 自定义 Hooks
│   │   ├── services/                # API 请求封装
│   │   ├── store/                   # Zustand store
│   │   └── utils/                   # 工具函数
│   ├── Dockerfile
│   └── package.json
├── infra/
│   ├── docker-compose.yml           # 本地开发编排
│   ├── docker-compose.prod.yml      # 生产编排
│   ├── k8s/                         # Kubernetes 配置
│   │   ├── backend-deployment.yaml
│   │   ├── milvus-cluster.yaml
│   │   └── ...
│   ├── nginx/                       # Nginx 配置
│   └── prometheus/                  # 监控配置
├── scripts/
│   ├── init_milvus.py               # 初始化 Milvus collection
│   ├── seed_data.py                 # 种子数据
│   └── start.sh                     # 启动脚本
├── .github/
│   └── workflows/
│       ├── ci.yml                   # CI 流水线
│       └── cd.yml                   # CD 流水线
├── docs/
│   ├── planner.md
│   ├── prd.md
│   ├── api.md
│   └── deployment.md
└── README.md
```

---

## 7. 开发里程碑（Week 1~8）

### Week 1 — 基础设施搭建
- [ ] 初始化项目仓库、目录结构
- [ ] Docker Compose 编排（PostgreSQL + Redis + Milvus + MinIO）
- [ ] FastAPI 骨架 + 配置中心
- [ ] React + Ant Design Pro 脚手架
- [ ] 数据库表创建（Alembic 迁移）

### Week 2 — 文档处理管线
- [ ] 文档解析模块（PDF/Office/MD 上传 + 解析）
- [ ] 切片策略（固定长度 / 语义切分 / Markdown 标题分割）
- [ ] Embedding 封装 + Milvus 写入
- [ ] 索引管理（全量刷新 + 增量回填）
- [ ] 文件上传 API + 前端上传页面

### Week 3 — 向量检索 + Reranker
- [ ] Milvus 检索（基础向量检索）
- [ ] BGE Reranker 集成（精排 top-k）
- [ ] 混合检索（向量 + Elasticsearch 关键词）
- [ ] 检索 API + 前端知识库预览页面

### Week 4 — RAG 问答引擎
- [ ] LLM 网关集成（LiteLLM + 通义千问）
- [ ] Prompt 模板设计与上下文组装
- [ ] 带引用的回答生成
- [ ] 对话 API + 前端聊天调试窗口

### Week 5 — 多 Agent 主图
- [ ] LangGraph 主图构建（意图检测 → 路由）
- [ ] 意图识别 Prompt + 校验
- [ ] Agent State 定义（SagtBaseModel）
- [ ] 知识百科子图 + RAG 工具节点
- [ ] 人工转接子图（L0→L1→L2）

### Week 6 — 子图扩展 + 企微集成
- [ ] 订单查询子图
- [ ] 退换货子图
- [ ] 物流追踪子图
- [ ] 闲聊子图
- [ ] 企业微信自建应用配置 + 消息回调
- [ ] 企微消息 → Agent 引擎对接

### Week 7 — 前端完善 + 结构化输出
- [ ] 对话记录与历史回溯页面
- [ ] Agent 监控面板（节点执行可视化）
- [ ] 知识库管理页面（分类、权限）
- [ ] 结构化输出渲染（卡片、按钮）
- [ ] 反馈机制（点赞/点踩/人工修正）

### Week 8 — 测试、优化、部署
- [ ] 单元测试 + 集成测试（覆盖率 > 70%）
- [ ] 性能压测（QPS、P99 延迟）
- [ ] 安全扫描 + XSS/CSRF 防护
- [ ] CI/CD 流水线配置
- [ ] K8s 部署 + Nginx + HTTPS
- [ ] 文档完善 + 上线

---

## 8. 风险提示

### 技术债
- **Milvus 运维复杂度**：Milvus 依赖 etcd + MinIO + Pulsar 三个组件，初期用 Docker Compose 启动简单，但生产 K8s 运维需要专人。考虑使用 Zilliz Cloud 托管版降低运维成本。
- **LangGraph 版本不稳定**：LangChain/LangGraph 迭代快，API 可能 breaking change。锁定依赖版本，定期升级测试。
- **文档解析质量**：PDF 表格 / 复杂排版解析准确率低。需要建立文档解析质量评估机制，必要时引入 OCR（PaddleOCR）。

### 性能瓶颈
- **Embedding 吞吐**：大量文档导入时，CPU Embedding 慢。建议 GPU 部署 Embedding 模型（NVIDIA T4 及以上）。
- **LLM 延迟**：大模型推理延迟在 1-5s 之间。用 Redis 缓存高频问题，流式输出改善体验。
- **Milvus 查询热点**：高并发场景下，需增加 Milvus 副本 + 读写分离。

### 安全问题
- **Prompt 注入**：用户问题可能构造对抗性 Prompt 绕过限制。需要输入过滤 + 输出校验。
- **企业微信 Token 泄露**：企微 Token 应存入 Vault / K8s Secret，不允许出现在代码或日志中。
- **文档权限越权**：知识库需要细粒度 RBAC 权限控制，防止跨部门访问。

### AI 幻觉
- LLM 可能生成看似合理但错误的答案。通过 Reranker 提升检索质量、Prompt 约束"不知道就说不知道"、引用标注等方式降低幻觉。

---

## 9. CI/CD 设计

### CI（GitHub Actions）

```yaml
name: CI

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Backend lint
        run: ruff check backend/ && mypy backend/
      - name: Frontend lint
        run: cd frontend && npx eslint src/ && npx prettier --check src/

  test:
    runs-on: ubuntu-latest
    services:
      postgres:
        image: postgres:16
        env: { POSTGRES_PASSWORD: test }
      redis:
        image: redis:7
    steps:
      - uses: actions/checkout@v4
      - name: Install dependencies
        run: pip install -r backend/requirements.txt
      - name: Run tests
        run: cd backend && pytest --cov=app --cov-report=xml -v
      - name: Upload coverage
        uses: codecov/codecov-action@v3

  build:
    runs-on: ubuntu-latest
    needs: [lint, test]
    steps:
      - uses: actions/checkout@v4
      - name: Build Docker images
        run: |
          docker build -t corp-rag-cs-backend:latest -f backend/Dockerfile .
          docker build -t corp-rag-cs-frontend:latest -f frontend/Dockerfile .
```

### CD（GitHub Actions + ArgoCD / 手动触发）

```yaml
name: CD

on:
  push:
    tags: ['v*']

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Login to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}
      - name: Push images
        run: |
          docker push ghcr.io/org/corp-rag-cs-backend:${{ github.ref_name }}
          docker push ghcr.io/org/corp-rag-cs-frontend:${{ github.ref_name }}
      - name: Deploy to K8s
        run: |
          kubectl set image deployment/backend app=ghcr.io/org/corp-rag-cs-backend:${{ github.ref_name }}
          kubectl set image deployment/frontend app=ghcr.io/org/corp-rag-cs-frontend:${{ github.ref_name }}
```

---

## 10. 部署方案

### 本地开发环境
```
Docker Compose 一键启动：
  - FastAPI + Uvicorn (hot reload)
  - React + Vite (HMR proxy → backend)
  - PostgreSQL 16
  - Redis 7
  - Milvus Standalone
  - MinIO
```

### 测试/预发布环境
```
单机 Docker Compose + 生产配置
- 使用预发布 Milvus 集群
- 连接测试企业微信应用
- 启用监控（Prometheus + Grafana）
```

### 生产环境
```
┌─────────────────────────────────────────────┐
│  Load Balancer (ALB / Nginx)               │
│     ├── Frontend (React SPA, CDN 加速)      │
│     └── Backend API (FastAPI, 2-4 pods)     │
│                                               │
│  Milvus Cluster (3 nodes + etcd + Pulsar)   │
│  PostgreSQL + Pgvector (主从 + WAL)         │
│  Redis Cluster (3 nodes, 会话 + 缓存)       │
│  MinIO (对象存储, 3 nodes, erasure coding)  │
│  Celery Worker (2-4 pods, 异步任务)         │
│  LLM Gateway (LiteLLM → 通义千问 API)       │
│  Prometheus + Grafana (监控)                │
│  EFK / Loki (日志聚合)                      │
└─────────────────────────────────────────────┘
```

### 资源估算（初期 1000 文档 / 日活 500 客服对话）
- 后端 API：2 台 4C8G
- Milvus：3 台 8C16G + 500GB SSD
- PostgreSQL：1 台 4C8G + 200GB SSD
- Redis Cluster：3 台 2C4G
- MinIO：3 台 4C8G + 1TB HDD
- Celery Worker：2 台 4C8G
- 月成本估算：~6000-8000 元（阿里云按量）

---

## 11. 项目初始化命令

```bash
# 1. 克隆并进入项目
git clone git@github.com:org/corp-rag-cs.git
cd corp-rag-cs

# 2. 启动基础设施（PostgreSQL / Redis / Milvus / MinIO）
docker compose -f infra/docker-compose.yml up -d

# 3. 后端初始化
cd backend
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
cp .env.example .env   # 编辑配置
alembic upgrade head
python scripts/init_milvus.py
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000

# 4. 前端初始化
cd frontend
npm install
cp .env.example .env.local   # 编辑 API 地址
npm run dev

# 5. 启动 Celery Worker
cd backend
celery -A app.tasks worker --loglevel=info --concurrency=4

# 6. 启动文件监听
cd backend
python -m app.core.indexer --mode listen

# 浏览器访问
# 前端: http://localhost:5173
# 后端 API: http://localhost:8000/docs
# MinIO Console: http://localhost:9001
# Milvus Dashboard: http://localhost:9091/web
```
