# 🏢 企业 RAG 知识库客服系统

> **作品集项目** | 完整展示 AI 产品经理的"融合架构设计"能力

---

## 项目简介

融合 **Mildoc（RAG 知识库）** 和 **Sagt（多 Agent 智能客服）** 两种架构模式，构建的企业级 AI 客服解决方案。

文档自动索引（PDF/Office/MD）→ 向量检索（Milvus）→ Reranker 重排序 → LLM 生成回答，配合 LangGraph 多 Agent 做意图路由和子图分发。

## 技术栈

| 技术 | 用途 |
|------|------|
| **LangChain** | RAG Pipeline 编排 |
| **LangGraph** | 多 Agent 架构（主图+子图） |
| **Milvus** | 向量数据库（IVF_FLAT + COSINE） |
| **Reranker (Cross-Encoder)** | 搜索结果重排序 |
| **FastAPI** | 后端 API |
| **企业微信 API** | 客服渠道集成 |
| **LiteLLM** | 多模型统一接入 |

## 文档导航

| 文件 | 内容 | 展示的 PM 能力 |
|------|------|---------------|
| [planner.md](./planner.md) | 技术规划：RAG 架构、Agent 编排、向量库选型评估 | 架构决策能力 |
| [prd.md](./prd.md) | 产品需求：竞品分析、MVP、检索评估体系、商业化 | 产品定义 + 评估体系 |

## 核心 AI PM 决策要点

```
RAG 三段式为什么这么设计？
  → 向量检索（召回）→ Reranker（精排）→ LLM（生成）
  → 每一段独立优化，一段出问题不影响其他段

为什么 Recall 和 MRR 比 Precision 更重要？
  → 检索的目标是"别漏掉"（Recall），
    排序的目标是"把最好的放最前面"（MRR），
    Precision 在 Top-K 场景下天然偏低，不需要过度关注

Reranker 的安全机制是什么？
  → 如果 Reranker 把原始第 1 名过滤掉了，强制加回来
  → 防止 Reranker "过度自信"把好结果排到后面
```

---

*这是 AI 产品经理作品集项目之一。更多项目：*
- [私人医生助手](https://github.com/Ruidee/private-doctor-assistant)
- [办公流程自动化 Agent](https://github.com/Ruidee/office-automation-agent)
