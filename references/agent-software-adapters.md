# Agent Software Adapters

本文档只覆盖三类宿主：Claude Code、OpenCode、Codex。拆分版业务流程先按 `references/runtime-adapter.md` 使用通用能力名，再按下表映射到当前宿主。

## 1. 能力映射

| 通用能力 | Claude Code | OpenCode | Codex |
|---|---|---|---|
| `read_file` | Read | 文件读取或 shell `cat/sed` | 文件读取或 shell `sed` |
| `search_text` | Grep/Glob | 搜索工具或 shell `rg` | shell `rg` |
| `write_file` | Write/Edit | 文件编辑工具 | apply_patch 或文件编辑工具 |
| `run_shell` | Bash | shell/terminal | exec_command |
| `web_search` | WebSearch | 宿主搜索工具；无则记录缺失 | web search 工具；无则记录缺失 |
| `web_fetch` | WebFetch | 宿主网页读取工具；无则记录缺失 | web open/fetch 工具；无则记录缺失 |
| `ask_user` | AskUserQuestion 或直接提问 | 宿主提问能力或直接提问 | request_user_input 或直接提问 |
| `spawn_agent` | Task/subagent | OpenCode agent/subtask 能力；无则顺序复核 | Codex multi-agent/subagent 能力；无则顺序复核 |
| `parallel_review` | 多 Task 或 Agent Teams | 并行 subtask；无则 `sequential-review` | 并行 subagent；无则 `sequential-review` |
| `project_memory` | `CLAUDE.md` 标记块 | OpenCode 项目规则文件；无则 `project-rules.md` | Codex/AGENTS 项目规则文件；无则 `project-rules.md` |

## 2. Claude Code

- Claude Code 是可用宿主之一；`CLAUDE.md` 是 `project_memory` 的 Claude Code 落点。
- Agent Teams/teammate 是 Claude Code 专属高级并行形态。只有用户显式触发 Team 时，才读取 `references/claude-team-config.md` 与 `references/team-routing.md`。
- 拆分版仍受 `references/researcher-agency-overlay.md` 约束：顾问、Team、网页检索、脚本和导出均需研究者确认后执行。

## 3. OpenCode

- OpenCode 调用本 skill 时，必须先读取 `references/runtime-adapter.md` 与本文件，再按能力表执行。
- 若 OpenCode 没有可用 subagent 或并行任务能力，按派发清单顺序完成顾问复核，并在 `agent-brief.md` 与 `agent-synthesis` 记录 `sequential-review`。
- 若没有宿主项目规则文件，长期选择写入 `paper-workspace/_index/project-rules.md`，不要创建 `CLAUDE.md` 作为 OpenCode 的默认规则文件。
- 缺少某项能力时记录能力缺失或 `researcher-deferred`，不得伪造执行结果。

## 4. Codex

- Codex 调用本 skill 时，必须按 `references/runtime-adapter.md` 映射本地文件读取、`rg`、shell、web、用户确认和可用的 subagent 能力。
- 若没有可用多 agent 能力，按同一 canonical agent 清单顺序复核，并记录 `sequential-review`。
- 若没有 Codex 项目规则文件，长期选择写入 `paper-workspace/_index/project-rules.md`，不要创建 `CLAUDE.md` 作为 Codex 的默认规则文件。
- 缺少某项能力时记录能力缺失或 `researcher-deferred`，不得伪造执行结果。

## 5. 共同回退规则

- 三宿主都不得因为缺少某项能力而伪造结果；只能记录能力缺失、用户暂缓、网络不可达或顺序复核。
- CNKI、Google Scholar、Zotero MCP、浏览器操纵和网页摘要抓取必须由实际可用工具完成；普通搜索或顾问意见不能替代 CNKI 完成状态。
- 三宿主都必须保持 `paper-workspace/` 输出结构和 agent canonical name 不变；拆分版不提供总控自动化接口。
