# 企业RAG知识库客服 — Product PRD 文档

---

## 1. 产品概述

### 产品名称
**企业 RAG 知识库客服系统**（英文名：CorpRAG CS）

### 定位一句话
企业级 AI 智能客服平台，以 RAG 知识库为核心，通过多 Agent 架构为企业提供精准、可溯源、7×24 小时的自动化客户服务。

### 目标用户
| 用户角色 | 典型场景 |
|----------|----------|
| 企业客服主管 | 搭建客服机器人、管理知识库、监控服务质量 |
| 一线客服人员 | 使用 AI 辅助应答、转接复杂问题、查看历史记录 |
| 知识库管理员 | 上传/管理文档、审核切片质量、更新知识内容 |
| 企业 IT 管理员 | 配置企业微信集成、管理权限、维护系统 |
| 最终客户 | 通过企业微信咨询产品/服务问题，获得即时回答 |

### 核心痛点
1. **客服人力成本高**：大量重复问题消耗人工客服时间，企业需雇佣大量客服人员
2. **知识管理散乱**：产品手册、FAQ、政策文档分散在不同系统，客服查找效率低
3. **应答质量不稳定**：不同客服人员业务水平参差不齐，客户体验不一致
4. **响应延迟**：非工作时间无人应答，客户等待时间长
5. **培训成本高**：新客服需要数周学习企业知识库
6. **数据不沉淀**：客服对话中的问题和答案未被系统化利用

### 价值主张
> "将企业知识库转化为 24 小时在线、永不离职、回答一致且可溯源的 AI 客服专家。"

核心价值量化目标：
- 客服人力成本降低 **60%**（自动处理 80% 的重复性问题）
- 平均首次响应时间从 **5 分钟降至 5 秒**
- 客服服务质量一致性提升至 **95%**
- 新客服培训周期从 **2 周缩短至 2 天**

---

## 2. 市场调研

### 市场现状
- **中国智能客服市场 2025 年规模预计突破 100 亿元**，年复合增长率 22%
- 电商、金融、政务、医疗是最主要的需求行业
- 大模型 RAG 技术成熟使"知识库+问答"模式成为主流
- 企业微信是国内企业服务的主要入口（月活超 2 亿）

### 用户需求趋势
1. **从规则型 FAQ 到语义理解**：用户不再接受关键词匹配，期望自然语言交流
2. **从单轮对话到多轮任务**：简单问答不够，需要上下文感知的多轮对话
3. **从黑盒输出到可溯源**：用户期望 AI 回答附带引用来源
4. **从纯文本到富媒体**：答案需要图片、表格、操作指引等
5. **从独立系统到渠道融合**：企微、网页、App、公众号多端打通

### 机会点分析
- **中等规模企业服务空白**：头部企业用定制方案（年费 50 万+），小企业用标准 SaaS（年费 1 万），中间地带（年费 5-15 万）缺乏好产品
- **"私有知识 + 公域 LLM" 的 RAG 组合**比纯微调方案更灵活、更安全
- **多 Agent 架构区分度**：大多数竞品仍是单链 RAG，缺乏意图路由和子图任务编排
- **企业微信原生集成**：利用企微开放 API 做深度集成，而非简单转发

---

## 3. 竞品分析

### 竞品 1：阿里云客服（云小蜜 / 新零售智能助理）
| 维度 | 评价 |
|------|------|
| 优点 | 阿里云背书，电商场景成熟，支持多轮对话，自带 NLP 能力 |
| 缺点 | 成本高（年费 20 万+），知识库管理体验差，嵌入企业微信需额外开发 |
| 可借鉴 | 闲聊和问题兜底策略，渠道接入 SDK 设计 |
| 差异化机会 | **更灵活的 RAG 索引模式**、**更轻量的部署方案**、**更低的 TCO** |

### 竞品 2：Tidio / Zendesk Answer Bot
| 维度 | 评价 |
|------|------|
| 优点 | UX 设计出色，工单系统无缝协同，SaaS 开箱即用 |
| 缺点 | 海外产品，中文理解弱，数据存储海外不合规，价格按坐席高 |
| 可借鉴 | 对话历史管理面板、满意的量化指标设计 |
| 差异化机会 | **企业微信原生集成**、**中文 Embedding 优化**、**数据本地化** |

### 竞品 3：智齿科技（BotFactory / 客服机器人）
| 维度 | 评价 |
|------|------|
| 优点 | 国内客服市场头部，多渠道集成好，知识库管理成熟 |
| 缺点 | 传统 NLP 为主，大模型接入较晚，定制化能力有限，价格不透明 |
| 可借鉴 | 企业微信集成流程、人工转接机制、工单系统配合 |
| 差异化机会 | **多 Agent 架构 vs 传统规则引擎**、**开源可自建**、**RAG 检索更精准** |

### 竞品 4：Dify / FastGPT（开源 RAG 方案）
| 维度 | 评价 |
|------|------|
| 优点 | 开源免费，社区活跃，RAG 管线完整 |
| 缺点 | 缺乏多 Agent 能力，客服场景特性缺失（转接/意图路由/结构化输出），企微集成不完善 |
| 可借鉴 | 知识库管理的 UI 设计、文档解析流程 |
| 差异化机会 | **企业级多 Agent 客服编排**、**企业微信深度集成**、**商业支持和 SLA** |

