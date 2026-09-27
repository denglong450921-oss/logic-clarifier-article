# logic-clarifier

一个用于 Codex 的“厘清逻辑” Skill。

它不是普通总结器，而是一个“路由 + 双引擎 + 审计 + 压缩”的逻辑系统：

```text
用户请求
│
├─ 分析现有材料
│   ↓
│  Argument Reconstruction
│
├─ 帮用户构建现实论证
│   ↓
│  Probabilistic Argument
│
└─ 两者都要
    ↓
   先重构原文
    ↓
   再审计 / 增强
```

最后再压缩成：

**母问题 → 核心答案 → 旧模型/新模型 → 论证机制 → 真实拓扑逻辑图 → 隐藏前提 → 适用边界 → 可复用框架**

## 目录

```text
logic-clarifier/
├── SKILL.md
├── README.md
├── assets/
│   └── output-template.md
├── references/
│   ├── task-router.md
│   ├── logic-audit.md
│   ├── probabilistic-argument.md
│   └── source-trace-map.md
└── examples/
    ├── article-analysis-example.md
    └── probabilistic-argument-example.md
```

## 安装到 Codex

Codex 支持用户级和项目级 Skill。

### 用户级（所有项目可用）

macOS / Linux:

```bash
mkdir -p ~/.codex/skills
cp -R logic-clarifier ~/.codex/skills/logic-clarifier
```

Windows PowerShell:

```powershell
New-Item -ItemType Directory -Force "$HOME/.codex/skills" | Out-Null
Copy-Item -Recurse -Force ".\logic-clarifier" "$HOME/.codex/skills/logic-clarifier"
```

### 项目级（只在当前仓库使用）

把整个目录复制到：

```text
<你的项目>/.codex/skills/logic-clarifier/
```

安装完成后，确保存在：

```text
.codex/skills/logic-clarifier/SKILL.md
```

或：

```text
~/.codex/skills/logic-clarifier/SKILL.md
```

## 推荐触发方式

自然语言通常即可触发，例如：

- 帮我厘清这篇文章的逻辑。
- 这篇文章主要回答了什么问题？
- 不要总结，帮我恢复作者完整论证链。
- 用二进制逻辑图拆一下这篇文章。
- 找出里面的逻辑跳跃、偷换概念和隐藏前提。
- 把这篇文章的几个观点合成一个统一模型。

如果你想显式调用，可直接对 Codex 说：

```text
Use the logic-clarifier skill to analyze this article.
```

## 推荐用法

### 1. 普通厘清

```text
帮我厘清这篇文章的逻辑。重点回答：
1. 它主要回答什么问题；
2. 核心结论是什么；
3. 各部分是怎么一步步推出的；
4. 用二进制逻辑图显示。
```

### 2. 批判分析

```text
用 logic-clarifier 深度分析这篇文章。
除了恢复作者逻辑，还要指出：
- 缺失前提
- 因果跳跃
- 偷换概念
- 适用边界
- 哪些结论说得过头
```

### 3. 转成自己的方法论

```text
厘清这篇文章后，不要停在总结。
把它转成我以后可以反复调用的判断框架和自问清单。
```


## 概率论证模式

当任务不是“分析作者怎么论证”，而是“帮我把一个现实观点论证得更有力”时，Skill 会自动从严格证明切换为 **概率论证 / 最小充分论证**。

推荐触发：

```text
帮我论证这个观点，但不要为了全面把所有变量都列出来。
请：
1. 先限定命题；
2. 找 3–5 个最可能改变结论的关键变量；
3. 优先补政府、大型机构或研究数据；
4. 说明因果/机制；
5. 处理最强反方；
6. 最后给一个与证据强度匹配的有限结论。
```

适合：

- 现实争论与辩论；
- 短视频口播观点；
- 教育、商业、管理、人生选择；
- “这个观点有没有道理”；
- “怎样证明得更顺、更有条理”。

核心不是穷尽世界，而是：

```text
限定命题
+
关键变量
+
可靠证据
+
机制
+
比较
+
最强反证
↓
足够可信的有限结论
```


## 核心架构

```text
Task Router
    ↓
┌───────────────┬────────────────┐
│               │                │
▼               ▼                │
Argument        Probabilistic    │
Reconstruction Argument         │
│               │                │
└───────────────┴───────┬────────┘
                        ↓
                   Logic Audit
                        ↓
                 Slow Variables
                        ↓
                Reusable Framework
```

### 为什么这样改？

旧版本把“分析作者论证”和“帮助用户自己论证”塞进同一条长 Workflow，导致概率论证直到后半段才分流。

现在一开始就判断任务类型：

- **Reconstruction**：恢复作者到底是怎么论证的；
- **Probability**：帮助用户构建现实世界的有限论证；
- **Mixed**：先冻结作者原逻辑，再进入审计/补强。

## 逻辑图原则

“二进制逻辑图”不再是默认强制形态。

根据真实拓扑选择：

- YES / NO 判断 → 二进制树；
- 原因 → 机制 → 结果 → 因果链；
- 多个平级变量 → 并列结构；
- 多路径回到同一结论 → 分支 + 汇聚；
- 治理 / 学习 / 风险迭代 → 反馈环。

**表达形式服从真实逻辑，而不是为了好看制造不存在的二元对立。**

## Source Trace Map

处理文章、字幕、PDF、白皮书时，可以内部记录：

```text
source span
→ node id
→ direct / synthesized / inference / gap
```

用于回答：

> “这个节点到底是作者原文说的，还是我们分析出来的？”

详细见：

`references/source-trace-map.md`
