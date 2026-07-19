# Paper Design 4SS：社会科学论文设计路由系统

**4SS** = Social Science Study Design System

一个面向社会科学研究的论文设计路由系统。将研究主题连接到 **14 个学科/领域**、**400+ 理论框架库**，按四种模式（FRAME → STORM → DESIGN → FULL）分发到具体操作阶段，并由多智能体顾问并行复核。

---

## 架构概览

```
用户输入（研究主题 + 模式 + 学科 + 期刊 + 数据）
        │
        ▼
┌─────────────────────────────────┐
│  第一层：问询用户层              │
│  解析模式 / 主题 / 学科 / 期刊   │
└─────────────────────────────────┘
        │
        ▼
┌─────────────────────────────────┐
│  第二层：限制层                  │
│  质量门控 (L0-L4) + 输出规范     │
└─────────────────────────────────┘
        │
        ▼
┌─────────────────────────────────┐
│  第三层：路由层                  │
│  WebSearch 发散关键词            │
│  → frame_locator.py 全文检索     │
│  → 学科框架库匹配                │
│  → 模式 → Phase 操作文件分发     │
└─────────────────────────────────┘
        │
        ▼
  FRAME / STORM / DESIGN / FULL
        │
        ▼
┌─────────────────────────────────┐
│  多智能体并行复核                │
│  theory / method / field /       │
│  journal-fit / critical-review   │
└─────────────────────────────────┘
```

---

## 四种模式

| 模式 | 做什么 | 输入 | 输出 |
|------|--------|------|------|
| **FRAME** | 单学科理论框架探索 | 研究主题 + 学科 | 理论定位报告 + 空白清单 + RQ 方向 |
| **STORM** | 跨学科头脑风暴 | 研究主题 + 多学科 | 理论嫁接地图 + Top 10 RQs + 评估评分卡 |
| **DESIGN** | 理论 → 研究设计蓝图 | 理论锚点 + 目标期刊 | 研究设计蓝图 + PAP 概要 |
| **FULL** | 全流程串联 | 研究主题 | 完整论文方案（理论 + 问题 + 设计 + 路线图） |

---

## 十四大学科/领域框架库

`frame/` 目录包含 14 个学科/领域的系统性理论框架，共 **400+ 理论条目**，每条含六项深度标准：

- 核心主张 + 边界条件
- 因果机制链条（含中介和调节变量）
- 关键实证证据（含效应量）
- 竞争/替代理论
- 关键论文
- 理论地位与前沿

| 学科/领域 | 文件 | 理论条目 |
|-----------|------|---------|
| 社会学 | `theory-frameworks-sociological.md` | 52 |
| 公共管理 | `theory-frameworks-public-admin.md` | 35+ |
| 心理学 | `theory-frameworks-psychology.md` | 25+ |
| 传播学 | `theory-frameworks-communication.md` | 20+ |
| 经济学 | `theory-frameworks-economics.md` | 30+ |
| 教育学 | `theory-frameworks-education.md` | 25+ |
| 政治学 | `theory-frameworks-political-science.md` | 30+ |
| 哲学 | `theory-frameworks-philosophy.md` | 60+ |
| 方法论 | `theory-frameworks-methodology.md` | 25 |
| 马克思主义 | `theory-frameworks-marxism.md` | 30 |
| 法学 | `theory-frameworks-law.md` | 15 |
| 新时代思想 | `theory-frameworks-xijinping.md` | 16 |
| 党史党建 | `theory-frameworks-party-history.md` | 18 |
| 国际政治 | `theory-frameworks-international-politics.md` | 30+ |

---

## 目录结构

