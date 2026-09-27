# Source Trace Map

用于文章、字幕、报告、白皮书、访谈等“Logic Extraction / Reconstruction”任务。

目的：

> 让每一个提炼后的逻辑节点，都能追溯到原始材料；防止为了让逻辑图更漂亮而偷偷补出原文没有的结论。

## Recommended structure

```json
{
  "sourceId": "article-01",
  "coordinateSystem": "rendered-lines",
  "nodes": {
    "n1": {
      "sourceSpans": [
        {"startLine": 12, "endLine": 18}
      ],
      "relation": "direct",
      "note": "作者直接提出母问题。"
    },
    "n2": {
      "sourceSpans": [
        {"startLine": 33, "endLine": 48}
      ],
      "relation": "synthesized",
      "note": "将三段案例压缩为一个共同机制。"
    },
    "n3": {
      "sourceSpans": [],
      "relation": "inference",
      "note": "这是分析者推出的含义，原文未直接表述。"
    }
  }
}
```

## Relation types

### `direct`
原文明确说出，节点基本是原文主张的结构化表达。

### `synthesized`
节点由多段原文归纳压缩而来，但没有改变原意或结论强度。

### `inference`
分析者基于原文推出的解释。不能冒充作者明确主张。

### `gap`
论证中缺失的前提、比较或证据。

例：

```text
作者说：
深圳是全国教育性价比最高

但原文没有做：
跨城市统一指标比较

→ relation = gap
```

## Rules

1. Reconstruction 模式下，核心节点应尽量可追溯。
2. `direct` / `synthesized` 应有 source span。
3. `inference` 必须和作者主张区分。
4. 不把“可能”升级成“一定”。
5. 不用一个漂亮箭头补掉原文缺失的前提。
6. 外部搜索得到的材料不写入原文 trace；另列为“外部补强证据”。

## Coordinates

### SRT / transcript
优先使用：
- 字幕块编号；或
- 渲染后的稳定行号。

### PDF / white paper
优先使用：
- 页码 + 行/段范围；
- 若只能可靠定位到页，则明确是 coarse trace。

### Web article
可使用：
- 段落编号；
- 标题 + 段落范围；
- 工具提供的稳定行号。

## Output visibility

Trace Map 默认是内部验证层，不必全部展示给用户。

以下情况建议显式展示：
- 用户问“这个结论原文哪里来的？”
- 需要高可靠审计；
- 要把结果交给另一个 Skill / renderer；
- 争议材料需要区分作者主张与分析者推论。
