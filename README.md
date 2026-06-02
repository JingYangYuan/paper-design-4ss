# Paper Design 4SS：社会科学论文设计路由系统

**4SS** = Social Science Study Design System

一个面向社会科学研究的论文设计路由系统。将研究主题连接到 7 个学科、195+ 理论框架库，按四种模式（FRAME → STORM → DESIGN → FULL）分发到具体操作阶段。

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
│  关键词 → 学科框架库匹配          │
│  模式 → Phase 操作文件分发        │
└─────────────────────────────────┘
        │
        ▼
  FRAME / STORM / DESIGN / FULL
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

## 七大学科框架库

`frame/` 目录包含七个学科的系统性理论框架，共 195+ 理论条目，每条含六项深度标准：

- 核心主张 + 边界条件
- 因果机制链条（含中介和调节变量）
- 关键实证证据（含效应量）
- 竞争/替代理论
- 关键论文
- 理论地位与前沿

| 学科 | 文件 | 理论条目 |
|------|------|---------|
| 社会学 | `theory-frameworks-sociological.md` | 20+ |
| 公共管理 | `theory-frameworks-public-admin.md` | 35+ |
| 心理学 | `theory-frameworks-psychology.md` | 25+ |
| 传播学 | `theory-frameworks-communication.md` | 47+ |
| 经济学 | `theory-frameworks-economics.md` | 30+ |
| 教育学 | `theory-frameworks-education.md` | 25+ |
| 政治学 | `theory-frameworks-political-science.md` | 30+ |

---

## 目录结构

```
paper-design-4ss/
├── SKILL.md                         # 主技能文件（问询层 + 限制层 + 路由层）
├── README.md                        # 本文件
├── phases/                           # 操作步骤（按模式收纳）
│   ├── 01-frame-mode.md             # FRAME: 单学科理论框架探索
│   ├── 02-storm-mode.md             # STORM: 跨学科头脑风暴
│   ├── 03-design-mode.md            # DESIGN: 理论 → 研究设计蓝图
│   ├── 04-full-pipeline.md          # FULL: 端到端全流程
│   └── 05-quality-gates.md          # 质量门控 + 输出规范
├── frame/                           # 七大学科理论框架库
│   ├── theory-frameworks-sociological.md
│   ├── theory-frameworks-public-admin.md
│   ├── theory-frameworks-psychology.md
│   ├── theory-frameworks-communication.md
│   ├── theory-frameworks-economics.md
│   ├── theory-frameworks-education.md
│   └── theory-frameworks-political-science.md
└── references/                      # 方法论参考
    ├── idea-essence.md              # RQ 生成公式库 + 五条生成路径
    ├── brainstorm-essence.md        # 跨学科头脑风暴方法论 + 交叉扫描体系
    ├── design-essence.md            # 研究设计决策树 + 理论-方法对齐
    └── storm-patterns.md            # 理论嫁接策略库 + 评估协议 + 陷阱规避
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

## 关键词 → 学科路由

| 关键词 | 路由到 |
|--------|--------|
| 社会/阶层/不平等/制度/文化/网络/集体/规范 | 社会学 |
| 政府/公共/政策/行政/治理/官僚/NGO/公共服务 | 公共管理 |
| 心理/认知/情绪/人格/动机/态度/行为/偏差 | 心理学 |
| 传播/媒体/舆论/新闻/社交/信息/框架/议程 | 传播学 |
| 经济/市场/产业/价格/激励/博弈/供给/消费 | 经济学 |
| 教育/学校/学习/教师/学生/课程/高考/大学 | 教育学 |
| 政治/选举/民主/政党/权力/投票/立法/制度 | 政治学 |

---

## 边界约束

- 本技能负责**理论定位 + 选题生成 + 研究设计蓝图**，不负责论文全文写作和数据分析执行
- 理论嫁接必须有实质机制链条，禁止表面类比（"A 就像 B"）
- 学科路由去重并限制：最多 3 个学科，按相关度排序
- 交叉扫描必须覆盖至少 2 个学科
- FATAL FLAW RQ 必须移出候选池
