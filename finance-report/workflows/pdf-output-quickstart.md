# PDF 报告生成（快速指南）

## 核心流程

1. **读取** `config/output.yaml` — 品牌名、语言、输出路径
2. **读取** `templates/components-ref.md` — HTML组件速查表（必读！）
3. 根据分析结果组装HTML（照抄速查表结构）
4. 注入CSS → Chromium渲染PDF
5. 发送PDF（⚠️ 见下方发送规则）

## HTML生成规则

1. 照抄 `components-ref.md` 中的HTML结构，**只改文字和数字**
2. 不要发明新的class名
3. 不要手动写inline CSS，靠模板class
4. 不要手动加page-break（除非确实需要）
5. 每个数字来自 `cli.py` 工具结果，不编造
6. 品牌名从 `config/output.yaml` 的 `brand.name` 读取

## CSS注入方式

```python
import os, yaml

skill_dir = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))  # 或手动指定
config = yaml.safe_load(open(f"{skill_dir}/config/output.yaml"))
css = open(f"{skill_dir}/templates/report-style.css").read()

# HTML模板中用CSSPLACEHOLDER占位
html = html_template.replace("CSSPLACEHOLDER", css)
```

如果没有yaml库，直接读CSS文件即可，品牌名硬写"AnyGen Research"。

## HTML骨架

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head><meta charset="UTF-8"><style>CSSPLACEHOLDER</style></head>
<body>
  <!-- page-header: 见 components-ref.md -->
  <!-- cover: 标准或简约 -->
  <!-- kpi-strip cols-N -->
  <!-- section × N -->
  <!-- page-footer -->
</body>
</html>
```

## PDF渲染

```bash
chromium --headless --no-sandbox --disable-gpu \
  --print-to-pdf-no-header --no-pdf-header-footer \
  --print-to-pdf="output.pdf" "file:///path/to/report.html"
```

## ⚠️ PDF输出路径（关键！）

### 规则：必须输出到 OpenClaw workspace 下

OpenClaw 只允许发送 **workspace 目录下** 的本地文件。输出到其他目录（如 `~/reports/`）会触发 `LocalMediaAccessError` 导致发送失败。

```python
import os

# ✅ 正确：输出到 workspace/reports/
workspace = os.path.expanduser("~/.openclaw/workspace")
report_dir = os.path.join(workspace, "reports")
os.makedirs(report_dir, exist_ok=True)
output_path = os.path.join(report_dir, f"anygen-{symbol}-{report_type}-{date}.pdf")

# ❌ 错误：输出到 ~/reports/（不在允许目录内）
# output_path = os.path.expanduser(f"~/reports/anygen-{symbol}-{report_type}-{date}.pdf")
```

## ⚠️ PDF发送（关键！）

### 规则：MEDIA: 必须在极短的独立消息中发送

OpenClaw的 `MEDIA:` 指令在长消息中容易解析失败。必须分步发送：

**步骤1：先回复分析结论（纯文字）**
```
NVDA Q4 FY2026 财报分析完成，报告要点：
- Revenue $68.1B beat +2.4%
- 评级：HOLD
```

**步骤2：单独发送 MEDIA: 指令（极短消息，只有这一行）**
```
MEDIA:/home/user/.openclaw/workspace/reports/anygen-NVDA-earnings-2026-03-04.pdf
```

### ❌ 常见错误（会导致文件发不出去）

| 错误 | 说明 |
|------|------|
| 输出到 `~/reports/` | `LocalMediaAccessError`，不在允许目录 |
| MEDIA: 混在大段文字中 | 长消息中的MEDIA:会被吞掉 |
| MEDIA: 前后有大量内容 | 解析器可能跳过 |
| 连续发送多个MEDIA: | 一条消息只放一个 |

### 输出路径总结

1. **输出到** `~/.openclaw/workspace/reports/`（不是 `~/reports/`！）
2. 文件名格式: `anygen-{symbol}-{type}-{date}.pdf`
3. 发送用绝对路径（`os.path.expanduser` 展开 `~`）
4. 不硬编码任何用户路径

## 常见错误（避免！）

| 错误 | 正确 |
|------|------|
| 输出到 `~/reports/` | 输出到 `~/.openclaw/workspace/reports/` |
| `<div class="kpi-strip">` 不加cols | `<div class="kpi-strip cols-5">` |
| 自定义cover class | 用 `.cover` > `.cover-body` > `.ticker` |
| `<span>品牌名</span>` | `<div class="brand">品牌名</div>` |
| 到处加page-break | 让内容自然流动 |
| 内联style写颜色 | 用 `.pos` `.neg` `.warn` class |
| 硬编码用户路径 | 从config读取或用 `~` |

详细的组件HTML结构见 `templates/components-ref.md`。
完整的排版规范见 `workflows/pdf-output.md`。
