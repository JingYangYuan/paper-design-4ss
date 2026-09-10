<p align="center">
  <img src="docs/banner.svg" alt="paper-design-4ss" width="100%">
</p>

# Paper 研究设计 4SS

社会科学论文设计路由系统。保留 FRAME、STORM、DESIGN、FULL 的拆分版操作流程；模式确认后强制确认研究取向，并在原流程内支持实证、概念/解释理论、规范理论、思想史/文本阐释与混合设计。

## 4SS 家族

| 包 | 职责 |
|---|---|
| [paper-master-4ss](https://github.com/JingYangYuan/paper-master-4ss) | 总控：登记输入、选择模块、维护工作区 |
| **[paper-design-4ss](https://github.com/JingYangYuan/paper-design-4ss)**（本仓库） | 选题、框架路由、研究设计蓝图 |
| [paper-lit-4ss](https://github.com/JingYangYuan/paper-lit-4ss) | 中英文检索、文献地图、空白与假设 |
| [paper-outline-4ss](https://github.com/JingYangYuan/paper-outline-4ss) | 素材转大纲、证据映射、缺口报告 |
| [paper-analysis-4ss](https://github.com/JingYangYuan/paper-analysis-4ss) | 定量 / 质性 / 混合，Stata · R · Python |
| [paper-write-4ss](https://github.com/JingYangYuan/paper-write-4ss) | 章节写作、润色、语言扫描、正文净稿 |
| [paper-check-4ss](https://github.com/JingYangYuan/paper-check-4ss) | 全文审稿、质量门控与精确回流 |
| [paper-submission-4ss](https://github.com/JingYangYuan/paper-submission-4ss) | Word 导出、体例、投稿清单与信函 |
| [paper-update-4ss](https://github.com/JingYangYuan/paper-update-4ss) | 待审核更新包，不直接改核心文件 |

## 它做什么

把研究主题路由到 14 个学科框架库，并在 FRAME / STORM / DESIGN / FULL 中选一条执行。模式确认后必须再确认研究取向（实证、概念/解释理论、规范理论、思想史/文本阐释、混合），不预设理论或实证。

## 四种模式

| 模式 | 用途 |
|---|---|
| FRAME | 框架锚定与学科定位 |
| STORM | 跨学科头脑风暴 |
| DESIGN | 研究设计蓝图 |
| FULL | 从框架走到完整设计 |

先读 `references/researcher-agency-overlay.md`。不自动连续推进阶段。

## 安装

将本目录放到宿主的 skill 目录。入口见 `SKILL.md`。

```bash
git clone https://github.com/JingYangYuan/paper-design-4ss.git
```

与 [`paper-master-4ss`](https://github.com/JingYangYuan/paper-master-4ss) 同级安装时，跨模块路径才能解析。只做本模块任务也可以单独使用。

## 与总控的关系

本包由总控 [`paper-master-4ss`](https://github.com/JingYangYuan/paper-master-4ss) 导出；对应源目录是总控包内的 `modules/design/`：

- 包内相对路径相对本包根目录解析
- `master/` 与部分 `references/` 是导出时的协议快照
- 更新方式：修改总控任一模块、家族表、路由或协议后，必须无参数重新导出**全部**独立包并 push 全部 GitHub 仓；不要只改本仓库，也不要只导出改过的那一个。

## License

[MIT](LICENSE)
