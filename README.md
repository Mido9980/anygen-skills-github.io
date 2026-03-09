# AnyGen AI Skills

> AI Skills for [OpenClaw](https://github.com/openclaw/openclaw) / Claude Code / Cursor

A collection of AI-powered content generation skills using AnyGen.

## Skills Included

### 📊 Task Manager
Generate various content using AnyGen API:
- **Slides** (PPT) — Professional presentations
- **Documents** — Reports, papers, documentation
- **Websites** — Landing pages, portfolios
- **Storybooks** — Visual narratives
- **Data Analysis** — Charts and insights
- **SmartDraw** — Diagrams (professional / hand-drawn style)

## Installation

### OpenClaw
```bash
# Clone to skills directory
git clone https://github.com/AnyGenIO/anygen-skills.git ~/.openclaw/skills/anygen
```

### Claude Code
```bash
git clone https://github.com/AnyGenIO/anygen-skills.git ~/.claude/skills/anygen
```

## Configuration

### AnyGen API Key (required for Task Manager)

```bash
# Option 1: Config file
python3 anygen-suite/scripts/anygen.py config set api_key "sk-xxx"

# Option 2: Environment variable
export ANYGEN_API_KEY="sk-xxx"
```

Get your API key at [anygen.io/home](https://www.anygen.io/home?auto_create_openclaw_key=1)

## Usage

```
# Task Manager
"Make a product roadmap PPT"
"Draw a user journey whiteboard"
"Write an AI industry deep research report"
"Organize this data into a table"
"Make a quarterly review slide deck"
"Draw a microservice architecture diagram"

```

## Structure

```
anygen/
├── SKILL.md                    # Skill router
├── anygen-suite/               # AnyGen content generation
│   ├── skill.md
│   └── scripts/
│       ├── anygen.py
│       ├── render-diagram.sh
│       └── diagram-to-image.ts
└── (more skills coming soon)
```

## License

MIT
