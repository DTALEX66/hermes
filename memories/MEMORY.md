# Hermes Agent 跨会话记忆（参考文件）
# 部署到新电脑后，Agent 会逐步积累新的记忆
# 此文件仅作为参考，了解之前的记忆结构

## ScreenLingua 项目
- 位置：~/Documents/Codex/Screen-Translation-Assistant/
- 技能：screenlingua（software-development 分类）
- 技术栈：React + Tauri + Python FastAPI sidecar（8765 端口），前端 5173
- 状态：sidecar 健康、OCR/翻译可用、术语表就绪
- 待办：P0（Rust/Cargo/VS Build Tools + tauri:dev）→ P1（覆盖层、区域管理、SQLite 历史）

## Cognitive-OS 项目
- 位置：~/Cognitive-OS（分支：codex/integrate-cognitive-runtime）
- 工作流：.venv/Scripts/python.exe 执行一切命令
- 测试：unittest discover -s tests
- 编译：compileall
- 诊断：scripts/doctor_environment.py --fix --check-files
- 项目根有 AGENTS.md，包含严格的数据边界和 Git 规则

## Obsidian 知识库项目
- 位置：E:/BaiduSyncdisk/Obsidian知识库/
- 工作区：C:/Users/ALEX/Documents/Codex/2026-06-28/files-mentioned-by-the-user-obsidian/
- 项目：把 E 盘课程资料自动拆解总结录入 Obsidian 知识库
- 第一课《知识内化训练营》已全部完成
- Obsidian 配置：19 个插件（dataview/templater/tasks/omnisearch/text-extractor/git 等）
- 3 个 CSS 片段，Minimal 主题，accentColor=#0071e3

## Aether-Radar 项目
- 位置：~/Aether-Radar/（分支：codex/consolidate-warehouse-projects）
- 技术栈：Next.js + Docker + MCP Server + PostgreSQL
- GitHub：github.com/DTALEX66/Aether-Radar
- 验证命令：check_encoding_syntax.py → validate_data.py → ten_round_self_check.py → cd next-app && npm run typecheck && npm run lint && npm run build:ci

## 通用注意事项
- AGENTS.md 在 Documents\Codex\AGENTS.md
- BOM 问题：百度网盘 YunDetectService 会为 JSON 注入 BOM
- 写入 E 盘用 Python（Node.js REPL 会 EPERM）
- PowerShell 5.1 不支持 && 和 utf8BOM，用 UTF8 参数
