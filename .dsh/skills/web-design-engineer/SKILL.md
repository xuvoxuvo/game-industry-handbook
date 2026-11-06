---
name: web-design-engineer
description: "Design or redesign polished, browser-rendered visual artifacts (pages, dashboards, prototypes, decks, data visualizations) with HTML/CSS/JS. Includes a design-system declaration step, anti-cliché rules, style recipes, and a 5-dimension critique rubric."
metadata:
  author: ConardLi
  source: https://github.com/ConardLi/web-design-skill
  vendored: SKILL.md（references/ 中的 recipe 库、失败模式清单未随仓库提供）
---

# Web Design Engineer

把一个页面从「能用」做到「有设计」。核心不是加装饰，而是在写代码之前先把设计系统说清楚，
并且对 AI 默认审美保持警惕。

## 工作流

1. **确认事实**：涉及具体品牌、产品、版本时先查证，不靠记忆编。
2. **判断是否需要问**：信息够就直接做；含糊时才问，且只问会影响结果的问题。
3. **产出 Design Read**：一句话说清产物类型、读者、视觉语言、以及五个旋钮（视觉变化 / 动效 / 信息密度 / 素材依赖 / 品牌保真）。
4. **宣告设计系统**：配色、字体、间距、圆角、阴影、动效，写成 Markdown 再动手。
5. **先给 v0**：布局 + token + 占位，让用户早纠正。
6. **完整构建**：状态、响应式、细节。
7. **验证**：按需截图或浏览器验收；交付前跑一遍自检清单。

## 反俗套（默认不要用）

- 紫粉蓝渐变、玻璃拟态堆叠
- 每张卡片都加左侧彩色边框
- emoji 当图标
- Inter / Roboto / Arial / system-ui 当标题字体（中文场景同理：不要只写 `sans-serif` 了事）
- 编造的数据、假 logo 墙、假好评
- 无意义的装饰性 SVG 插画

例外只有一个：品牌或既有设计系统本来就这样用。

## 排版要求（对中文尤其重要）

- 字号必须有**明确的层级差**：标题与正文的比例通常 2.5× 以上。
- 一套页面里字号数量控制在 5–7 个，并且每个字号有固定用途，不要「看着差不多就调一个」。
- 正文行高 1.7–1.9；中文字距默认 0，不要负字距；不要在中文里做 `letter-spacing:-0.02em`。
- 正文颜色接近纯黑，不要用灰字做正文——中文笔画密，灰字一糊就「不清楚」。
- 数字用等宽并开启 `tabular-nums`；中英混排时数字两侧留空格。
- 支持 `text-wrap: pretty` / `balance`，避免孤字。

## 评审（交付前自查）

| 维度 | 看什么 |
| --- | --- |
| 方向一致性 | 每个细节都能追溯到最初的设计方向 |
| 视觉层级 | 眯眼看，视线是否按预期流动；标题/正文比例是否够 |
| 工艺 | 对齐、间距系统、颜色数量 ≤ 4、字体家族 ≤ 2 |
| 功能性 | 每个元素删掉后设计是否变差，不变差就删 |
| 原创性 | 是否躲开了模板感 |

每项 0–10 分，总分低于 32/40 不要交付。

## 本项目已确定的取舍

- 中文正文用系统黑体栈（PingFang / 思源黑体 / 微软雅黑），不加载网络字体：GitHub Pages 上首屏更快，也不受 CDN 影响。
- 文章正文放在白色「纸」上，页面底色是浅米色——文字对比度更高，中文更清楚。
