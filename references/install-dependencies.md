# Paper Master 4SS — 依赖安装路径

本文档按模块列出 paper-master-4ss 下所有脚本、模板和运行时的外部依赖，以及各模块自带的安装说明位置。总控路由前先检查目标模块的依赖状态，缺失时引导安装。

---

## 一、总控快速检查

```bash
python3 --version    # 所有 Python 脚本的最低要求
pandoc --version     # submission 模块 Markdown → Word 导出
```

---

## 二、各模块依赖明细

### 2.1 design 模块

**路径**: ``

**依赖**: 无外部依赖。`scripts/frame_locator.py` 仅使用 Python 3 标准库（argparse, json, re, dataclasses, pathlib）。

**验收**:
```bash
python3 scripts/frame_locator.py --help
```

---

### 2.2 lit 模块

**路径**: `../paper-lit-4ss/`

**详细安装说明**: `../paper-lit-4ss/references/install-dependencies.md`

**依赖**:

| 依赖 | 用途 | 强制 |
|------|------|------|
| Chrome MCP (`chrome-devtools-mcp`) | CNKI / Google Scholar 网页操纵 | 是 |
| Google Chrome（可见桌面窗口） | CNKI 检索、验证码处理 | 是 |
| Zotero Desktop + Connector | 本地文献库保存与去重 | 否 |
| Zotero MCP | 代理直接搜索 Zotero、读取全文 | 否 |

**快速检查**:
```bash
npx -y chrome-devtools-mcp@latest --help >/dev/null
```

---

### 2.3 outline 模块

**路径**: `../paper-outline-4ss/`

**依赖**: 无外部依赖。纯 Markdown 处理，不包含脚本或运行时。

**验收**:
```bash
test -f ../paper-outline-4ss/SKILL.md
test -f ../paper-outline-4ss/references/outline-patterns.md
test -f ../paper-outline-4ss/references/output-formats.md
```

---

### 2.4 analysis 模块

**路径**: `../paper-analysis-4ss/`

**三语言模板各自依赖，按用户所选语言按需安装：**

#### Python 模板 (`templates/python-analysis-template.py`)

| 包 | 用途 | 强制 |
|----|------|------|
| numpy, pandas | 数据处理 | 是 |
| scipy | 统计检验 | 是 |
| statsmodels | 回归诊断、Logit/Probit/Poisson/Tobit/Heckman | 是 |
| linearmodels | 面板 FE/RE/GMM、IV/2SLS | 否（面板/IV 时必装） |
| matplotlib, seaborn | 图形导出 | 否（出图时必装） |

```bash
python3 -m pip install --user numpy pandas scipy statsmodels
# 面板/IV 分析追加:
python3 -m pip install --user linearmodels
# 出图追加:
python3 -m pip install --user matplotlib seaborn
```

#### R 模板 (`templates/r-analysis-template.R`)

| 包 | 用途 | 强制 |
|----|------|------|
| ggplot2, dplyr, tidyr, tibble, purrr, readr | 核心数据处理与绑图 | 是 |
| haven, readxl | 读取 Stata/Excel 数据 | 否 |
| fixest, lfe | 高维固定效应 | 否（面板时推荐） |
| AER, ivreg | IV/2SLS | 否 |
| MatchIt, cobalt | PSM/CEM | 否 |

```r
install.packages(c("ggplot2", "dplyr", "tidyr", "tibble", "purrr", "readr"))
```

#### Stata 模板 (`templates/stata-analysis-template.do`)

| 包 | 用途 | 强制 |
|----|------|------|
| outreg2 / estout | 回归表导出 | 是 |
| reghdfe | 高维固定效应 | 否（FE 时必装） |
| ivreg2 | IV/2SLS 诊断 | 否（IV 时必装） |
| psmatch2 | PSM | 否 |

```stata
ssc install outreg2
ssc install estout
ssc install reghdfe
ssc install ivreg2
```

详细安装、镜像配置、验收命令和故障排除见各语言专属文档：

| 语言 | 文档 |
|------|------|
| Python | `../paper-analysis-4ss/references/python-ecosystem-setup.md` |
| R | `../paper-analysis-4ss/references/r-ecosystem-setup.md` |
| Stata | `../paper-analysis-4ss/references/stata-ecosystem-setup.md` |

---

### 2.5 write 模块

**路径**: `../paper-write-4ss/`

**依赖**: 无外部依赖。以下四个脚本均仅使用 Python 3 标准库：

