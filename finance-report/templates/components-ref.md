# HTML Component Quick Reference

AI生成报告时查阅此文件。每个组件给出最小HTML结构。

**规则：**
1. 照抄结构，只改内容文本和数字
2. 品牌名从 `config/output.yaml` 的 `brand.name` 读取（默认 "AnyGen Research"）
3. 示例中的 "ANYGEN RESEARCH" 替换为实际品牌名
4. 不硬编码任何用户私有信息

---

## Page Header (每页顶部)
```html
<div class="page-header">
  <div>
    <div class="brand">ANYGEN RESEARCH</div>
    <div class="brand-sub">权益研究</div>
  </div>
  <div class="meta">NVDA · Q4 FY2026<br>2026-03-04</div>
</div>
```

## Cover (封面，两种)

### 标准封面（带评级卡）
```html
<div class="cover">
  <div class="cover-body">
    <div class="ticker">NVDA</div>
    <div class="company-name">NVIDIA Corporation · NASDAQ</div>
    <div class="headline">一句话观点标题（不是主题词）</div>
    <div class="sub-headline">补充说明，2-3个关键数据点</div>
  </div>
  <div class="rating-box">
    <div class="rating-box-head">
      <div class="rating-label">ANYGEN 评级</div>
      <div class="rating-value">BUY</div>
    </div>
    <div class="rating-grid">
      <div class="rating-cell"><div class="rating-k">标签</div><div class="rating-v">值</div></div>
      <div class="rating-cell"><div class="rating-k">标签</div><div class="rating-v">值</div></div>
      <!-- 通常6-8个cell，每行2个 -->
    </div>
  </div>
</div>
```

### 简约封面（无评级卡）
```html
<div class="cover-minimal">
  <div class="headline">一句话观点标题</div>
  <div class="sub-headline">补充说明</div>
</div>
```

## KPI Strip (关键指标条)
```html
<div class="kpi-strip cols-5">  <!-- cols-3/4/5/6 -->
  <div class="kpi">
    <div class="kpi-k">标签</div>
    <div class="kpi-v pos">$68.1B</div>  <!-- pos/neg/无 -->
    <div class="kpi-note">可选注释</div>
  </div>
  <!-- 重复N个kpi -->
</div>
```
**注意：kpi-k在上，kpi-v在下。必须加cols-N class。**

## Section / Subsection
```html
<div class="section">
  <div class="section-head">1. 标题</div>
  <!-- 内容 -->
  <div class="subsection-title">子标题</div>
  <!-- 子内容 -->
</div>
```

## Tables

### 标准表格
```html
<table class="table">
  <thead><tr><th>列1</th><th class="r">数字列</th></tr></thead>
  <tbody>
    <tr><td>文本</td><td class="r">123</td></tr>
    <tr><td class="b">加粗</td><td class="r pos">+5.3%</td></tr>
  </tbody>
</table>
<div class="table-source">Source: xxx</div>
```
辅助class: `.r`右对齐 `.c`居中 `.b`加粗 `.pos`绿 `.neg`红

### 财务表格（深色表头）
```html
<table class="fin-table">
  <thead><tr><th>指标</th><th>Q1</th><th>Q2</th></tr></thead>
  <tbody>
    <tr><td>Revenue</td><td>$39.3B</td><td>$44.1B</td></tr>
    <tr class="row-total"><td>Total</td><td>$xxx</td><td>$xxx</td></tr>
  </tbody>
</table>
<div class="table-source">Source: xxx</div>
```

## Callout (提示框)
```html
<div class="callout callout-key callout-pos">  <!-- callout-pos/neg/warn/无 -->
  <div class="callout-label">标签文字</div>
  正文内容。<span class="badge-t2">T2</span>
</div>
```

## Stat Row (大数字展示)
```html
<div class="stat-row cols-4">  <!-- cols-3/4 -->
  <div class="stat">
    <div class="stat-v">36.7x</div>  <!-- stat-v pos/neg -->
    <div class="stat-k">TRAILING PE</div>
  </div>
  <!-- 重复 -->
</div>
```

## Scenario Row (情景分析)
```html
<div class="scenario-row cols-3">
  <div class="scenario" style="border-color:var(--neg);">
    <div class="scenario-title" style="color:var(--neg);">🐻 Bear</div>
    <div class="scenario-prob">假设参数</div>
    <div class="scenario-body">目标价 <strong>$75</strong> · 说明</div>
  </div>
  <!-- 重复 -->
</div>
```

