# Task Router

在进入分析前，先判断用户到底在要求哪一种工作。不要让“分析现有论证”和“帮助用户构建论证”共用同一条流水线。

## Route A — Argument Reconstruction

用户已经提供文章、字幕、报告、白皮书、访谈、演讲或观点材料，主要问：

- 这篇材料在回答什么问题？
- 作者的核心结论是什么？
- 逻辑怎么一步步推出？
- 有没有逻辑跳跃？
- 帮我厘清、拆解、理顺。

目标：

> 恢复原作者的论证结构，而不是替作者补一个更漂亮的新论证。

进入：**Argument Reconstruction Engine**

---

## Route B — Argument Building / Probability

用户主要问：

- 帮我论证这个观点。
- 这个说法怎么证明得更有力？
- 找数据支持。
- 这个观点有没有道理？
- 怎么辩？
- 从概率上论证。

目标：

> 在明确范围内，用关键变量、可靠证据、机制和最强反方，构建“足够可信”的现实论证。

进入：**Probabilistic Argument Engine**

---

## Route C — Mixed

用户先提供材料，再要求：

> 先厘清作者怎么论证，再判断是否成立 / 帮我增强。

顺序必须是：

```text
先 Reconstruction
↓
冻结“作者原本说了什么”
↓
再进入 Audit / Probability
↓
补外部证据或重建更强论证
```

不要把后补证据冒充原文。

---

## Fast decision tree

```text
用户是否提供了现成材料？
│
├─ YES
│   ↓
│  主要是在问“作者怎么论证”？
│   ├─ YES → Reconstruction
│   └─ NO
│       ↓
│      还要求判断/增强/找证据？
│       └─ YES → Reconstruction → Audit/Probability
│
└─ NO
    ↓
   用户是否要自己证明/论证一个现实观点？
    ├─ YES → Probability
    └─ NO → 普通解释，不必强制使用本 Skill
```

## Formal-proof exception

若任务属于：

- 数学；
- 定义系统；
- 封闭规则；
- 形式逻辑；

可要求：

```text
前提成立
↓
结论必然成立
```

现实社会、教育、商业、管理、人生选择等默认不是这种模式。
