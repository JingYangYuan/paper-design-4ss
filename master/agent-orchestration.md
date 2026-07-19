# Agent Orchestration Protocol

本协议定义 `paper-master-4ss` 的默认顾问派发方式。总控和各模块先按 `references/runtime-adapter.md` 与 `references/agent-software-adapters.md` 确认当前宿主能力，再按本文件确定派发强度，随后读取 `master/output-protocol.md`、`references/agent-registry.md` 和目标模块的 `agents/` 文件。

## 1. 默认策略

- 默认采用丰富强制派发：除轻量任务外，每次实质性模块执行至少派发 3 个相关顾问；模块内不足 3 个顾问时派发全部顾问。
- 全流程、主题模糊、材料复杂、跨模块串联、质量风险高或用户要求“系统规划/完整检查/继续推进”时，按 `references/agent-registry.md` 的跨模块矩阵完整派发，并追加相邻模块顾问做风险预判。
- 普通 orchestration 是多 canonical agent 顾问派发；显式 Agent Team 是同一 canonical agent 的多视角辩论，二者不可互相替代。
- Agent 文件 frontmatter 中的 `tools:` 只表示 Claude Code 兼容能力别名。Claude Code、OpenCode 与 Codex 都必须经 runtime adapter 映射到 `read_file`、`search_text`、`web_search`、`web_fetch`、`spawn_agent` 等通用能力；缺少能力时按本协议记录回退，不得伪造工具结果。
- 派发前必须先规范化 agent 身份：凡用户选择、模块表格、路由矩阵或过程计划中出现短名、路径名或角色描述，都先对照 `references/agent-registry.md` 转成 agent 文件 frontmatter 的 `name:`，即 canonical agent name。`Agent Name` 是唯一执行身份；短名和 `agents/*.md` 或 sibling skill 的 `agents/*.md` 路径只作别名、阅读入口和角色协议路径。
- 规范化后的派发清单必须同时写出：用户选择或模块选择原文、canonical agent name、agent 文件路径、派发顺序、并行或 `sequential-review` 状态。实际派发不得偏离该清单；如需增删顾问，必须先更新清单并说明理由。
- **参考库回查 — 主流程预注入机制（关键）**：Agent 子进程通常运行在独立沙箱中，**无法直接访问本 skill 的 `frame/`、`references/`、`phases/` 目录**。因此，派发前主流程必须先 Read 对应参考文件，将实际内容注入 agent prompt。注入内容以 `## 参考库内容（主流程已预注入）` 标记开头。Agent 给出判断时仍需在意见开头输出 `## 参考库回查`，但此时列出的是"已使用的注入内容来源"（即主流程注入的文件路径），而非自行读取的文件路径。Agent 不得伪造"已读取"的文件列表。若注入内容不完整，Agent 应在参考回查中标注"注入内容不完整"及缺失项。

  **Design 模块 agent 预注入映射表**：

  | Agent canonical name | 主流程须预注入的参考文件（按 agent 定义中的回查清单） |
  |---|---|
  | `paper-design-theory-consultant` | frame_locator 命中的 `frame/theory-frameworks-*.md` 行号区间全文 + `references/storm-patterns.md` 嫁接策略库 + `references/design-essence.md` 理论定位部分 |
  | `paper-design-method-consultant` | `references/method-router.md` 定量方法路由 + `references/identification-strategies.md` 识别策略 + `references/design-essence.md` 操作化部分 |
  | `paper-design-field-consultant` | frame_locator 命中的 `frame/theory-frameworks-*.md` 相关理论条目 + `references/storm-patterns.md` 学科交叉部分 |
  | `paper-design-journal-fit-consultant` | 当前阶段 `phases/0*-*-mode.md` 输出规范 + `master/output-protocol.md` |
  | `paper-design-critical-review-consultant` | `references/storm-patterns.md` FATAL FLAW 标准 + `phases/05-quality-gates.md` 四层门控 + `references/design-essence.md` 对齐检查项 |

  注入内容量控制：frame 文件按 `read_ranges` 注入（50-150 行/区间）；references 注入核心条款（200-400 行/agent）。总注入量 ≤ 800 行/agent prompt。若参考文件超过此限制，优先注入与当前任务最相关的条款部分，并在注入段落中标注已省略的章节。
