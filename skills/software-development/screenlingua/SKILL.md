---
name: screenlingua
description: 本地截图翻译桌面应用（OCR + 翻译全在本地完成）。React + Tauri + Python FastAPI sidecar。
task: 接手开发 ScreenLingua 项目，按 P0→P1→P2→P3 优先级推进
---

# ScreenLingua

> 项目根目录：`C:\Users\<用户名>\Documents\Codex\Screen-Translation-Assistant\`

## 技术栈

| 层 | 技术 | 端口 |
|----|------|------|
| 前端 | React + Vite + TypeScript | 5173 |
| 桌面端 | Tauri (Rust) | — |
| Sidecar | Python FastAPI | 8765 |
| OCR | RapidOCR (本地) | — |
| 翻译 | Argos Translate (本地), en→zh 模型已装 | — |
| 术语表 | 49 词条 + 12 品牌替换, `config/glossary.zh-CN.json` | — |

## 常用命令

```bash
pnpm sidecar:ensure           # 启动 Python sidecar (8765)
pnpm dev:compat               # 启动 Vite 前端 (5173)
pnpm services:status          # 检查 sidecar + 前端状态
pnpm check                    # tsc --noEmit 类型检查
pnpm build:compat             # vite build
pnpm test:local-flow          # 全链路测试
pnpm tauri:dev                # Tauri 开发模式（需 Rust + VS Build Tools）
```

## 待完成任务

### P0 — 桌面环境就绪
- [ ] 安装 winget → Rust/Cargo → VS Build Tools C++
- [ ] 跑通 `pnpm tauri:dev`

### P1 — 核心功能完善
- [ ] 真机测试：窗口、侧栏、深色模式、医学词条、清理缓存
- [ ] 区域选择覆盖层（拖拽框选）
- [ ] 固定区域管理
- [ ] 历史页接真实 SQLite
- [ ] 术语库搜索/导入/导出/恢复默认
- [ ] 设置页：模型状态、数据目录、日志目录、缓存容量

### P2 — 数据边界与打包
- [ ] 统一路径管理模块
- [ ] 启动时数据目录体检
- [ ] 清理策略
- [ ] `pnpm tauri:build` 打包安装版

### P3 — 质量与体验
- [ ] 前端冒烟测试 / sidecar API 回归测试
- [ ] 友好错误提示