### 差异化总结
| 对比维度 | 竞品 | 我们的优势 |
|----------|------|------------|
| 架构 | 单链 RAG / 规则引擎 | LangGraph 多 Agent（1主图+6子图） |
| 渠道 | 多渠道但浅层集成 | 企业微信深度集成（消息+侧边栏+群聊） |
| 部署 | 纯 SaaS / 纯私有化 | 灵活部署（SaaS + 私有化 + 混合） |
| 检索 | 简单向量检索 | 三种索引模式 + Reranker 精排 + 混合检索 |
| 定价 | 坐席制 / 高门槛 | 按文档量 + Token 用量，透明定价 |
| 开放性 | 封闭平台 | 开源核心 + 开放 API + 可自建 |

---

## 4. MVP 定义

### P0 — MVP 必须包含（第 1-6 周）

| 模块 | 功能 | 验收标准 |
|------|------|----------|
| 文档上传与解析 | 支持 PDF / DOCX / MD / TXT 上传 | 上传成功率 > 98%，解析准确率 > 90% |
| 文档切片与索引 | 自动切片 + Embedding + Milvus 写入 | 单文档处理 < 30s（100页以内） |
| 三种索引管理 | 全量刷新 / 增量回填 / 实时监听 | 增量更新不影响线上检索 |
| 向量检索 | Milvus ANN 检索，返回 top-30 | 检索 P99 < 200ms |
| Reranker 精排 | BGE Reranker，top-30→top-5 | 精排后 top-5 准确率 > 85% |
| RAG 问答 | 基于检索结果 + LLM 生成回答 | 回答准确率 > 80%（人工评估） |
| 意图检测 | 用户问题意图分类（客服场景 6 类） | 意图识别准确率 > 90% |
| 主对话图 | LangGraph 主图，意图→子图路由 | 端到端响应 P99 < 5s |
| 知识百科子图 | 基于 RAG 的知识问答 | 带引用来源 |
| 人工转接子图 | L0→L1→L2 三级转接 | 转接成功率 100%，上下文保留 |
| 企业微信集成 | 消息接收 + 自动回复 | 企微消息 10s 内响应 |
| 前端管理面板 | 文档管理 + 对话调试 + 基础设置 | 覆盖主要管理操作 |

### P1 — 第二阶段（第 7-10 周）

| 模块 | 功能 |
|------|------|
| 多 Agent 子图 | 订单查询、退换货、物流追踪、闲聊 |
| 结构化输出 | SagtBaseModel → 前端卡片/按钮渲染 |
| 对话历史管理 | 按用户/时间/意图检索历史 |
| 反馈机制 | 点赞/点踩/人工修正 |
| 知识库分类与权限 | RBAC 目录级权限控制 |
| 企业微信侧边栏 | 知识库面板内嵌 |

### P2 — 远期规划（第 11 周+）

| 模块 | 功能 |
|------|------|
| BI 数据看板 | 对话漏斗、解决率、热点统计 |
| LoRA 微调 | 针对特定领域微调 |
| 开放 API | REST + WebSocket 第三方集成 |
| 企业微信群机器人 | 群聊 @机器人 问答 |
| 多语言 | 英文支持 |

### 明确不做什么（MVP 范围边界）
- ❌ 不做工单系统（只用转接，不建工单）
- ❌ 不做电话客服/IVR
- ❌ 不做 CRM 集成（只留 API 接口）
- ❌ 不做模型训练平台
- ❌ 不做多租户管理（MVP 单租户，P2 加）

---

## 5. 功能详细设计

### 模块 1：文档管理与索引

#### 功能描述
用户通过管理后台上传文档（PDF/Office/MD/TXT），系统自动解析为纯文本，按策略切片，生成 Embedding 存入 Milvus，并通过三种索引模式保持知识库最新。

#### 用户价值
- "我在企微后台上传一份产品手册，AI 客服立刻就能用里面的知识回答客户问题"
- "更新了价格表，增量索引自动生效，无需手动重启系统"

#### 输入/输出
| 输入 | 输出 |
|------|------|
| PDF/DOCX/MD 文件 + 索引模式参数 | 切片列表 + Embedding 向量 + 存储状态 |
| 文件系统 watch 事件 | 增量更新的索引记录 |
| 手动触发全量刷新 | 全新的 Milvus collection + 索引 |

#### 关键逻辑
```
文档上传 → 格式检测 → 文本提取 → 切片（固定256/512tokens / 按Markdown标题 / 语义分割）
→ Embedding(bge-large-zh) → Milvus upsert → 更新元数据表
```

### 模块 2：向量检索与 Reranker 精排

#### 功能描述
用户问题 → Embedding 查询向量 → Milvus ANN 搜索（top-30）→ BGE Reranker 精排（top-5）→ 返回切片文本 + 相关性分数

#### 用户价值
- 相比纯向量检索，Reranker 将准确率从 70% 提升到 85%+
- 客户得到的答案更精准，减少"这个我不知道"的情况

#### 输入/输出
| 输入 | 输出 |
|------|------|
| 用户问题文本 | 精排后的 top-5 切片（含文本+来源文档+分数） |
| 可选的 filter（如部门筛选） | 按 metadata 过滤后的结果 |

#### 关键逻辑
```
query → embedding → Milvus.search(top_k=30) → 取结果 → reranker.rerank(query, candidates) → top_5
```

### 模块 3：RAG 问答引擎

#### 功能描述
基于检索到的 top-5 切片 + 对话历史 + Prompt 模板，调用 LLM 生成带引用的自然语言回答。

#### 用户价值
- 回答有据可查，客户和客服都信任 AI 的回答
- "如果不知道就说不知道"避免误导

#### 关键逻辑
```
System Prompt: "你是一个客服助手，基于以下知识片段回答问题。如果知识片段不足以回答，请说'根据现有知识无法回答'。请注明信息来源。"
User Message: 拼接 top-5 切片文本 + 用户问题
LLM 生成: 回答（带 [1][2] 引用标记）
```

