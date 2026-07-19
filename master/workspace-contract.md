# Workspace Contract

拆分版 paper 4SS skills 只统一输出，不统一输入。用户材料可以位于任意路径；输入路径登记后直接引用。

所有阶段核心产物默认使用中文 Markdown。凡涉及机制链、因果链、阶段流程、模块交接、理论嫁接、假设推导、写作派发、agent 调度或回流链路，必须按 `master/output-protocol.md` 内嵌 Mermaid 图示；普通证据表、模型结果和引用清单继续使用 Markdown 表格或既有导出格式。`write` 阶段的 `manuscript*.md` 与 `revisions/styled*.md` 是论文正文净稿，只允许标题层级和自然段，不得混入报告式 Markdown 装饰。用户层论文路径图按 `master/user-journey.md` 维护。

## 默认输出结构

```text
paper-workspace/
├── 00-meta/
├── 01-design/
├── 02-literature/
├── 03-outline/
├── 04-analysis/
├── 05-writing/
├── 06-submission/
├── 07-update/
├── _logs/
│   ├── agents/
│   └── runs/
└── _index/
```

## 阶段输出

| 阶段 | 默认目录 | 核心产物 |
|---|---|---|
| design | `paper-workspace/01-design/` | `design-brief.md`, `theory-map.md`, `rq-candidates.md`, `research-blueprint.md` |
| lit | `paper-workspace/02-literature/` | `search-log.md`, `paper-registry.csv`, `literature-map.md`, `gap-map.md`, `hypothesis-derivation.md` |
| outline | `paper-workspace/03-outline/` | `paper-outline.md`, `paragraph-blueprint.md`, `evidence-map.md`, `gap-report.md` |
| analysis | `paper-workspace/04-analysis/` | `analysis-plan.md`, `variable-dictionary.csv`, `tables/`, `figures/`, `reports/results-brief.md` |
| write | `paper-workspace/05-writing/` | `manuscript.md`, `manuscript-[slug]-[date].md`, `plans/`, `drafts/`, `assembly/`, `reviews/`, `revisions/styled-[slug]-[date].md`, `scans/scan-report.md` |
| submission | `paper-workspace/06-submission/` | `submission.docx`, `format-check-report.md`, `citation-normalized.md`, `citation-gap-report.md`, `submission-checklist.md`, `cover-letter.md`, `response-letter.md` |
| update | `paper-workspace/07-update/` | `update-report.md`, `review-checklist.md`, `proposed-diffs/`, `evidence/`, `merge-instructions.md` |

## 日志与索引

- 所有流程日志写入 `paper-workspace/_logs/`；顾问意见写入 `paper-workspace/_logs/agents/[module]-[YYYY-MM-DD]/`。
- 脚本、检索、导出等经研究者确认后的执行记录写入 `paper-workspace/_logs/runs/`。
- 项目状态写入 `paper-workspace/_index/project-state.md`。
- 输入登记写入 `paper-workspace/_index/input-registry.md`。
- 阶段交接写入 `paper-workspace/_index/handoff-status.md`。
- 用户层论文路径图写入 `paper-workspace/_index/paper-roadmap.md`，记录当前位置、阶段建议、最重要下一步、暂不建议事项和回流提醒。
- 研究者要求质量诊断时，可写入 `paper-workspace/_index/quality-notes.md`，保留证据缺口、失败归因和下一步修复建议。
