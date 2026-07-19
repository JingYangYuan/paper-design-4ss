# Routing Matrix

先判断用户目标，确定一个主模块，再按 `master/agent-orchestration.md` 决定是否追加相邻模块顾问。不要把全部业务模块一次性读入上下文；跨模块任务先加载主模块，再加载必要顾问文件做风险预判。

| 用户意图 | 内部模块 | 入口 |
|---|---|---|
| 选题、理论锚点、研究问题、研究设计、PAP | design | `SKILL.md` |
| 文献检索、文献综述、文献地图、研究空白、假设推导、CNKI/Scholar | lit | `../paper-lit-4ss/SKILL.md` |
| 已有材料转论文结构、大纲、证据映射、缺口报告 | outline | `../paper-outline-4ss/SKILL.md` |
| 数据清洗、描述统计、回归诊断(VIF/BP/DW/Hausman/弱IV/过度识别)、基准回归、Logit/Probit/Poisson/Tobit/Heckman、面板FE/RE/动态GMM、IV/2SLS/GMM、DID/事件研究/多期DID(交错处理)、RDD(局部平滑性/安慰剂/带宽)、PSM/CEM/IPW、SCM/SDID、分位数、中介/调节、时间序列(ARMA/VAR/VECM)、空间计量(SAR/SDM/SEM)、Bootstrap/稳健性、质性编码、混合方法。三语言模板(Stata/R/Python)自含完整可执行代码。 | analysis | `../paper-analysis-4ss/SKILL.md` |
| 正文写作、章节改写、润色、语言扫描、复杂度诊断 | write | `../paper-write-4ss/SKILL.md` |
| 投稿前检查、Markdown 转 Word、Word 模板对照、参考文献 GB/T 7714、APA 与中文社会学体例整理、cover letter、response letter、审稿回应 | submission | `../paper-submission-4ss/SKILL.md` |
| 更新知识边界、补充理论框架、补充写作范式、补充方法/流程协议、补充工具模板、从书籍/论文/笔记/方法手册/工具日志吸收知识，或为 update 模块自身生成待审核更新包 | update | `../paper-update-4ss/SKILL.md` |
| 不知道下一步、整理项目状态、串联全流程 | master | 先读 `_index/paper-roadmap.md`、`_index/project-state.md` 与 `_index/handoff-status.md`，再按缺口路由，并默认规划 design → lit → outline → analysis/write 的顾问预判链路 |

## 优先级

1. 用户明确指定模块时，按指定模块执行。
2. 用户给出材料但目标不明时，先登记输入，再扫描 `project-state.md` 判断阶段。
3. 用户说“继续”“下一步”“整理一下”时，先读 `_index/paper-roadmap.md`、`_index/project-state.md` 与 `_index/handoff-status.md`；若路线图缺失，则按 `master/user-journey.md` 根据现有索引和产物补建。
4. 如果缺少研究主题或任务目标，先简短询问；如果可从项目状态推断，则不问。

## 顾问派发例外

路径登记、已有产物摘要、依赖检查、单文件格式检查和明确的单点转换任务可不派发 agent，但必须在日志或最终回复中记录 `agent-skip` 和原因。除此之外，每次实质性模块执行至少派发 3 个相关顾问；全流程、材料复杂或阶段不清时按 `references/agent-registry.md` 的矩阵完整派发，并追加相邻模块风险预判。

## 跨模块默认链路

- 全流程规划：design 主导，追加 lit/search-strategy、outline/structure、analysis/identification-model、write/structure-writing 做预判。
- 文献到大纲：lit 主导，追加 outline/structure 和 outline/evidence-map 预判结构承接。
- 分析到写作：analysis 主导，追加 write/argument 和 write/material-integration 预判结果声称边界。
- 写作到投稿：write 主导，追加 submission/format-check 和 submission/citation-integrity 预判投稿风险。