### 模块 4：多 Agent 引擎（核心架构）

#### 功能描述
基于 LangGraph 的主图 + 子图架构，实现意图识别、任务路由、子图执行、结构化输出。

#### 用户价值
- 不同场景（查订单、退换货、咨询知识）由不同 Agent 专门处理，准确率更高
- 复杂任务可编排多个步骤（如"先查订单状态，再根据状态判断是否可退货"）

#### 关键逻辑
```
用户输入 → 主图入口节点
  → 意图检测节点 (LLM classify: order/return/logistics/knowledge/transfer/smalltalk)
    → order 子图 → 执行订单查询流程 → 结构化输出
    → return_exchange 子图 → 执行退换货流程 → 结构化输出
    → knowledge 子图 → 调用 RAG 工具 → 结构化输出
    → transfer 子图 → 转接人工客服
    → smalltalk 子图 → 闲聊处理
```

#### Agent State 定义（SagtBaseModel）
```python
class AgentState(SagtBaseModel):
    user_id: str
    session_id: str
    messages: list[dict]  # 对话历史
    intent: str | None     # 当前意图
    subgraph: str | None   # 当前子图
    context: list[dict]    # RAG 检索到的切片
    structured_output: dict | None  # 子图输出的结构化数据
    transfer_requested: bool = False
    feedback: dict | None
```

### 模块 5：企业微信集成

#### 功能描述
- 接收企业微信用户发送的消息 → 传给 Agent 引擎 → 返回回答
- 支持文本、图片（OCR）、小程序卡片等消息类型
- 企业微信侧边栏展示知识库搜索

#### 用户价值
- 客户在企微聊天中直接咨询，无需切换到其他平台
- 客服人员在企微侧边栏中实时搜索知识库，辅助应答

#### 关键逻辑
```
企微消息回调 → 解密 → 解析消息类型 → 调用 Agent 引擎
→ Agent 生成回答 → 组装企微消息格式 → 被动回复 / 主动推送
```

### 模块 6：人工转接

#### 功能描述
- L0（AI 自动应答）→ 无法回答或用户要求转人工 → L1（一线客服）→ 复杂问题 → L2（专家客服）
- 转接时保留完整对话上下文

#### 用户价值
- 复杂问题不会丢失上下文，无需客户重复描述
- 人工客服能看到 AI 已尝试的回答，避免重复劳动

---

## 6. 用户流程

### 流程 1：知识库管理员 — 首次上架知识库

```
1. 登录管理后台 → 进入"知识库管理"
2. 点击"新建知识库" → 输入名称、描述、所属部门
3. 进入"文档管理" → 上传文档（PDF 产品手册 / Word FAQ）
4. 系统自动解析 → 显示切片预览
5. 管理员检查切片质量 → 可手动调整切片边界
6. 点击"构建索引" → 选择"全量刷新"模式
7. 等待索引完成（状态: 绿色✔）
8. 进入"对话调试" → 输入测试问题 → 检查回答质量
9. 若满意 → 发布到线上 → 企微客服开始使用
```

### 流程 2：最终客户 — 通过企微咨询

```
1. 客户在企业微信中打开聊天窗口
2. 输入："请问物流怎么还没到？"
3. 企微消息 → 后端接收 → Agent 引擎
4. 意图检测 → "logistics" 意图
5. 物流追踪子图执行：
   a. 提取订单号（若无，反问客户）
   b. 查询物流系统 API
   c. 返回物流状态
6. 结构化输出 → 企微回复：
   "📦 您的订单 #ORD20240301 物流状态：快递已到达【北京分拣中心】，预计明天 18:00 前送达。查看详情：[点击查看物流]"
7. 对话结束 → 用户可点赞/点踩反馈
8. 若用户不满意 → 转接人工客服
```

### 流程 3：人工客服 — 处理转接

```
1. 客户连续 2 次点踩 → 触发转接
2. L0（AI）标记转接请求 → 推送到 L1 客服工作台
3. L1 客服打开对话窗口 → 看到完整对话历史 + AI 尝试的回答
4. 客服基于上下文继续回复
5. 若问题超出 L1 能力 → 标记并转接 L2 专家
6. 解决后关闭对话 → 对话记录入库
```

---

## 7. 页面结构设计

### 页面清单

| 页面 | 路由 | 目标用户 | 主要功能 |
|------|------|----------|----------|
| 总览面板 | `/dashboard` | 客服主管 | 核心指标卡片、趋势图、今日对话量/解决率/Top 问题 |
| 知识库管理 | `/knowledge` | 管理员 | 知识库列表、创建/编辑/删除、目录结构树 |
| 知识库详情 | `/knowledge/:id` | 管理员 | 文档列表、索引状态、切片预览、重新索引 |
| 文档管理 | `/documents` | 管理员 | 上传文档、解析状态、切片编辑、删除 |
| 文档详情 | `/documents/:id` | 管理员 | 文件预览、切片列表、切片文本编辑 |
| 对话调试 | `/chat` | 管理员/客服主管 | 模拟对话输入、查看 AI 回答与引用、重置对话 |
| Agent 监控 | `/agent` | 管理员/技术 | LangGraph 图可视化、节点执行轨迹、耗时分布 |
| 对话记录 | `/history` | 客服主管/客服 | 按时间/用户/意图筛选、查看/导出对话详情 |
| 企业微信配置 | `/settings/wecom` | IT 管理员 | 企微应用配置、Token 管理、回调地址 |
| 系统设置 | `/settings/system` | IT 管理员 | 模型选择、Prompt 编辑、Reranker 开关、权限管理 |
| 用户管理 | `/settings/users` | IT 管理员 | 角色管理、邀请成员、权限分配 |
| BI 分析 | `/analytics` (P2) | 客服主管 | 漏斗分析、热点词云、趋势报表 |

