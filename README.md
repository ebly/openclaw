# OpenClaw 配置与技能

这是我的 OpenClaw 个性化配置项目，包含多个 AI 助手 agent、自定义技能、定时任务和团队协作配置。

## 📋 目录

- [项目概述](#项目概述)
- [Agent 团队](#agent-团队)
- [技能集合](#技能集合)
- [定时任务](#定时任务)
- [通道配置](#通道配置)
- [项目结构](#项目结构)
- [快速开始](#快速开始)

## 📖 项目概述

OpenClaw 是一个强大的 AI 助手框架，本项目配置了完整的 AI 团队，支持飞书消息通道，实现了跨 agent 协作、定时任务播报等功能。

**主要特性：**
- 🔀 跨 agent 通信与协作
- 📅 定时任务调度（天气、新闻播报）
- 💬 飞书消息通道集成
- 🛠️ 自定义技能扩展
- 🤖 多模型支持（通义千问、GLM、Kimi）

## 👥 Agent 团队

### 主要成员

| Agent | 角色 | Workspace | 特点 |
|-------|------|-----------|------|
| **main** (小二) | 私人助理 / 团队大脑 | workspace | 默认助手，负责协调和日常任务 |
| **designer** (美美) | 首席设计师 | workspace-designer | 设计、创意、视觉相关任务 |
| **coder** (老张) | 资深程序员 | workspace-coder | 编码、技术实现、调试 |
| **test** (玲子) | 测试专员 | workspace-test | 质量保证、测试、验证 |
| **support** (小刘) | 后勤专员 | workspace-support | 文档、整理、辅助工作 |

### 通道绑定

每个 agent 都有对应的飞书账号：

- `default` → main (小二)
- `meimei` → designer (美美)
- `laozhang` → coder (老张)
- `lingzi` → test (玲子)
- `xiaoliu` → support (小刘)

## 🎯 技能集合

### 核心技能

- **cross-session-chat** - 跨会话交流，实现 agent 之间的消息传递
- **name-recognition** - 机器人名字识别，避免误响应
- **ontology** - 本体构建，建立知识结构
- **proactive-agent** - 主动型 AI，预判需求、主动建议
- **self-improving** - 自我提升，持续学习和优化
- **response-timing** - 判断回应时机，智能沉默
- **team-communication** - 团队内部沟通技能

### 扩展技能

- **search** - 网络搜索技能，查找信息和研究话题
- **weather-cn** - 中文天气播报，使用 wttr.in
- **humanize-ai-text** - AI 文本人性化处理
- **xiaohongshu** - 小红书内容工具

## ⏰ 定时任务

配置的定时任务（通过 cron/jobs.json）：

1. **天气播报** - 每天 08:00 自动播报武汉天气
   - 执行者：main (小二)
   - 发送到：飞书私聊

2. **热点新闻** - 每天 08:00 播报 3-5 条热点新闻
   - 执行者：main (小二)
   - 发送到：飞书私聊

## 💬 通道配置

### 飞书集成

- **连接模式**：WebSocket
- **群组策略**：Open（开放模式）
- **会话范围**：按群组
- **账号配置**：5 个独立飞书应用账号

## 📁 项目结构

```
.openclaw/
├── agents/              # Agent 配置目录
│   ├── main/           # 小二配置
│   ├── designer/       # 美美配置
│   ├── coder/          # 老张配置
│   ├── test/           # 玲子配置
│   └── support/        # 小刘配置
├── skills/             # 自定义技能
│   ├── cross-session-chat/
│   ├── name-recognition/
│   ├── ontology/
│   ├── proactive-agent/
│   └── ...
├── cron/               # 定时任务
│   ├── jobs.json       # 任务配置
│   └── jobs.json.bak   # 备份
├── feishu/             # 飞书插件数据
│   └── dedup/          # 去重配置
├── completions/        # Shell 自动补全脚本
│   ├── openclaw.bash
│   ├── openclaw.zsh
│   └── openclaw.ps1
├── identity/           # 设备身份信息
└── openclaw.json       # 主配置文件
```

## 🚀 快速开始

### 环境要求

- Node.js >= v24
- OpenClaw >= 2026.3.2
- 飞书开发者账号

### 安装步骤

1. **克隆仓库**
   ```bash
   git clone https://github.com/ebly/openclaw.git
   cd openclaw
   ```

2. **安装依赖**
   ```bash
   npm install
   ```

3. **配置环境**
   - 复制 `openclaw.json` 并根据需要修改
   - 配置飞书应用的 App ID 和 App Secret

4. **启动 Gateway**
   ```bash
   openclaw gateway start
   ```

5. **测试连接**
   ```bash
   openclaw status
   ```

### 常用命令

```bash
# 查看 Gateway 状态
openclaw gateway status

# 启动/停止/重启
openclaw gateway start|stop|restart

# 列出 agents
openclaw agent list

# 发送测试消息
openclaw agent send --agent main "测试消息"

# 查看 cron 任务
openclaw cron list
```

## 📝 配置说明

### 模型配置

支持多种模型（通过 `openclaw.json` 配置）：

- **通义千问系列**：qwen3.5-plus, qwen3-max, qwen3-coder-next, qwen3-coder-plus
- **GLM 系列**：glm-5, glm-4.7
- **Kimi 系列**：kimi-k2.5

### Agent 间通信

启用 agent-to-agent 通信，支持以下 agents：
- main, meimei, laozhang, lingzi, xiaoliu

## 🔐 安全说明

本项目使用 `.gitignore` 排除敏感内容：

- ❌ 不包含：credentials/, logs/, sessions/, device auth tokens
- ✅ 包含：agents 配置、技能定义、定时任务配置

**注意**：部署前请检查并替换所有敏感信息（API keys、tokens 等）。

## 📄 许可证

MIT License

## 👤 作者

ebly

## 🙏 致谢

- [OpenClaw](https://github.com/openclaw/openclaw) - 强大的 AI 助手框架
- 飞书开放平台
- 所有贡献者

---

💰 **OpenClaw 让 AI 助手更强大！**