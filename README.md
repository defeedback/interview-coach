# interview-coach

> 项目经历教练 / Interview Project Coach —— 一个把面试准备变成可重复执行流程的 WorkBuddy 技能。

## 这是什么

不是"简历生成器"，而是一个**面试能力构建工作流**。它扮演教练而非写手，通过不断提问，把用户脑中零散的项目经验逐步结构化，并通过面试追问暴露知识边界，最终形成可复用的**项目知识库**（简历只是其中一个视图）。

## 核心流程

```text
采集真实经历 → 重建职责 → 重建项目 → 深挖技术 → 模拟追问
                → 捕获漏洞 → 补齐知识 → 再次验证 → 输出简历与面试表达
```

## 关键机制

- **真实性分级**：每段经历/技术标注 `OWNED` / `CONTRIBUTED` / `UNDERSTOOD` / `TEAM` / `UNKNOWN`，防止把团队成果误当个人成果，简历只写前两级。
- **一次一问**：绝不一次性生成项目，一个问题接一个问题地还原。
- **递归追问式模拟面试**：直到发现知识边界才停，不主动给标准答案。
- **漏洞闭环**：每次答不上来都记录为知识漏洞（知识/表达/证据/归属四类），驱动学习与验证。

## 技能结构

```text
interview-coach/
├── SKILL.md              # 核心规则、状态机、阶段路由
├── references/
│   ├── phases.md         # Phase 0-9 流程、目录初始化、经历考古、项目重建
│   ├── deep-dive.md      # 技术深挖模板、递归追问、面试题树、表达训练
│   └── gap-system.md     # 归属分级、漏洞记录、学习闭环
├── README.md
└── LICENSE
```

## 安装

```bash
# 方式一：直接克隆到 WorkBuddy 用户级技能目录
git clone git@github.com:defeedback/interview-coach.git \
  "$HOME/.workbuddy/skills/interview-coach"

# 方式二：下载 zip 解压到 ~/.workbuddy/skills/interview-coach/
```

安装后在 WorkBuddy 中说"开始梳理我的项目经历"或"模拟面试"即可触发。

## 使用方式

| 你想做 | 我会 |
|---|---|
| 开始面试准备 | 初始化工作目录结构 |
| 梳理工作经历 | 一个一个问题考古，生成职责地图 |
| 重建某个项目 | 13 个文件逐问还原 |
| 深挖技术点 | 按"是什么→为什么→怎么做→取舍→验证"递归追问 |
| 模拟面试 | 递归追问直到知识边界 |
| 看漏洞 | 按四类失败类型分类记录 |
| 生成简历 | 只从已验证的 OWNED/CONTRIBUTED 内容抽取 |

## 在其他智能体中使用

本 skill 采用通用的 `SKILL.md` + YAML frontmatter 格式，核心字段（`name` / `description`）被主流智能体共同识别，可直接复用到以下产品。仓库已托管在 GitHub：

```bash
git clone https://github.com/defeedback/interview-coach.git
```

克隆后把 `interview-coach/` 目录整体复制到对应智能体的技能目录下即可。

### WorkBuddy
```bash
git clone https://github.com/defeedback/interview-coach.git \
  "$HOME/.workbuddy/skills/interview-coach"
```

### Claude Code
技能放在项目级或用户级 `.claude/skills/` 下（目录结构与本仓库一致）：
```bash
# 用户级（所有项目可用）
cp -r interview-coach "$HOME/.claude/skills/interview-coach"
# 或项目级
cp -r interview-coach .claude/skills/interview-coach
```
会话中输入 `/interview-coach` 直接调用，或当描述匹配时由 Claude 自动触发。也可打包为 Plugin（`.claude-plugin/plugin.json` + `skills/`）共享给团队。

### OpenCode
原生搜索 `.opencode/skills/`，同时兼容 `.claude/skills/` 与 `.agents/skills/`：
```bash
# 全局
cp -r interview-coach "$HOME/.config/opencode/skills/interview-coach"
# 或项目级
cp -r interview-coach .opencode/skills/interview-coach
```
可选：在 `SKILL.md` 的 frontmatter 增加 `compatibility: opencode` 字段。Agent 通过原生 `skill` 工具按需加载。

### OpenClaw
OpenClaw 支持从 Git 仓库直接安装（也支持 ClawHub 市场）：
```bash
# 安装到当前工作区
openclaw skills install git:defeedback/interview-coach@main
# 安装到所有本地 agent（共享目录 ~/.openclaw/skills）
openclaw skills install git:defeedback/interview-coach@main --global
```
或手动把目录放入工作区 `/skills` 或 `~/.openclaw/skills` 后重启会话。

### 其他遵循 Open Agent Skills 规范的产品
本 skill 符合 [Open Agent Skills](https://openagentskills.dev) 约定（`SKILL.md` + `name`/`description` frontmatter）。任何识别该规范、在 `.claude/skills/`、`.opencode/skills/`、`.agents/skills/` 等路径下发现 `SKILL.md` 的智能体，都可直接加载。

> 说明：核心规则与流程已内联在 `SKILL.md`；`references/` 为补充细节，支持资源加载的智能体可一并保留，不支持的仅用 `SKILL.md` 亦完整可用。

## License

MIT © defeed