### 页面跳转关系

```
登录 (/login)
  └── 总览 (/dashboard) ← 所有页面均可返回
        ├── 知识库管理 (/knowledge)
        │     └── 知识库详情 (/knowledge/:id)
        │           └── 文档详情 (/documents/:id)
        ├── 文档管理 (/documents)
        │     └── 文档详情 (/documents/:id)
        ├── 对话调试 (/chat)
        ├── Agent 监控 (/agent)
        ├── 对话记录 (/history)
        └── 设置 (/settings)
              ├── 企业微信配置 (/settings/wecom)
              ├── 系统设置 (/settings/system)
              └── 用户管理 (/settings/users)
```

### HTML 原型描述（非代码，文字描述关键组件）

**页面骨架：**
```
┌─────────────────────────────────────────────────────────┐
│  Logo         总览  知识库  文档  对话  监控  设置  │ ← 顶部导航
├─────────────────────────────────────────────────────────┤
│                                                         │
│  侧边栏（上下文菜单）    主内容区                       │
│  ├ 知识库列表            [面包屑导航]                   │
│  ├ 最近文档              [页面核心功能]                 │
│  └ 操作入口              [数据表格/图表/表单]           │
│                                                         │
├─────────────────────────────────────────────────────────┤
│  底部状态: 系统运行中 | Milvus 正常 | LLM 连接正常   │ ← 状态栏
└─────────────────────────────────────────────────────────┘
```

**总览面板核心卡片：**
- 今日对话量（数字 + 趋势箭头）
- 自动解决率（百分比 + 环形图）
- 平均响应时间（毫秒）
- 等待转接数（数字 + 闪烁标记）
- 下方：近 7 天趋势折线图 + TOP 5 问题排行

**对话调试页面布局：**
```
┌──────────────────────────────────────────────────────────┐
│  左侧: Agent 面板                          右侧: 预览   │
│  ┌──────────────────────┐  ┌──────────────────────────┐ │
│  │ 用户输入框            │  │ 💬 AI 回答 + 引用标注    │ │
│  │ [测试问题] [发送]     │  │                          │ │
│  ├──────────────────────┤  │ 📄 参考文档切片1          │ │
│  │ 意图检测: logistics   │  │ 📄 参考文档切片2          │ │
│  │ 子图路径: main→intent │  │ 🔄 重新生成  👍  👎     │ │
│  │   →logistics→rag_tool │  └──────────────────────────┘ │
│  │ 执行耗时: 1.2s        │                               │
│  │ [查看图谱]            │                               │
│  └──────────────────────┘                               │
└──────────────────────────────────────────────────────────┘
```

---

## 8. 数据结构设计

### 核心表结构

#### 知识库表 (knowledge_bases)

```sql
CREATE TABLE knowledge_bases (
    id            UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name          VARCHAR(255) NOT NULL,
    description   TEXT,
    department    VARCHAR(100),       -- 所属部门
    milvus_collection VARCHAR(255),   -- 对应的 Milvus collection 名称
    status        VARCHAR(20) DEFAULT 'active',  -- active/inactive/deleted
    created_by    UUID NOT NULL REFERENCES users(id),
    created_at    TIMESTAMPTZ DEFAULT NOW(),
    updated_at    TIMESTAMPTZ DEFAULT NOW()
);
```

#### 文档表 (documents)

```sql
CREATE TABLE documents (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    kb_id           UUID NOT NULL REFERENCES knowledge_bases(id),
    filename        VARCHAR(500) NOT NULL,
    file_type       VARCHAR(20) NOT NULL,  -- pdf/docx/md/txt
    file_size       BIGINT,
    file_path       VARCHAR(1000),          -- MinIO 对象存储路径
    status          VARCHAR(20) DEFAULT 'pending', -- pending/parsing/ready/failed
    parsing_errors  TEXT,
    chunk_count     INTEGER DEFAULT 0,
    version         INTEGER DEFAULT 1,
    created_by      UUID REFERENCES users(id),
    created_at      TIMESTAMPTZ DEFAULT NOW(),
    updated_at      TIMESTAMPTZ DEFAULT NOW()
);
CREATE INDEX idx_documents_kb_id ON documents(kb_id);
CREATE INDEX idx_documents_status ON documents(status);
```

#### 文档切片表 (document_chunks)

```sql
CREATE TABLE document_chunks (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    document_id     UUID NOT NULL REFERENCES documents(id) ON DELETE CASCADE,
    kb_id           UUID NOT NULL REFERENCES knowledge_bases(id),
    chunk_index     INTEGER NOT NULL,       -- 切片顺序
    content         TEXT NOT NULL,           -- 切片文本
    content_hash    VARCHAR(64),             -- 用于增量去重
    token_count     INTEGER,
    metadata        JSONB DEFAULT '{}',      -- 来源页码/章节标题等
    milvus_id       VARCHAR(255),            -- Milvus 中的 ID
    created_at      TIMESTAMPTZ DEFAULT NOW()
);
CREATE INDEX idx_chunks_doc_id ON document_chunks(document_id);
CREATE INDEX idx_chunks_kb_id ON document_chunks(kb_id);
```

#### 对话会话表 (conversations)

