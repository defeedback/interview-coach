# Phases 0-9 完整流程

## Phase 0：初始化工作目录

在用户指定的工作目录下创建：

```text
interview-coach/
├── README.md
├── profile/
│   ├── basic.md        # 基本信息：姓名、工作年限、目标岗位
│   ├── career.md       # 职业时间线
│   └── skills.md       # 技能清单（每项标注归属层级）
├── experiences/
│   └── raw-experience.md   # 原始经历考古记录
├── projects/
│   └── <project-name>/     # 每个项目一个目录
├── interview/
│   ├── questions.md    # 面试题树汇总
│   ├── sessions/       # 每次模拟面试记录
│   └── feedback/       # 面试反馈分析
├── knowledge/
│   ├── gaps.md         # 知识漏洞清单
│   └── learning/       # 针对漏洞的学习笔记
└── resume/
    └── resume.md       # 最终输出：简历
```

## Phase 1：工作经历考古

**禁止直接问"请描述你的工作经历"** —— 这样用户容易开始"包装"。

采用循环：`回忆 → 追问 → 记录 → 验证 → 继续追问`。

提问链示例（一次只问一个）：

1. 你入职后的第一个实际任务是什么？
2. 这个任务是谁提出的？
3. 你具体负责哪一步？
4. 是你自己写的，还是别人已经写好你修改？
5. 使用了什么技术？
6. 为什么需要你做？
7. 最终交付给谁？

每个任务还原后写入结构化记录：

```yaml
task:
  name: 合同解析
  source: 业务需求
  responsibility:
    - PDF文本提取
    - Word文本提取
  ownership:
    level: primary        # 对应 OWNED
    confidence: high
  technologies:
    - Python
    - FastAPI
  output:
    - 结构化合同文本
```

## Phase 2：职责地图

原始经历收集完成后，自动分类生成职责地图，例如：

```text
工作经历
├── 业务需求（合同审核、配方研发…）
├── AI应用（LLM、RAG、Prompt、Agent…）
├── 后端（FastAPI、PostgreSQL、Redis…）
├── 数据工程（数据清洗、文档解析、数据导入…）
├── 模型部署（vLLM、Docker…）
└── 业务交付（钉钉集成、业务验证…）
```

然后给出一个**来自真实经历的结论**（不是提前规定的），例如：

> 你的核心职责不是"写 Python"，而是"围绕企业业务场景进行 AI 应用落地：从需求分析、方案设计、LLM/RAG 开发，到 API、模型部署和业务验证。"

## Phase 3：项目重建

逐个项目处理，每个项目建立 13 个文件：

```text
projects/<project-name>/
├── 01_business.md        # 业务背景：为什么做？谁使用？解决什么问题？
├── 02_requirement.md     # 需求：原来怎么完成？最大痛点？
├── 03_responsibility.md  # 职责：你负责哪部分？实际写了哪些代码？
├── 04_architecture.md    # 整体架构、服务划分、数据流
├── 05_modules.md         # 模块拆解
├── 06_data.md            # 数据来源、处理、存储
├── 07_llm.md             # Prompt、Context、结构化输出、幻觉处理
├── 08_rag.md             # 数据、Chunk、Embedding、Retrieval、Rerank、评估
├── 09_deployment.md      # Docker、vLLM、GPU
├── 10_problems.md        # 遇到的问题与解决
├── 11_decisions.md       # 技术选型与取舍
├── 12_results.md         # 结果与验证
└── 13_interview.md       # 该项目的面试问答积累
```

**关键规则：绝不允许一次生成整个项目。** 一个问题一个问题地问，直到项目被还原。提问顺序示例：这个项目为什么要做？→ 原来怎么完成这个工作？→ 最大的问题是什么？→ 你负责哪一部分？→ 你实际写了哪些代码？→ 数据从哪里来？→ …

## Phase 4：技术深挖

见 references/deep-dive.md。

## Phase 5：模拟面试

递归追问式模拟，见 references/deep-dive.md。每次模拟后必须做四分类分析，见 references/gap-system.md。

## Phase 6-7：漏洞分析与知识补齐

见 references/gap-system.md。闭环：`面试 → 暴露漏洞 → 记录漏洞 → 学习 → 重新回答 → 验证`。

## Phase 8：项目表达训练

知识补齐之后才训练表达。生成三个版本：

- **30 秒版**：回答"简单介绍一下这个项目"
- **2 分钟版**：回答"详细讲一下这个项目"
- **5-10 分钟版**：从业务、架构、技术选型、难点、优化完整讲

**表达训练不是背稿。** 随机改变提问角度：

- "不从项目背景开始，从你负责的模块开始讲。"
- "假设我是后端面试官，只问技术。"
- "假设我是 AI 应用面试官，只问 RAG。"

## Phase 9：输出

从项目知识库抽取生成：

```text
          ┌──── 简历
          ├──── 自我介绍
项目知识库 ┼──── 项目介绍
          ├──── 面试回答
          └──── 技术追问
```

**硬性约束**：简历内容只能使用已验证为 `OWNED` 或 `CONTRIBUTED` 的经历；`UNDERSTOOD` 的内容只能在面试口头表达中作为"了解"出现；`TEAM`/`UNKNOWN` 不得写入简历。
