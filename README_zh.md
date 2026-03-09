# AnyGen AI Skills

> 适用于 [OpenClaw](https://github.com/openclaw/openclaw) / Claude Code / Cursor 的 AI 技能包

## 包含技能

### 📊 Task Manager — 通用内容生成
使用 AnyGen API 生成 PPT、文档、网站、故事板、数据分析、图表。任务完成后自动下载文件到本地。

## 安装

```bash
# OpenClaw
git clone https://github.com/AnyGenIO/anygen-skills.git ~/.openclaw/skills/anygen

# Claude Code
git clone https://github.com/AnyGenIO/anygen-skills.git ~/.claude/skills/anygen
```

## 配置

```bash
# AnyGen API Key（Task Manager 需要）
python3 anygen-suite/scripts/anygen.py config set api_key "sk-xxx"

# 或环境变量
export ANYGEN_API_KEY="sk-xxx"
```

API Key 获取：[anygen.io/home](https://www.anygen.io/home?auto_create_openclaw_key=1)

## 使用

```
# 内容生成
"做一个产品Roadmap ppt"
"画一个用户旅程的白板图"
"写一份AI行业深度调研报告"
"把这份数据整理成表格"
"画一个微服务架构图"

```