```sql
CREATE TABLE conversations (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    session_id      VARCHAR(255) NOT NULL,   -- 企微消息会话 ID
    user_id         VARCHAR(255) NOT NULL,   -- 企业微信用户 ID
    user_name       VARCHAR(255),
    channel         VARCHAR(50) DEFAULT 'wecom',  -- wecom/web/api
    status          VARCHAR(20) DEFAULT 'active',  -- active/transferred/closed
    current_agent   VARCHAR(50),             -- 当前子图名称
    metadata        JSONB DEFAULT '{}',
    created_at      TIMESTAMPTZ DEFAULT NOW(),
    updated_at      TIMESTAMPTZ DEFAULT NOW()
);
CREATE INDEX idx_conv_session ON conversations(session_id);
CREATE INDEX idx_conv_user ON conversations(user_id);
CREATE INDEX idx_conv_status ON conversations(status);
```

#### 对话消息表 (messages)

```sql
CREATE TABLE messages (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    conversation_id UUID NOT NULL REFERENCES conversations(id) ON DELETE CASCADE,
    role            VARCHAR(20) NOT NULL,   -- user/assistant/agent/system
    content         TEXT NOT NULL,
    content_type    VARCHAR(20) DEFAULT 'text',  -- text/card/image
    intent          VARCHAR(50),            -- 检测到的意图
    agent_path      TEXT,                   -- 执行路径: main→intent→order
    structured_data JSONB,                  -- SagtBaseModel 结构化输出
    retrieved_chunks JSONB,                 -- RAG 检索到的切片
    llm_model       VARCHAR(100),
    latency_ms      INTEGER,                -- Agent 执行耗时
    tokens_used     INTEGER,
    feedback        VARCHAR(10),            -- like/dislike/null
    created_at      TIMESTAMPTZ DEFAULT NOW()
);
CREATE INDEX idx_msg_conv ON messages(conversation_id);
CREATE INDEX idx_msg_intent ON messages(intent);
CREATE INDEX idx_msg_feedback ON messages(feedback);
```

#### 用户反馈表 (feedback)

```sql
CREATE TABLE feedback (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    message_id      UUID NOT NULL REFERENCES messages(id),
    conversation_id UUID NOT NULL REFERENCES conversations(id),
    feedback_type   VARCHAR(10) NOT NULL,     -- like/dislike
    comment         TEXT,
    corrected_answer TEXT,                    -- 人工修正答案
    handled_by      UUID REFERENCES users(id),
    created_at      TIMESTAMPTZ DEFAULT NOW()
);
```

#### 索引日志表 (index_logs)

```sql
CREATE TABLE index_logs (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    kb_id           UUID NOT NULL REFERENCES knowledge_bases(id),
    mode            VARCHAR(20) NOT NULL,   -- full_refresh/backfill/listen
    status          VARCHAR(20) NOT NULL,   -- running/completed/failed
    total_docs      INTEGER DEFAULT 0,
    processed_docs  INTEGER DEFAULT 0,
    total_chunks    INTEGER DEFAULT 0,
    error_message   TEXT,
    started_at      TIMESTAMPTZ,
    finished_at     TIMESTAMPTZ,
    created_at      TIMESTAMPTZ DEFAULT NOW()
);
```

### Milvus Collection Schema

```python
from pymilvus import CollectionSchema, FieldSchema, DataType

schema = CollectionSchema([
    FieldSchema(name="id", dtype=DataType.VARCHAR, max_length=64, is_primary=True),
    FieldSchema(name="vector", dtype=DataType.FLOAT_VECTOR, dim=1024),  # bge-large-zh: 1024维
    FieldSchema(name="chunk_id", dtype=DataType.VARCHAR, max_length=64),
    FieldSchema(name="document_id", dtype=DataType.VARCHAR, max_length=64),
    FieldSchema(name="kb_id", dtype=DataType.VARCHAR, max_length=64),
    FieldSchema(name="content", dtype=DataType.VARCHAR, max_length=8192),
    FieldSchema(name="metadata", dtype=DataType.JSON),
])

index_params = {
    "index_type": "IVF_FLAT",  # 或 HNSW
    "metric_type": "COSINE",
    "params": {"nlist": 1024}
}
```

---

## 9. 技术依赖说明

| 依赖 | 版本建议 | 用途 | 许可证 |
|------|----------|------|--------|
| Python | ≥3.11 | 后端语言 | PSF |
| FastAPI | ≥0.110 | Web 框架 | MIT |
| LangChain | ≥0.2 | LLM 应用框架 | MIT |
| LangGraph | ≥0.1 | 多 Agent 编排 | MIT |
| Pydantic | ≥2.5 | 数据校验 | MIT |
| SQLAlchemy | ≥2.0 | ORM | MIT |
| Alembic | ≥1.13 | 数据库迁移 | MIT |
| Celery | ≥5.3 | 异步任务队列 | BSD |
| Redis-py | ≥5.0 | Redis 客户端 | MIT |
| pymilvus | ≥2.4 | Milvus 客户端 | Apache 2.0 |
| pdfplumber | ≥0.11 | PDF 解析 | MIT |
| python-docx | ≥1.1 | Word 解析 | MIT |
| markdown-it-py | ≥3.0 | Markdown 解析 | MIT |
| boto3 | ≥1.34 | MinIO/S3 客户端 | Apache 2.0 |
| httpx | ≥0.27 | HTTP 客户端 | BSD |
| LiteLLM | ≥1.40 | LLM 网关 | MIT |
| | | | |
| React | ≥18 | 前端框架 | MIT |
| TypeScript | ≥5.3 | 前端语言 | Apache 2.0 |
| Ant Design | ≥5.15 | UI 组件库 | MIT |
| Zustand | ≥4.5 | 状态管理 | MIT |
| Vite | ≥5.1 | 构建工具 | MIT |