- Design 模块在读取 frame 前，必须先由主流程从选题中提取 3-8 个框架定位关键词，再把关键词传入 `paper-design-4ss/scripts/frame_locator.py --keywords` 查询框架库。脚本返回的候选 frame、相关度分数、命中词和 `read_ranges` 行号区间必须：①由主流程按行号区间 Read 得到 frame 实际内容，②将该内容注入 agent prompt 的参考库段落中。**禁止**只将行号区间传给 agent 而期望 agent 自行读取。
- 轻量任务可以跳过顾问，但必须在最终回复或过程日志写明 `agent-skip` 和跳过原因。
- 若当前宿主不能真实并行或没有 `spawn_agent` / `parallel_review` 能力，按同一顾问列表顺序复核，并在 `agent-brief.md`、对应顾问输出和 `agent-synthesis` 记录 `sequential-review` 与能力缺失原因。
- 所有顾问输出、综合文件和最终回复遵守 `master/output-protocol.md`：使用中文 Markdown；顾问输出、综合文件和落盘报告若涉及派发链、机制链、流程链、分歧处理链或跨模块风险链，必须加入 Mermaid 图示和 2-4 条中文解释；直接发给用户的最终回复按 `master/output-protocol.md` 第 6 节使用纯文字路径导航。

## 2. 轻量任务例外

以下任务可不派发顾问：

- 仅登记输入路径、查看项目状态或摘要已有产物。
- 单文件格式检查、依赖检查或明确的转换命令。
- 用户明确要求只回答一个事实性问题，且不进入论文流程。

例外不得用于跳过设计、文献、分析、写作或投稿的质量复核；不得用于跳过 agent 的参考库回查。

## 3. 输出落盘

每次派发顾问时创建：

```text
paper-workspace/_logs/agents/[module]-[YYYY-MM-DD]/
├── agent-brief.md
├── [agent-name].md
└── agent-synthesis-[module]-[YYYY-MM-DD].md
```

`agent-brief.md` 记录研究主题、输入路径、当前阶段、已知产物、用户约束、需要顾问判断的问题，并附规范化派发清单：用户选择或模块选择原文、canonical agent name、agent 文件路径、派发顺序、并行或 `sequential-review` 状态。**必须包含"预注入参考文件清单"**：列出每个 agent 的 prompt 中已注入的参考文件路径及注入内容行数。

每个 `[agent-name].md` 保存该顾问的原始意见，沿用顾问文件中的“参考库回查/判断/依据/风险/建议”结构。

Write 模块的 `paper-write-chapter-draft-writer` 是特殊的可重复派发 canonical writer：同一 canonical agent 可按 `writing-dispatch-plan` 的多个 `task_id` 并行或顺序执行，但每个任务必须独立落盘为 `paper-write-chapter-draft-writer--{task_id}.md`。这些 writer 输出必须经 `../paper-write-4ss/scripts/assemble_drafts.py` 拼接，生成 draft、source map 和 assembly check，并由主 agent 阅读审查后，才可进入 argument、material、style 和 chapter-reviewer 顾问链。

`agent-synthesis` 必须包含：

- 派发清单：用户选择或模块选择原文、canonical agent name、agent 文件路径、派发顺序、并行或 `sequential-review` 状态、输入摘要。
- 核心共识：哪些判断一致。
- 核心分歧：哪些判断冲突。
- 采纳决策：主流程采纳了什么。
- 未采纳理由：哪些建议暂不采纳及原因。
- 后续风险：进入下一阶段前仍需处理的问题。

`agent-synthesis` 必须使用中文 Markdown；若存在派发链、分歧处理链、跨模块风险链或回流链，必须加入 Mermaid `flowchart LR` 或 `flowchart TD` 图示，并在图后解释关键节点、采纳路径和剩余风险。

## 4. 索引更新

模块结束后，总控或模块主流程必须把以下内容写入：

- `paper-workspace/_index/project-state.md`：本次顾问派发状态、关键风险、已生成产物、下一步建议。
- `paper-workspace/_index/handoff-status.md`：进入下阶段时应交接的顾问结论和未解决风险。
- `paper-workspace/_index/paper-roadmap.md`：按 `master/user-journey.md` 更新当前位置、推荐下一步、暂不建议事项和回流提醒。

## 5. 跨模块默认链路

当用户请求全流程、继续推进、整理项目或当前阶段不清时，先确定主模块，再按相邻阶段追加顾问：

| 当前主任务 | 默认追加顾问 |
|---|---|
| 选题/设计 | lit 的 `search-strategy` 预判文献可检索性；analysis 的 `identification-model` 预判方法可行性 |
| 文献综述 | design 的 `theory-consultant` 校准理论锚点；outline 的 `structure-consultant` 预判结构承接 |
| 大纲构建 | write 的 `structure-writing` 预判写作顺序；analysis 的 `result-reporting` 预判经验章节需求 |
| 数据分析 | write 的 `argument-consultant` 预判结果声称边界；submission 的 `citation-integrity` 预判引用回流 |
| 写作润色 | submission 的 `format-check` 和 `citation-integrity` 预判投稿风险 |
| 投稿整备 | write 的 `chapter-standard-reviewer` 复核需回流正文的问题 |

跨模块顾问只做预判和风险提示，不替代主模块执行。