```
paper-design-4ss/
├── SKILL.md                         # 主技能文件（问询层 + 限制层 + 路由层）
├── README.md                        # 本文件
├── phases/                          # 操作步骤（按模式收纳）
│   ├── 01-frame-mode.md             # FRAME: 单学科理论框架探索
│   ├── 02-storm-mode.md             # STORM: 跨学科头脑风暴
│   ├── 03-design-mode.md            # DESIGN: 理论 → 研究设计蓝图
│   ├── 04-full-pipeline.md          # FULL: 端到端全流程
│   └── 05-quality-gates.md          # 质量门控 + 输出规范
├── frame/                           # 十四大框架库
│   ├── theory-frameworks-sociological.md
│   ├── theory-frameworks-public-admin.md
│   ├── theory-frameworks-psychology.md
│   ├── theory-frameworks-communication.md
│   ├── theory-frameworks-economics.md
│   ├── theory-frameworks-education.md
│   ├── theory-frameworks-political-science.md
│   ├── theory-frameworks-philosophy.md
│   ├── theory-frameworks-methodology.md
│   ├── theory-frameworks-marxism.md
│   ├── theory-frameworks-law.md
│   ├── theory-frameworks-xijinping.md
│   ├── theory-frameworks-party-history.md
│   └── theory-frameworks-international-politics.md
├── agents/                          # 多智能体顾问定义
│   ├── theory-consultant.md         # 理论适配 / 机制链条 / 贡献空间
│   ├── method-consultant.md         # 可检验性 / 操作化 / 识别路径
│   ├── field-consultant.md          # 学科位置 / 领域贡献 / 现实意义
│   ├── journal-fit-consultant.md    # 目标期刊 / 论文类型适配
│   └── critical-review-consultant.md# 致命缺陷 / 弱论证 / 不可执行环节
├── master/                          # 总控协议
│   ├── agent-orchestration.md       # 顾问派发策略
│   ├── handoff-checklists.md        # 模块交接清单
│   ├── input-registry.md            # 输入路径登记
│   ├── output-protocol.md           # 输出规范（Markdown + Mermaid）
│   ├── routing-matrix.md            # 跨模块路由矩阵
│   ├── user-journey.md              # 用户旅程
│   └── workspace-contract.md        # 工作区契约
├── scripts/                         # 工具脚本
│   └── frame_locator.py             # AI 关键词全文检索路由
└── references/                      # 方法论参考
    ├── design-essence.md            # 研究设计决策树 + 理论-方法对齐
    ├── idea-essence.md              # RQ 生成公式库 + 五条生成路径
    ├── storm-patterns.md            # 理论嫁接策略库 + 评估协议
    ├── brainstorm-essence.md        # 跨学科头脑风暴变量体系
    ├── method-router.md             # 定量方法路由 + 诊断序列
    ├── regression-models.md         # OLS / Logistic 参考
    ├── panel-models.md              # 面板因果模型族
    ├── factor-network-bootstrap.md  # 因子分析 + 社会网络 + Bootstrap
    ├── identification-strategies.md # 因果识别策略匹配 + 稳健性方案
    ├── qualitative-methods.md       # 质性设计家族 + 编码分析
    ├── agent-registry.md            # Canonical agent 名册
    ├── agent-software-adapters.md   # 多宿主能力映射
    ├── runtime-adapter.md           # 运行时能力适配
    ├── researcher-agency-overlay.md # 研究者能动性覆盖协议
    ├── team-routing.md              # 团队路由
    ├── claude-team-config.md        # Claude Team 配置
    ├── ask-user-question-examples.md# 结构化问询示例
    └── install-dependencies.md      # 依赖安装
```

---

## 快速开始

**FRAME 模式**（找理论锚点）：

```
frame 公共管理 政策执行
```

**STORM 模式**（跨学科选题）：

```
storm 数字平台劳动治理 社会学 经济学 传播学
```

**DESIGN 模式**（出研究方案）：

```
design 教育不平等 社会学 ASR CFPS
```

**FULL 模式**（全流程）：

```
full 环境健康差异 社会学 公共管理
```

---

## 路由机制

### 关键词 → 学科路由

| 关键词 | 路由到 |
|--------|--------|
| 社会 / 阶层 / 不平等 / 制度 / 文化 / 网络 / 集体 / 规范 | 社会学 |
| 政府 / 公共 / 政策 / 行政 / 治理 / 官僚 / NGO / 公共服务 | 公共管理 |
| 心理 / 认知 / 情绪 / 人格 / 动机 / 态度 / 行为 / 偏差 | 心理学 |
| 传播 / 媒体 / 舆论 / 新闻 / 社交 / 信息 / 框架 / 议程 | 传播学 |
| 经济 / 市场 / 产业 / 价格 / 激励 / 博弈 / 供给 / 消费 | 经济学 |
| 教育 / 学校 / 学习 / 教师 / 学生 / 课程 / 高考 / 大学 | 教育学 |
| 政治 / 选举 / 民主 / 政党 / 权力 / 投票 / 立法 / 制度 | 政治学 |
| 哲学 / 伦理 / 形而上 / 认识论 / 价值 / 理性 / 公正 | 哲学 |
| 方法 / 设计 / 测量 / 信效度 / 因果 / 实验 / 准实验 | 方法论 |
| 资本 / 阶级 / 唯物 / 辩证 / 异化 / 意识形态 / 生产方式 | 马克思主义 |
| 法 / 权利 / 规范 / 合同 / 诉讼 / 司法 / 法治 / 立法 | 法学 |
| 新时代 / 中国式现代化 / 共同富裕 / 高质量发展 / 全过程人民民主 | 新时代思想 |
| 党建 / 党史 / 党规 / 全面从严治党 / 党的领导 / 组织建设 | 党史党建 |
| 国际 / 外交 / 大国关系 / 全球治理 / 国际秩序 / 地缘政治 | 国际政治 |