### 外部服务依赖
- **通义千问 API** 或 **DeepSeek API**：LLM 推理
- **企业微信开放平台**：消息回调、OAuth 授权
- **BGE Embedding / Reranker 模型**：可本地部署（GPU 推荐）
- **Milvus 集群**：向量存储与检索
- **MinIO / S3**：文件对象存储

---

## 10. 风险分析

### 技术风险

| 风险 | 概率 | 影响 | 应对措施 |
|------|------|------|----------|
| LLM 回答幻觉 | 中 | 高 | Reranker 精排 + Prompt 约束 + 引用标注 + 人工审核 |
| 文档解析失败 | 低 | 中 | 支持多种解析引擎 fallback，提供手动编辑切片能力 |
| Milvus 性能瓶颈 | 中 | 高 | 合理设置索引参数（IVF_FLAT→HNSW），做数据分片 |
| LangGraph 版本升级破坏 | 中 | 中 | 锁定版本，建立回归测试套件 |
| 企微 API 变更 | 低 | 高 | 抽象企微适配层，支持多渠道 |
| Embedding 模型更新 | 低 | 中 | 旧向量保留，索引重建时可选 | 

### 成本风险

| 风险 | 说明 | 应对 |
|------|------|------|
| LLM API 费用超支 | 1000 次对话 ≈ 40 万 Token ≈ 1-2 元 | 设置日限额，Redis 缓存高频问题 |
| Milvus 机器费用 | 3 节点 8C16G ≈ 4000 元/月 | MVP 用 pgvector 替代，量上后迁移 |
| GPU 资源需求 | Embedding + Reranker GPU 部署 | 初期 CPU 推理（慢但可用），量上后加 GPU |

### 性能风险

| 风险 | 目标值 | 应对 |
|------|--------|------|
| 端到端响应延迟 | P99 < 5s | 流式输出、LLM 缓存、异步 Embedding |
| 检索延迟 | P99 < 200ms | Milvus 索引优化、连接池设置 |
| 高并发削峰 | 100 QPS | Redis 限流、任务队列削峰、水平扩展 |

### AI 幻觉风险
- **Prompt 层**：System Prompt 明确约束"不知道就说不知道"
- **检索层**：Reranker 精排 + 设置相似度阈值（低于阈值不回答）
- **输出层**：要求 LLM 标注引用 [1][2]，无引用内容标记为推测
- **监控层**：用户反馈自动标记可疑回答

### 数据风险
- 企业文档可能包含敏感信息
- 需支持数据不离开私有化部署
- 对话数据需加密存储，定期清理

---

## 11. 商业化设计

### 定价模式

| 方案 | 适用客户 | 定价 | 核心限制 |
|------|----------|------|----------|
| 社区版（开源） | 技术团队自建 | 免费 | 无商业支持，单租户 |
| 标准版（SaaS） | 中小企业（10-50 客服） | 基础费 ¥2,999/月 + ¥0.5/千次对话 | 最多 50 万文档，10 个知识库 |
| 专业版（SaaS） | 中型企业（50-200 客服） | ¥9,999/月 + ¥0.3/千次对话 | 不限文档量，多 Agent 全部功能 |
| 企业版（私有化） | 大型企业/金融机构 | ¥20万/年起（含 5 个节点部署） | 私有化部署、定制 Agent、SLA 99.9% |

### 付费点设计
1. **知识库容量**：免费版 1000 文档，超出按量付费
2. **LLM Token 消耗**：基础费含 100 万 Token/月，超出按 ¥0.002/千 Token
3. **Agent 定制**：标准版 6 个子图可用，专业版支持自定义 Agent
4. **企业微信侧边栏**：专业版及以上
5. **BI 分析面板**：专业版及以上
6. **人工转接坐席**：按坐席数收费（¥99/坐席/月）

### 转化路径
```
免费试用（14天全功能）
  → 体验到期
    → 社区版（开源自建）
    → 标准版（¥2,999/月）
      → 使用量增加
        → 升级专业版（¥9,999/月）
          → 安全合规需求
            → 企业私有化（¥20万/年）
```

### 附加收入
- **Agent 定制开发服务**：¥3-10 万/个
- **企业微信配置与培训**：¥5,000/次
- **专属模型微调**：¥8 万/次

---

## 12. 指标体系

### 产品核心指标

| 指标 | 定义 | 目标值 | 埋点位置 |
|------|------|--------|----------|
| DAU | 日活跃客服对话 | MVP 100 / 半年 1000 | 对话表日统计 |
| 对话量 | 日均处理对话数 | MVP 500 / 半年 5000 | 消息表日统计 |
| 自动解决率 | AI 独立解决 / 总对话 | > 80% | 转接标记 |
| 首次响应时间 | 用户发送到 AI 首次回复 | < 5s | 消息时间戳差 |
| 用户满意度 | 好评 / (好评+差评) | > 85% | 反馈表 |

### 质量指标

| 指标 | 定义 | 目标值 | 测量方式 |
|------|------|--------|----------|
| 意图识别准确率 | 识别正确的意图 / 总意图 | > 90% | 人工抽检 + 用户反馈 |
| 检索 top-5 准确率 | 前 5 个结果包含正确答案的比例 | > 85% | 标注数据集评估 |
| 回答准确率 | AI 回答正确的比例 | > 80% | 人工抽检 + 用户反馈 |
| 幻觉率 | AI 生成错误/虚假信息的比例 | < 5% | 人工抽检 |
| 文档解析成功率 | 成功解析 / 上传文档数 | > 95% | 解析日志 |

