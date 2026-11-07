# 写一篇新文章：完整工作流

这个仓库的约定：**一篇文章 = 一个自包含的 HTML 文件**。样式、脚本都内联，没有构建、没有依赖，发出去、离线打开、A4 打印都能用。

新增文章时，按下面的顺序做，不要跳步。

---

## 0. 开工前先定四件事

动手写 HTML 之前，先把这四项确定下来（缺哪项就先问，不要猜）：

| 项 | 说明 |
| --- | --- |
| 主题与结论 | 一篇文章只回答一个问题；写出那句话，再决定分几节 |
| 数据时点 | 「2026 年 11 月」这种绝对时间，写进导语区与文末 |
| 来源清单 | 每条数据对应哪个原始出处；找不到就标注为估算 |
| slug | 英文小写加连字符，如 `2026-mini-game-economy`；**发布后不再改** |

---

## 1. 建文件

```powershell
Copy-Item -Recurse articles\2026-mobile-game-metrics articles\<slug>
```

得到 `articles/<slug>/index.html`，然后整篇替换内容。不要新建一套样式——模板里的 `<style>` 与 `<script>` 直接沿用。

---

## 2. 必须改的 7 处

| # | 位置 | 改什么 |
| --- | --- | --- |
| 1 | `<head>` | `<title>`、`<meta name="description">` |
| 2 | 左栏 `.rail__brand` | 短标题（不超过 8 字）+ 副标题 |
| 3 | 左栏 `<nav>` | 每条 `<a href="#s1" data-section="s1" data-label="01 一条结论">01 一条结论</a>`：**短标签**，不是正文章节全名 |
| 4 | 导语 `<header class="hero content-section">` | eyebrow、`<h1>`、lead、补充段落、`.meta` 四项、`.stats` 五张卡 |
| 5 | 各 `<section class="content-section">` | `id` 从 `s1` 连续编号，`<h2><span class="no">01</span>完整标题</h2>` |
| 6 | 最后一节 | `<ol class="sources">` 参考资料 + 免责声明 |
| 7 | `index.html` | 列表里加一行（日期 + 标题链接 + 一句话摘要） |

`data-section` 与 `<section id>` 必须一一对应；左侧目录高亮、阅读进度、当前案例都靠它。

---

## 3. 正文组件速查（直接复制改数字）

### 章节骨架

```html
<section id="s1" class="content-section">
  <h2><span class="no">01</span>一条结论：2026 年的「及格线」</h2>
  <p>……</p>
</section>
```

### 指标卡（5 张，最多 2 张 accent）

```html
<div class="stats">
  <div class="stat">
    <div class="s-label">次留 D1<br>全市场中位数</div>
    <div class="s-value">22<span>%</span></div>
    <div class="s-foot">P25 仅 12.5%</div>
  </div>
  <div class="stat accent">
    <div class="s-label">月付费渗透率<br>全球口径</div>
    <div class="s-value">&lt;5<span>%</span></div>
    <div class="s-foot">RPG/SLG 约 1.5% 即领先</div>
  </div>
</div>
```

小于是 `&lt;`，不要在 HTML 里直接写 `<5`。

### 表格（带题注）

```html
<div class="table-wrap">
  <table>
    <caption>表 1　三条线（来源：GameAnalytics 2026 基准报告）</caption>
    <thead>
      <tr><th>指标</th><th class="num">全市场中位数</th><th class="num">头部 P99</th></tr>
    </thead>
    <tbody>
      <tr><td class="name">次留 D1</td><td class="num">22%</td><td class="num">64–68%</td></tr>
    </tbody>
  </table>
</div>
```

- 数字列加 `class="num"`（等宽、右对齐、不换行）
- 首列名称加 `class="name"`（加粗、不换行）
- `<caption>` 写「表 N　标题（来源：…）」
- 表后需要补说明时用 `<p class="small">…</p>`

### 提示块 / 术语框

```html
<div class="note">
  <span class="n-t">READ THIS FIRST</span>
  正文，可用 <b>加粗</b>。
</div>

<div class="terms">
  <span class="n-t">口径对照</span>
  「89% 付过费」与「5% 本月付费」描述的是两件事。
</div>
```

### 公式

```html
<div class="formula">
  <div class="f">月 ARPPU <span class="op">≈</span> （月流水 <span class="op">÷</span> MAU） <span class="op">÷</span> <em>月付费渗透率</em></div>
  <div class="f-note">括号内即「每 MAU 月均贡献收入」</div>
</div>
```

### 漏斗（多行衰减）

```html
<div class="funnel">
  <div class="f-row">
    <div class="f-name">全市场中位数<span>22% / &lt;4% / 0.7%</span></div>
    <div class="steps">
      <div class="step"><b>1000</b><i>新增</i></div><div class="arrow">→</div>
      <div class="step s1"><b>220</b><i>次日</i></div><div class="arrow">→</div>
      <div class="step s2"><b>40</b><i>第 7 天</i></div><div class="arrow">→</div>
      <div class="step s3"><b>7</b><i>第 30 天</i></div>
    </div>
  </div>
</div>
```

### 条形对比

`width` 按「本行数值 ÷ 本组最大值」计算，最大值那行写 `100%`。