| 脚本 | 用途 |
|------|------|
| `scripts/complexity_analyzer.py` | 中文社科文本复杂度诊断 |
| `scripts/writing_scanner.py` | 中文学术写作 25 条反模式扫描 |
| `scripts/method_router.py` | 研究方法类型识别与路由 |
| `scripts/example_extractor.py` | 范文按需截取 |

**验收**:
```bash
python3 ../paper-write-4ss/scripts/complexity_analyzer.py --help
python3 ../paper-write-4ss/scripts/writing_scanner.py --help
python3 ../paper-write-4ss/scripts/method_router.py --help
python3 ../paper-write-4ss/scripts/example_extractor.py --help
```

---

### 2.6 submission 模块

**路径**: `../paper-submission-4ss/`

**详细安装说明**: `../paper-submission-4ss/references/install-dependencies.md`

**依赖**:

| 依赖 | 用途 | 强制 |
|------|------|------|
| Python 3 | 所有脚本运行 | 是 |
| pandoc | Markdown → Word 导出 | 否（仅导出时） |
| python-docx | Word 格式检查、reference docx 清洗 | 否（仅格式检查时） |
| lxml | docx XML 处理 | 否（仅格式检查时） |

**安装（macOS）**:
```bash
brew install pandoc
python3 -m pip install --user python-docx lxml
```

**验收**:
```bash
python3 ../paper-submission-4ss/scripts/export_docx.py --help
python3 ../paper-submission-4ss/scripts/check_docx_format.py --help
python3 ../paper-submission-4ss/scripts/sanitize_reference_docx.py --help
python3 ../paper-submission-4ss/scripts/check_citations.py --help
```

---

### 2.7 update 模块

**路径**: `../paper-update-4ss/`

**依赖**: 无外部依赖。纯 agent 派发，不包含脚本或运行时。

**验收**:
```bash
test -f ../paper-update-4ss/SKILL.md
```

---

## 三、一键验收脚本

```bash
#!/bin/bash
# paper-master-4ss 全模块依赖验收
# 从 paper-design-4ss/ 根目录执行

SKILL_ROOT="$(cd "$(dirname "$0")" && pwd)"
cd "$SKILL_ROOT"

echo "=== Python ==="
python3 --version || echo "MISSING: python3"

echo ""
echo "=== pandoc ==="
pandoc --version 2>/dev/null | head -1 || echo "MISSING: pandoc"

echo ""
echo "=== design ==="
python3 scripts/frame_locator.py --help >/dev/null 2>&1 && echo "OK" || echo "MISSING"

echo ""
echo "=== lit ==="
test -f ../paper-lit-4ss/SKILL.md && echo "lit/SKILL.md OK"
npx -y chrome-devtools-mcp@latest --help >/dev/null 2>&1 && echo "Chrome MCP OK" || echo "Chrome MCP NOT FOUND"

echo ""
echo "=== outline ==="
test -f ../paper-outline-4ss/SKILL.md && echo "outline/SKILL.md OK"

echo ""
echo "=== analysis ==="
python3 -c "
import importlib, sys
for pkg in ['numpy','pandas','scipy','statsmodels']:
    try:
        importlib.import_module(pkg)
        print(f'{pkg} OK')
    except ImportError:
        print(f'{pkg} MISSING')
" || echo "analysis/Python check failed"

echo ""
echo "=== write ==="
python3 ../paper-write-4ss/scripts/complexity_analyzer.py --help >/dev/null 2>&1 && echo "complexity_analyzer OK"
python3 ../paper-write-4ss/scripts/writing_scanner.py --help >/dev/null 2>&1 && echo "writing_scanner OK"

echo ""
echo "=== submission ==="
python3 -c "
import importlib
for pkg in ['docx','lxml']:
    try:
        importlib.import_module(pkg)
        print(f'{pkg} OK')
    except ImportError:
        print(f'{pkg} MISSING')
" || echo "submission/Python check failed"
python3 ../paper-submission-4ss/scripts/export_docx.py --help >/dev/null 2>&1 && echo "export_docx OK"

echo ""
echo "=== update ==="
test -f ../paper-update-4ss/SKILL.md && echo "update/SKILL.md OK"

echo ""
echo "=== DONE ==="
```

---

## 四、模块级安装说明索引

各模块如需更详细的安装指引（如 Chrome MCP 配置、Zotero MCP 环境变量、pandoc 模板调试），直接读取模块自己的安装文档：

| 模块 | 详细安装说明 |
|------|-------------|
| lit | `../paper-lit-4ss/references/install-dependencies.md` |
| submission | `../paper-submission-4ss/references/install-dependencies.md` |

其余模块（design / outline / analysis / write / update）仅有本文档中的依赖声明，不设独立安装说明。