### 运营指标

| 指标 | 定义 | 目标值 |
|------|------|--------|
| 知识库更新频率 | 每周新增/更新文档数 | > 10 篇/周 |
| 人工介入率 | 需人工处理的对话比例 | < 20% |
| 转接满意度 | 转接后用户满意度评分 | > 80% |
| 反馈率 | 用户反馈/总对话 | > 10% |
| 答案修正率 | 人工修正 AI 回答 / 总反馈 | < 5% |

### 技术指标

| 指标 | 定义 | 目标值 |
|------|------|--------|
| API P99 延迟 | 最慢的 1% 请求耗时 | < 5s |
| 检索 P99 延迟 | 最慢的 1% 检索耗时 | < 200ms |
| 系统可用性 | 服务正常运行时间 | 99.5% |
| Milvus QPS | 每秒查询数 | > 100 |
| 文档处理吞吐 | 每分钟处理文档数 | > 10 篇 |

---


---

## 14. 评估数据来源与 PM 自测用例

### 评估数据来源

本项目评估数据来自三部分：

| 数据来源 | 内容 | 数量 |
|---------|------|------|
| 历史客服对话 | 企业微信客服过去 3 个月的真实客户咨询记录 | 500 条 |
| 检索 Ground Truth | 对每条问题人工标注"应该命中哪些文档" | 200 条 |
| 问答 Ground Truth | 每条客户问题配上标准答案（由资深客服编写） | 200 条 |

**Ground Truth 标注流程**：
1. 从 500 条客服对话中抽出 200 条
2. 2 位客服主管分别标注"这个问题应该从知识库的哪些文档找答案"
3. 取两人选择的交集作为 ground truth，争议项讨论
4. 最终每条问题对应 1-5 个相关文档 ID

### KPI 定义与计算公式

**检索阶段 KPI**

| KPI | 公式 | 数据来源 | 目标值 |
|-----|------|---------|--------|
| **Recall@10** | 前 10 个检索结果中，命中 Ground Truth 文档数 / GT 总文档数 × 100% | 200 条检索 GT | > 85% |
| **MRR** | 每条问题第一个命中 GT 的排名的倒数，取 200 条平均 | 200 条检索 GT | > 0.85 |
| **Hit Rate** | 至少命中 1 个 GT 文档的问题数 / 总问题数 × 100% | 200 条检索 GT | > 95% |
| **Precision@5** | 前 5 个结果中命中 GT 的比例 | 200 条检索 GT | > 60% |

**生成阶段 KPI**

| KPI | 公式 | 数据来源 | 目标值 |
|-----|------|---------|--------|
| **Faithfulness** | 回答内容能在检索文档中找到依据的比例（人工评） | 200 条问答 GT | > 95% |
| **回答要素覆盖率** | 每条回答中 expected_elements 命中率，取平均 | 10 条自测 + 200 条 GT | > 85% |
| **无答案准确率** | 知识库无相关内容时，正确回答"不知道"的比例 | 含无 GT 的用例 | > 90% |

**系统性能 KPI**

| KPI | 公式 | 数据来源 | 目标值 |
|-----|------|---------|--------|
| **端到端 P50 延迟** | 用户发消息到收到回复的时间中位数 | 全量请求 | < 3s |
| **检索 P99 延迟** | 最慢的 1% 检索耗时 | 全量请求 | < 200ms |

### PM 自测用例（10 条）与评分规则

每条用例跑完后记录两个阶段的数据：

```python
test_result = {
    "用例编号": 1,
    "query": "A-line婚纱有哪些颜色可选？",
    
    # 阶段一：检索
    "实际检索到的 docs": ["product_guide", "size_chart", "fabric_guide"],
    "GT 期望的 docs": ["product_guide", "color_chart"],
    "命中数": 1,           # product_guide 命中了
    "Recall": 1/2 = 50%,   # 2 个期望文档，只命中 1 个
    "MRR 贡献": 1/1 = 1.0, # 第 1 个就命中了
    
    # 阶段二：生成
    "模型回答": "A-line婚纱有白色、象牙色、香槟色可选...",
    "预期要素": ["A-line", "颜色选项"],
    "实际命中要素": ["A-line", "颜色选项"],
    "要素覆盖率": 100%,
    
    "响应时间_ms": 1850,
    "是否通过": True,   # 检索 Recall > 85%（这条没通过）+ 要素全命中
}
```

**这个评分揭示了重要信息**：
- 检索 Recall 只有 50%（没到 85%）→ 问题出在 Milvus 检索，不是 LLM
- Reranker 即使把结果排好了，检索阶段漏了也是白费
- 这就是为什么 Recall 是 RAG 系统**最核心**的 KPI

### 10 条自测用例