### 学科冗余度

部分学科之间存在高冗余度，路由时通常选其一；低冗余度学科推荐组合扫描：

- 公共管理 ↔ 政治学（高，65%）：通常选其一
- 哲学 ↔ 政治学（高，70%）：通常选其一
- 法学 ↔ 政治学（高，65%）：通常选其一
- 新时代思想 ↔ 马克思主义（高，70%）：推荐组合
- 党史党建 ↔ 新时代思想（高，75%）：推荐组合
- 社会学 ↔ 经济学（低，20%）：推荐组合
- 国际政治 ↔ 政治学（高，70%）：通常选其一

### 全文检索路由

模式确认和主题确认后，路由流程：

```
研究主题
  ↓
WebSearch 发散 3-8 个关键词（覆盖至少 2 个学科视角）
  ↓
python3 scripts/frame_locator.py --topic "..." --keywords "..."
  ↓
候选 frame + read_ranges 行号区间排序
  ↓
按行号区间读取 frame 相关段落
  ↓
design agents 复核 → 主流程确认 Top 1-3 学科
```

---

## 多智能体并行复核

跨学科头脑风暴、研究问题生成、理论框架选择、研究设计审查或 Top RQ 精炼时，必须并行派发本模块顾问：

| 触发场景 | 顾问 |
|---------|------|
| 理论框架适配、机制链条、理论贡献 | `theory-consultant` |
| 可检验性、操作化、识别路径、资料可得性 | `method-consultant` |
| 学科位置、领域贡献、现实议题意义 | `field-consultant` |
| 目标期刊或论文类型适配 | `journal-fit-consultant` |
| 致命缺陷、弱论证、不可执行环节 | `critical-review-consultant` |

主流程负责综合顾问意见，形成理论锚点、研究问题、设计蓝图和质量门控结论。所有顾问意见写入 `paper-workspace/_logs/agents/design-[YYYY-MM-DD]/`，并生成 `agent-synthesis-design-[YYYY-MM-DD].md`。

---

## 输出协议

所有报告、顾问意见、综合文件使用中文 Markdown；理论机制、研究设计流程、跨学科理论嫁接、阶段门控和 agent 派发/综合链路必须使用 Mermaid 图示，并在图后附 2-4 条中文解释。

```
paper-workspace/01-design/
├── frame-report-[discipline]-[slug]-[YYYY-MM-DD].md
├── storm-report-[slug]-[YYYY-MM-DD].md
├── design-report-[slug]-[YYYY-MM-DD].md
└── full-report-[slug]-[YYYY-MM-DD].md

paper-workspace/_logs/
└── process-log-design-[YYYY-MM-DD].md
```

---

## 质量门控

| 层级 | 门控 | 阻断规则 |
|------|------|---------|
| **L0 路由** | 学科匹配正确 + 模式合理 | 路由错误 → 中断，要求用户确认 |
| **L1 FRAME** | 理论定位充分 + 空白识别有据 | 候选理论 < 3 → 扩大搜索或切换学科 |
| **L2 STORM** | 交叉扫描多学科 + FATAL FLAW 清理 | 未覆盖 2 学科或致命缺陷未清理 → 补充/修正 |
| **L3 DESIGN** | 理论-方法对齐 + 稳健性充足 | 任何"不通过"项 → 修正后重检 |
| **L4 整体** | 实质内容 + 逻辑自洽 + 可操作 + 完整 | 任一项不满足 → 返回修正 |

---

## 边界约束

- 本技能负责**理论定位 + 选题生成 + 研究设计蓝图**，不负责论文全文写作和数据分析执行
- 理论嫁接必须有实质机制链条，禁止表面类比（"A 就像 B"）
- RQ 必须可检验，禁止无操作化路径的理论空谈
- 学科路由去重并限制：最多 3 个学科，按相关度排序
- 交叉扫描必须覆盖至少 2 个学科
- FATAL FLAW RQ 必须移出 Top 10
- 默认不自动连续推进阶段、不自动派发 agent、不自动并行复核
- 外部检索、脚本执行、导出和会改变项目状态的写入均先呈现方案、风险和证据缺口，经研究者明确确认后执行

---

## 相关 Skill

本技能是 `paper-master-4ss` 总控工作流下的设计模块。其他姊妹模块：

- `paper-lit-4ss`：文献综述与假设推导
- `paper-outline-4ss`：论文大纲与结构
- `paper-analysis-4ss`：定量/质性分析
- `paper-write-4ss`：论文写作与润色

---

## License

本仓库仅用于学术研究与教学。引用或改编请标注来源。
