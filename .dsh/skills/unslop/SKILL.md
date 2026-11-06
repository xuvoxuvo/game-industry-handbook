---
name: unslop
description: Remove AI writing patterns from prose. Use when editing or reviewing AI-drafted copy (article ledes, site text, docs) to make it read like a person wrote it — or when asked to "humanize", "de-slop", "fix AI text", or "make it sound natural".
license: MIT
metadata:
  author: claytonkim
  version: "2.3.0"
  source: https://github.com/theclaymethod/unslop
  vendored: SKILL.md + references/core-contract.md（其余 references/presets 未随仓库提供）
argument-hint: "[cleanup|rewrite] [file]"
---

# Unslop（精简安装版）

Humanize AI-generated prose. Audit first. Rewrite only when the user asks for a rewrite.

## 用法

- **审计**：逐句指出「公式化开场、空洞抽象、无依据的确定性、比喻混用、标题与内容不符、无意义重复、自相矛盾」的位置，只报告不改写。
- **改写**：只动被确认的句子，其余逐字保留；不新增事实、建议、结论。

判定规则：`references/core-contract.md`。下面是其中最关键的部分。

## 核心判定

- 一次扫描命中不足以构成修改理由。字面用法、领域术语、引用、已准确加限定的表述、体裁惯例——都算受保护的用法。
- 删除后不损失信息的，才算填充词；把夸大措辞换成朴素说法。
- 标点、用词、节奏、结构本身不能证明文本有问题，也不能用来判断作者是谁。
- 不要根据日期或外部知识去事实核查；缺少证据本身不算缺陷。
- 对照原文的主张：如果观察结果与某个状态矛盾，就收窄那个状态。

## 改写规则

- 只改有确认缺陷的句子，用最小改动；其他句子逐字保留、顺序不变、分段不变。
- 保留事实、数量、日期、人名、引文、代码、单位、范围、不确定性、归属与语域。
- 不要补充主张、建议、个人经历或结论；不要用新填充替换旧填充，也不要为了"反 AI"写成断句式短句堆叠。
- 安全、法务、技术规则里的 "never" / "must" / "all" 原样保留。

## 输出格式（审计）

```markdown
## Issues Found
- [引用原句 | 类别 | 严重度 | 为什么读起来像 AI]

## Assessment
- [哪些是明确问题]
- [哪些是判断题]
```

## 中文常见 AI 痕迹（补充清单）

原 skill 面向英文；中文写作时同样适用下列形态：

- 开场套话：「在当今……的时代」「随着……的不断发展」
- 三段式凑数：任何事情都拆成「首先/其次/最后」三点
- 无主断言：「业内普遍认为」「众所周知」
- 空洞收尾：「综上所述」「希望本文能为你带来启发」
- 动词膨胀：赋能、抓手、闭环、打造、助力
- 假精确：「据研究表明」但不给出处
