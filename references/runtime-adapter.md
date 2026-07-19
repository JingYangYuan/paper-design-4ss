# Runtime Adapter

本文档定义拆分版 paper 4SS skills 在 Claude Code、OpenCode 与 Codex 三类 agent 软件中的通用能力层。业务协议只引用本文件中的能力名；具体工具、项目记忆文件和多 agent 形态由 `references/agent-software-adapters.md` 映射。

## 1. 通用能力名

| 能力名 | 用途 | 缺失时处理 |
|---|---|---|
| `read_file` | 读取 `SKILL.md`、模块协议、用户材料和产物 | 停止当前步骤，请用户提供可读路径或权限 |
| `search_text` | 在 skill 包、项目目录和材料中全文检索 | 可退化为宿主可用搜索或 shell `rg`；仍不可用时记录能力缺失 |
| `write_file` | 写入 `paper-workspace/` 产物、日志、索引和项目规则 | 未获写权限时停止写入型任务 |
| `run_shell` | 执行 Python/R/Stata/pandoc/依赖检查等命令 | 只能给出待执行命令，不得声称已运行 |
| `web_search` | 在线检索关键词、核心文献和公开资料 | 记录 `web_search=能力缺失`，不得伪造搜索结果 |
| `web_fetch` | 打开网页、摘要页、API 响应或公开全文 | 无法抓取时把文献列为待核验 |
| `ask_user` | 结构化询问、确认方向、阻断确认和长期选择固化 | 无交互能力时采用最小可行默认，并记录为推断而非用户确认 |
| `spawn_agent` | 派发一个 canonical agent 顾问或 writer | 无独立 agent 能力时由主流程按角色顺序复核 |
| `parallel_review` | 多 canonical agent 并行复核或多 writer 并行草拟 | 不可并行时记录 `sequential-review` |
| `project_memory` | 持久化稳定项目规则和用户选择 | 无宿主项目记忆文件时写入 `paper-workspace/_index/project-rules.md` |

## 2. 执行规则

- 三类宿主都必须先判断自身能力，再执行模块流程；不得把某宿主专属工具名当作通用要求。
- Agent frontmatter 中的 `tools:`、模块入口中的 `tools` 或 `allowed-tools` 是 Claude Code 兼容声明；执行时必须通过本适配层映射到当前宿主能力。
- 缺少 `web_search`、`web_fetch`、`browser_control`、`spawn_agent` 或 `parallel_review` 时，必须在过程日志、`agent-brief.md`、`agent-synthesis` 或最终回复中记录能力状态和回退方式。
- 能力缺失不得改变真实性边界：不能伪造网页检索、CNKI/Scholar 页面操纵、脚本执行、统计结果或 agent 意见。
- 拆分版默认不自动派发、不自动并行、不自动连续执行阶段；这些能力只有在研究者明确同意后才作为可选执行。

## 3. Project Memory

`project_memory` 只保存稳定选择和死规则，不保存临时任务、原始隐私材料、token、cookie、日志全文或阶段待办。

优先级：

1. 当前宿主已有项目级规则文件。
2. Claude Code 的 `CLAUDE.md` paper 4SS 标记块。
3. `paper-workspace/_index/project-rules.md`。

读取时以上述顺序合并；本次用户明确指令优先于历史项目规则。写入时只更新当前宿主可安全维护的 paper-master 标记块或 `project-rules.md`，不得写入 skill 包目录。