```python
test_cases = [
    # 场景1：产品咨询
    {"query": "A-line婚纱有哪些颜色可选？",
     "expected_docs": ["product_guide", "color_chart"],
     "expected_elements": ["A-line", "颜色选项"]},
    # 场景2：尺码咨询
    {"query": "我5'4，140磅，穿什么码？",
     "expected_docs": ["size_chart", "fit_guide"],
     "expected_elements": ["尺码建议", "测量方法"]},
    # 场景3：物流查询
    {"query": "订单AZ2024001发货了吗？",
     "expected_docs": ["shipping_policy", "order_tracking"],
     "expected_elements": ["订单状态", "物流时效"]},
    # 场景4：退换货
    {"query": "婚纱不合适能退吗？",
     "expected_docs": ["return_policy", "exchange_process"],
     "expected_elements": ["退货条件", "时间窗口", "流程"]},
    # 场景5：材质清洗
    {"query": "蕾丝婚纱怎么清洗？",
     "expected_docs": ["care_instructions"],
     "expected_elements": ["干洗", "蕾丝保养"]},
    # 场景6：定制修改
    {"query": "能改短裙摆吗？多少钱？",
     "expected_docs": ["alteration_service", "pricing"],
     "expected_elements": ["改短", "费用"]},
    # 场景7（边界）：无此知识
    {"query": "老板叫什么？",
     "expected_docs": [],
     "expected_elements": ["无法回答", "转人工"]},
    # 场景8（边界）：多语言
    {"query": "Do you ship to Canada?",
     "expected_docs": ["shipping_policy"],
     "expected_elements": ["英文", "加拿大"]},
    # 场景9（边界）：投诉情绪
    {"query": "太过分了！20天还没收到！",
     "expected_docs": ["complaint_process", "shipping_policy"],
     "expected_elements": ["道歉", "查询", "方案"]},
    # 场景10（边界）：多问题混合
    {"query": "多少钱？有折扣吗？多久到？",
     "expected_docs": ["pricing", "promotion", "shipping_policy"],
     "expected_elements": ["价格", "促销", "物流"]},
]
```

### 通过标准（四层，顺序执行）

```
第一层：10 条自测通过
  → 检索 Recall >= 70%（10 条平均）
  → 回答要素覆盖率 100%（每条都全命中）
  → 不通过就调检索策略或 Prompt

第二层：200 条检索测试集
  → Recall@10 > 85%     ← 检索阶段的核心指标
  → MRR > 0.85           ← 排名够不够靠前
  → Hit Rate > 95%       ← 有没有完全查不到的

第三层：200 条问答评估
  → Faithfulness > 95% ← LLM 有没有编造
  → 人工评分 >= 4.0/5

第四层：上线后追踪
  → 转人工率 < 15%
  → 用户修正率 < 20%
  → P50 延迟 < 3s
### ROI 计算

| 项目 | 金额 | 说明 |
|------|------|------|
| 开发（2工程师 x 3月） | $48,000 | RAG + Agent + 企微对接 |
| 知识库整理（2人月） | $7,000 | 文档分类与质量审核 |
| Ground Truth 标注 | $1,500 | 200条检索 + 200条问答 |
| **一次性总成本** | **$56,500** | 分摊3年 = $18,833/年 |
| LLM API | $113/年 | |
| Embedding + Reranker | $560/年 | |
| 服务器 | $960/年 | |
| 维护（0.5工程师） | $25,000/年 | |
| **年总成本** | **$45,506** | |
| **年总收益** | **$620,000** | 省10人$42万+退货降3%$15万+夜间$5万 |

**ROI = ($620,000 - $45,506) / $45,506 = 1,262%**
**回本周期：约 1 个月**

## 13. 与研发协作说明

### 协作流程

```
产品（PRD + 原型）→ 技术评审 → 任务拆分（Jira/Notion）
  → 前端/后端/算法并行开发
  → 每日站会 15min（阻塞问题同步）
  → 每周验收（产品验收 Demo）
  → 回归测试 → 发布上线
```

### 各阶段协作要点

**需求阶段（Week 0）**
- 产品：输出 PRD + 页面原型（Figma / Axure）
- 研发：技术评审，输出技术选型文档
- 共识：明确 MVP 范围，P0 功能不可删减

**开发阶段（Week 1-6）**
- 产品：每周一验收上周交付功能，反馈修改意见
- 后端：先交付 API 文档（OpenAPI），前端可并行开发
- 前端：使用 Mock 数据开发，API 就绪后联调
- Agent 开发：数据标注（意图分类样本）需要产品协助准备

**测试阶段（Week 7-8）**
- 研发：单元测试、集成测试、压力测试
- 产品：UAT（用户验收测试），准备测试用例
- QA：功能测试、兼容性测试、安全测试

**上线阶段（Week 8）**
- 产品：编写帮助文档、培训资料
- 运营：配置企业微信应用、准备种子知识库
- 研发：部署 K8s、配置监控告警、备份策略

### 日常协作规范

| 事项 | 频率 | 参与人 | 输出物 |
|------|------|--------|--------|
| 站会 | 每日 10:00 | 全员 | 昨日完成/今日计划/阻塞 |
| 需求评审 | 每迭代开始 | 产品+研发 | PRD 确认 |
| 技术评审 | 需求评审后 | 后端+前端+算法 | 技术方案文档 |
| 代码 Review | 每次 PR | 研发 | Code Review Comment |
| Demo 验收 | 每周五 | 产品+研发 | 验收通过/修改清单 |
| 迭代复盘 | 每迭代结束 | 全员 | 复盘文档 |

### 分工建议

| 角色 | 人数 | 职责 |
|------|------|------|
| 产品经理 | 1 | PRD、验收、运营配置 |
| 后端工程师 | 2-3 | API、数据库、文档处理管线、Milvus |
| 前端工程师 | 1-2 | 管理后台、对话调试页 |
| AI/Agent 工程师 | 1-2 | LangGraph 图、Agent 子图、RAG 管线 |
| DevOps/运维 | 1 | CI/CD、K8s 部署、监控 |
| QA 测试 | 1 | 功能测试、回归测试、性能测试 |
| UI/UX 设计 | 0.5（可复用） | 页面原型、交互设计 |

**总计：约 7-10 人核心团队，8 周交付 MVP**