```html
<div class="chart">
  <div class="bar-row">
    <div class="b-label">王者荣耀<span>MOBA · 高渗透低 ARPPU</span></div>
    <div class="track"><div class="fill" style="width:10.7%"></div></div>
    <div class="b-val">4.6 元</div>
  </div>
  <div class="bar-row">
    <div class="b-label">无尽冬日<span>SLG · 大 R 驱动</span></div>
    <div class="track"><div class="fill alt" style="width:100%"></div></div>
    <div class="b-val">43 元</div>
  </div>
</div>
```

### 案例卡

```html
<article class="case">
  <div class="case-top">
    <span class="case-badge">射击 · 搜打撤</span>
    <span class="case-number">案例 01 / 05</span>
  </div>
  <h3>三角洲行动</h3>
  <div class="kv">
    <dt>月流水</dt><dd>1 月 4400 万美元 → 10 月 2350 万美元（-39%）</dd>
    <dt>用户规模</dt><dd>国内 MAU 约 7000 万</dd>
  </div>
  <p><b>为什么值得看：</b>……</p>
</article>
```

`案例 01 / 05` 的分子按顺序递增、分母写总数；右下角「当前案例」提示由脚本自动跟踪。

### 列表

普通要点用 `<ul>`（方块标记、强调色），编号要点用 `ol.mis`（带编号方块，适合「五条判断」「常见误读」这类）。

```html
<ul>
  <li><strong>移动</strong>：采用 Motion Matching。</li>
  <li>命中判定使用动画通知状态配合多点扫描。</li>
</ul>
```

### 编号列表（误读、要点）

```html
<ol class="mis">
  <li><b>拿中位数当目标。</b>22% 的 D1 是全市场中位数，不是及格线。</li>
  <li><b>跨品类直接比较。</b>消除的 D30 10% 与 SLG 的 D30 5% 不是同一个含义。</li>
</ol>
```

### 参考资料

```html
<ol class="sources">
  <li>GameAnalytics，《2026 Mobile &amp; PC Gaming Benchmarks》，2026 年 8 月。<a href="https://www.gameanalytics.com/reports/2026-mobile-pc-gaming-benchmarks" target="_blank" rel="noopener noreferrer">gameanalytics.com</a></li>
</ol>
```

### 徽章（表格内标估算）

```html
<td class="num">约 2000 万 <span class="badge b-plain">估</span></td>
```

---

## 4. 数据与文字规范

- **三层标注**：可核实硬数据 / 第三方监测 / 倒推估算。估算必须写出公式与假设，并在文末免责声明里点名。
- **时点**：所有敏感数字带绝对时间（「2026 年 11 月」），不写「目前」「最近」。
- **来源**：每条数据对应 `<ol class="sources">` 里的一条；引用第三方要先说清口径（分母是谁、含不含渠道分成、iOS 还是全平台）。
- **查不到就写查不到**，不要用「业内普遍认为」替代。
- **数字格式**：中文与拉丁字母、数字之间留空格（`30 留 D30`、`MAU 2.6 亿`）；区间用 `–`；小于号用 `&lt;`。
- **不用 emoji**；不用「赋能」「抓手」「闭环」「打造」这类词。
- 写完可以用 `unslop` skill 过一遍 AI 腔。

---

## 5. 本地验收

```bash
python -m http.server 8080    # 然后打开 http://localhost:8080/
```

逐项检查：

- [ ] 左侧目录能点，点击后跳到对应章节；滚动时当前项高亮、已读项变实心点
- [ ] 阅读百分比与进度条随滚动变化；移动端顶部出现 3px 进度条
- [ ] 有案例卡时，「当前案例」提示随滚动更新
- [ ] 390px 宽下没有横向滚动；表格在自己的容器里滚动
- [ ] `Ctrl+P` 预览：左栏与提示不出现，表格不跨页
- [ ] `index.html` 里的链接能打开新文章，返回链接能回到列表

---

## 6. 提交与发布

1. `index.html` 加一行：

```html
<li class="item">
  <time datetime="2026-12-01">2026/12/01</time>
  <div>
    <a href="articles/<slug>/"><h2>文章标题</h2></a>
    <p>一句话摘要。</p>
  </div>
</li>
```

2. 提交并推送：

```bash
git add -A
git commit -m "新增：<文章标题>"
git push
```

推送后 Actions 自动发布到 `https://xuvoxuvo.github.io/game-industry-handbook/`（纯静态上传，无构建）。

---

## 7. 常见错误

| 症状 | 原因 |
| --- | --- |
| 目录点击错位 | `data-section` 与 `<section id>` 不匹配 |
| 当前章节不跟随 | 章节没有 `class="content-section"`，或没放在 `<main>` 下 |
| 案例提示不显示 | 案例卡少了 `class="case"`，或页面里没有案例 |
| 数字列换行错乱 | 漏了 `class="num"` |
| 表格撑破页面 | 漏了外层 `<div class="table-wrap">` |
| 打印出现左栏 | `.rail` 的打印隐藏规则被覆盖（改样式时注意 `@media print`） |
| 页面在 `file://` 下不工作 | 引入了外部资源；本仓库要求全部内联 |
