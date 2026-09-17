# 归属分级与知识漏洞系统

## 归属五级分类（真实性机制）

每一段经历、每一项技术必须标注归属，防止把团队成果误认为个人成果：

| 标记 | 含义 |
|---|---|
| `OWNED` | 我亲自实现 |
| `CONTRIBUTED` | 我参与过 |
| `UNDERSTOOD` | 我了解原理，但没实现 |
| `TEAM` | 团队其他人做的 |
| `UNKNOWN` | 我现在不确定 |

示例：

```text
Hybrid Retrieval   ownership: OWNED
Rerank             ownership: CONTRIBUTED
vLLM 部署          ownership: OWNED
前端 Vue           ownership: TEAM
OCR                ownership: UNKNOWN
```

用途：简历只写 OWNED / CONTRIBUTED；模拟面试中被追问到 TEAM / UNKNOWN 的内容时，重点检验用户是否能诚实界定边界。

## 面试失败四分类

每次模拟面试后，把答不上来或答不好的问题分类：

1. **Knowledge Gap（知识漏洞）** — 真正不会。例：不知道 Rerank 为什么存在。
2. **Expression Gap（表达漏洞）** — 知道但说不出来。例：知道 Hybrid Retrieval，但无法组织语言。
3. **Evidence Gap（证据漏洞）** — 知道原理但没有真实项目证据。例：说用了 Rerank，但不知道具体模型、参数、效果。
4. **Ownership Gap（归属漏洞）** — 其实不是自己做的。例：简历写"负责模型部署"，实际只是执行别人给的 docker 命令。

## 漏洞记录 Schema

所有漏洞记录到 `knowledge/gaps.md`：

```yaml
gap:
  topic: Hybrid Retrieval
  question: 为什么需要 Hybrid Retrieval？
  type: knowledge_gap          # knowledge_gap / expression_gap / evidence_gap / ownership_gap
  severity: high               # high / medium / low
  current_answer:
    "因为向量检索和关键词检索结合效果更好"
  problem:
    "知道结论，不知道具体业务原因"
  required:
    - BM25 原理
    - Dense Retrieval
    - Recall / Precision
    - Hybrid Retrieval 融合方式
  status: TODO                 # TODO / LEARNING / REVIEW / DONE
```

## 学习闭环

```text
面试 → 暴露漏洞 → 记录漏洞 → 学习 → 重新回答 → 验证
```

执行方式：

1. **学习**：针对 `required` 清单讲解知识点，结合用户的真实项目场景（不用抽象例子），笔记写入 `knowledge/learning/<topic>.md`。
2. **重新回答**：让用户用自己的话重新回答原问题。
3. **验证**：换角度追问同一知识点（防止背答案）。通过后把 status 改为 `REVIEW`。
4. **复习**：`REVIEW` 状态的漏洞在后续模拟面试中随机抽考，连续两次答对才改 `DONE`。

## 反模式（禁止）

```text
面试 → 发现不会 → 看答案 → 背答案 → 忘掉
```

漏洞的价值在于驱动学习和验证，不在于收集标准答案。
