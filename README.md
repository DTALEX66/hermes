# Hermes Agent 部署包

> 一键将 Hermes Agent 配置/技能/插件迁移到新电脑

## 📦 目录结构

```
hermes-pack/
├── config/
│   ├── config.yaml          ← Hermes 完整配置（密钥已剔除）
│   └── SOUL.md              ← Agent 人格/身份设定
├── skills/
│   └── software-development/
│       ├── screenlingua/         ← 截图翻译项目技能
│       ├── python-testing/       ← Python 测试约定
│       └── windows-development/  ← Windows 开发环境排坑
├── memories/
│   └── MEMORY.md            ← 跨会话记忆参考（仅供参考）
├── setup.ps1                ← 一键部署脚本（Windows）
├── setup.sh                 ← 一键部署脚本（Linux/macOS）
└── README.md                ← 本文件
```

## 🚀 快速部署

### Windows

以**管理员身份**打开 PowerShell，执行：

```powershell
# 克隆本仓库
cd ~
git clone git@github.com:DTALEX66/hermes.git
cd hermes

# 一键部署
.\setup.ps1

# 或预览模式（不实际执行）
.\setup.ps1 -DryRun
```

### Linux / macOS

```bash
git clone git@github.com:DTALEX66/hermes.git
cd hermes
chmod +x setup.sh
./setup.sh
```

## 📋 部署内容

脚本会自动完成以下操作：

| # | 步骤 | 说明 |
|---|------|------|
| 1 | 安装 Hermes Agent | 通过 winget 或 pip |
| 2 | 写入 config.yaml | 模型、显示、工具、安全等全部配置 |
| 3 | 写入 SOUL.md | 中文人格设定 |
| 4 | 安装本地技能 | screenlingua / python-testing / windows-dev |
| 5 | 安装 Python 依赖 | `ddgs`（DuckDuckGo 搜索库） |
| 6 | 启用工具集 | x_search / video / spotify |
| 7 | 启用插件 | disk-cleanup / google_meet / security-guidance / web-ddgs |

## 🔑 部署后手动配置

部署完成后，需手动设置以下内容：

### 1. API Key

在 `%LOCALAPPDATA%\hermes\.env` 中添加：

```env
DEEPSEEK_API_KEY=你的deepseek密钥
```

如果使用其他模型提供商，添加对应的环境变量：
- `ANTHROPIC_API_KEY` — Claude
- `OPENAI_API_KEY` — OpenAI
- `OPENROUTER_API_KEY` — OpenRouter
- `GOOGLE_API_KEY` — Gemini

### 2. 选择模型

```bash
hermes model
```

### 3. Spotify（可选）

```bash
hermes auth spotify
```

### 4. 加载项目技能

```bash
# 加载 ScreenLingua 技能
hermes -s screenlingua

# 或通过技能查看
skill_view(name='screenlingua')
```

### 5. 重启 Hermes

关闭并重新打开 Hermes，或在新会话中 `/reset` 使所有插件生效。

## 🛠️ 查看当前配置

```bash
hermes config               # 查看完整配置
hermes config path          # 查看配置路径
hermes skills list          # 查看已安装技能
hermes plugins list         # 查看已安装插件
hermes tools list           # 查看已启用工具集
hermes doctor               # 环境健康检查
```

## ❌ 已剔除的内容（需在新电脑重新配置）

以下内容**不包含**在此部署包中，需手动设置：

- API 密钥（`.env` 文件）
- OAuth 令牌（`auth.json`）
- 会话历史（`state.db`）
- cron 作业运行时数据
- 缓存文件和日志

## 📝 备注

- 所有内置技能（62 个）由 Hermes 自动安装，无需手动处理
- 部署包仅包含本地创建的自定义技能（3 个）
- 不同电脑的用户名不同时，需调整 `config.yaml` 中的路径
- 建议部署后运行 `hermes doctor` 做一次全面检查