## Bar Chart
```html
<div class="chart">
  <div class="chart-head">
    <div class="chart-title">标题</div>
    <div class="chart-subtitle">副标题</div>
  </div>
  <div class="bar-chart">
    <div class="bar-row">
      <div class="bar-label">标签</div>
      <div class="bar-track"><div class="bar-fill pos" style="width:78%"></div></div>
      <div class="bar-value">+24.7%</div>
    </div>
    <!-- 重复bar-row -->
  </div>
  <div class="chart-source">Source: xxx</div>
</div>
```
bar-fill class: 无(默认蓝) / `.pos`(绿) / `.neg`(红) / `.alt`(灰蓝)

## Consensus Gap (预期差异)
```html
<div class="consensus-gap">
  <div class="gap-head"><div class="gap-title">标题</div></div>
  <div class="gap-grid">
    <div class="gap-cell"><div class="gap-k">指标</div><div class="gap-v">Revenue</div></div>
    <div class="gap-cell"><div class="gap-k">我们</div><div class="gap-v">$78B</div></div>
    <div class="gap-cell"><div class="gap-k">市场</div><div class="gap-v cons">$78.4B</div></div>
    <div class="gap-cell"><div class="gap-k">差异</div><div class="gap-v delta-neg">-0.5%</div></div>
  </div>
</div>
```

## Evidence Ladder (证据分层)
```html
<div class="evidence-ladder">
  <div class="evidence-item">
    <div class="evidence-head"><span class="badge-t1">T1</span> 标题</div>
    <div class="evidence-body">内容说明</div>
  </div>
  <!-- 重复 -->
</div>
```
Badge: `.badge-t1`(蓝) `.badge-t2`(灰) `.badge-t3`(棕)

## Trigger Board (状态看板)
```html
<div class="trigger-board">
  <div class="trigger-row">
    <div class="trigger-dot on"></div>    <!-- on(绿)/watch(黄)/off(红) -->
    <div class="trigger-k">指标名</div>
    <div class="trigger-v">数值</div>
    <div class="trigger-status status-on">ACTIVE</div>  <!-- status-on/watch/off -->
  </div>
  <!-- 重复 -->
</div>
```

## Risk Matrix
```html
<table class="risk-matrix">
  <thead><tr><th>风险</th><th>级别</th><th>描述</th><th>监控</th></tr></thead>
  <tbody>
    <tr>
      <td>风险名</td>
      <td><span class="risk-level risk-high">HIGH</span></td>  <!-- risk-high/med/low -->
      <td>描述</td>
      <td>方式</td>
    </tr>
  </tbody>
</table>
```

## Quote (引用)
```html
<div class="quote">
  "引用内容"
  <div class="quote-attr">— 来源 <span class="badge-t1">T1</span></div>
</div>
```

## Disclosure (免责声明)
```html
<div class="disclosure-box">
  <div class="disclosure-title">免责声明</div>
  <p>内容</p>
</div>
```

## Page Footer
```html
<div class="page-footer">
  <p>© 2026 AnyGen Research · Generated YYYY-MM-DD</p>
</div>
```

## Exhibit Title & Source
```html
<div class="exhibit-title">Exhibit 1: 标题</div>
<!-- 图表或表格 -->
<div class="exhibit-source">Source: xxx</div>
```

## 分页
- 自然流动，**不要手动加 page-break**
- 只在确实需要新页开始时用: `<div class="page-break"></div>`
- 避免页面底部大面积空白

## 颜色语义 class
- `.pos` 绿色（正面）
- `.neg` 红色（负面）
- `.warn` 橙色（警告）
- `.muted` 灰色（次要）
- `.bold` / `.b` 加粗

## Inline Badge
```html
<span class="badge-t1">T1</span>  <!-- 一手证据 -->
<span class="badge-t2">T2</span>  <!-- 事实数据 -->
<span class="badge-t3">T3</span>  <!-- 观点推测 -->
```

## Tag
```html
<span class="tag tag-pos">利好</span>
<span class="tag tag-neg">利空</span>
<span class="tag tag-warn">警惕</span>
```
