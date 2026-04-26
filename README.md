# PostDocReport - 浙江大学博士后研究报告 LaTeX 模板

## 项目简介

本项目是一个用于撰写浙江大学博士后研究报告的 LaTeX 模板。模板遵循全国博士后管委会办公室发布的《博士后研究报告编写规则》，并针对浙江大学博士后研究报告格式要求进行了适配和优化，提供了完整的文档结构和格式示例。

## 致谢

本模板的格式和内容参考了 Overleaf 上的《博士后研究报告模板》，在此基础上针对浙江大学博士后研究报告格式要求进行了修改和适配。感谢原模板作者的贡献。

- 原模板来源：[Overleaf - 博士后研究报告模板](https://www.overleaf.com/)

本模板基于 CTEX 宏包的 ctexbook 文档类开发，感谢 CTEX.ORG 的贡献。

## 文件结构

```
PostDocReport/
├── PostDocReport.tex    # 主文件，包含文档类声明和封面信息
├── PostDocRep.cls       # 文档类文件
├── PostDocRep.cfg       # 配置文件
├── gbt7714.sty          # 国标参考文献格式宏包
├── gbt7714-*.bst        # 国标参考文献样式文件
├── black_logo.png       # 封面logo图片
├── chapter/             # 章节文件目录
│   ├── abstract.tex     # 中文摘要和英文摘要
│   ├── chap-intro.tex   # 第一章：引言
│   ├── chap-method.tex  # 第二章：研究方法示例章
│   ├── chap-experiment.tex # 第三章：实验研究示例章
│   ├── chap-analysis.tex  # 第四章：数值分析示例章
│   ├── chap-discussion.tex # 第五章：结果讨论示例章
│   ├── chap-conclusion.tex # 第六章：结论与展望
│   ├── thanks.tex       # 致谢
│   ├── pub.tex          # 科研成果清单
│   ├── resume.tex       # 个人简历
│   └── chap-req.tex     # 编写规则说明（可选）
├── figures/             # 图片目录（示例图片）
├── bib/                 # 参考文献
│   └── tex.bib          # 参考文献数据库
└── README.md            # 本说明文件
```

## 环境配置

### 推荐编译环境

| 项目 | 推荐版本 |
|------|----------|
| **TeX 发行版** | TeX Live 2023 或更高版本 |
| **编译引擎** | XeLaTeX（推荐，支持中文字体） |
| **BibTeX** | BibTeX 0.99d 或 biber |
| **latexmk** | Version 4.83 或更高版本 |

### 查看本地环境版本

```bash
# 查看 XeLaTeX 版本
xelatex --version

# 查看 BibTeX 版本
bibtex --version

# 查看 latexmk 版本
latexmk --version

# 查看 TeX Live 发行版信息
tex --version
```

### 系统要求

- **Linux**: TeX Live 2023+（推荐通过 `sudo apt install texlive-full` 安装）
- **Windows**: TeX Live 2023+ 或 MiKTeX
- **macOS**: MacTeX 2023+

### 必需宏包

模板依赖以下宏包（TeX Live 完整安装通常已包含）：

- `ctex` - 中文支持
- `gbt7714` - 国标参考文献格式
- `fancyvrb` - 代码块
- `algorithm`, `algpseudocode` - 算法伪代码
- `booktabs`, `array`, `multirow` - 表格增强
- `graphicx`, `subcaption` - 图片支持

## 编译方法

本模板支持 XeLaTeX 和 pdfLaTeX 编译。推荐使用 XeLaTeX 以获得更好的中文支持。

### 编译顺序说明

LaTeX 文档涉及参考文献时，需要多次编译才能正确生成：

```
1. xelatex PostDocReport.tex   → 生成 .aux 文件（包含引用信息）
2. bibtex PostDocReport        → 处理参考文献，生成 .bbl 文件
3. xelatex PostDocReport.tex   → 整合参考文献到文档
4. xelatex PostDocReport.tex   → 更新交叉引用，最终确认
```

### XeLaTeX 编译步骤（手动）

```bash
xelatex PostDocReport.tex
bibtex PostDocReport
xelatex PostDocReport.tex
xelatex PostDocReport.tex
```

### XeLaTeX 编译步骤（一键命令）

推荐使用 latexmk 自动管理编译流程：

```bash
# 清理旧的编译文件（如有问题时执行）
latexmk -xelatex -C PostDocReport.tex

# 一键编译（自动处理多次编译和参考文献）
latexmk -xelatex PostDocReport.tex
```

> **提示**：项目已包含 `.latexmkrc` 配置文件，预设使用 XeLaTeX 编译，因此可直接运行：
> ```bash
> latexmk PostDocReport.tex
> ```

### pdfLaTeX 编译步骤

```bash
pdflatex PostDocReport.tex
bibtex PostDocReport
pdflatex PostDocReport.tex
pdflatex PostDocReport.tex
```

### 编译输出文件

编译成功后会生成以下文件：

| 文件 | 说明 |
|------|------|
| `PostDocReport.pdf` | 最终 PDF 文档 |
| `PostDocReport.aux` | 辅助文件（引用信息） |
| `PostDocReport.bbl` | 参考文献列表 |
| `PostDocReport.log` | 编译日志 |
| `PostDocReport.toc` | 目录信息 |
| `PostDocReport.lof` | 图片目录 |
| `PostDocReport.lot` | 表格目录 |

## 使用说明

### 修改封面信息

在 `PostDocReport.tex` 主文件中修改以下命令来设置封面信息：

```latex
\classification{分类号}      % 分类号
\confidential{密级}          % 密级，如"公开"、"内部"等
\UDC{UDC编号}                % 国际十进制分类号
\serialnumber{编号}          % 报告编号
\school{学校名称}            % 学校名称
\title[短标题]{完整标题}      % 中文标题
\author{作者姓名}             % 博士后姓名
\workdate{工作完成日期}       % 工作完成日期
\submitdate{提交日期}         % 提交报告日期
\address{地址}               % 地址
\englishtitle{英文标题}       % 英文标题
\major{流动站名称}            % 流动站名称
\submajor{专业名称}           % 二级学科名称
\advisorent{企业导师}         % 企业合作导师
\advisorschool{学校导师}      % 学校合作导师
\institute{学院名称}          # 学院名称
\begindate{起始时间}          % 研究工作起始时间
\ssdate{期满时间}             % 研究工作期满时间
```

### 添加章节

1. 在 `chapter/` 目录下创建新的 `.tex` 文件
2. 在 `PostDocReport.tex` 中使用 `\include{chapter/新文件名}` 引入

### 添加图片

1. 将图片放入 `figures/` 目录
2. 在正文中使用以下代码插入图片：

```latex
\begin{figure}[htbp]
    \centering
    \includegraphics[width=0.8\textwidth]{figures/图片文件名.jpg}
    \caption{图片标题}
    \label{fig:图片标签}
\end{figure}
```

### 添加参考文献

1. 在 `bib/tex.bib` 中添加文献条目
2. 在正文中使用 `\cite{文献标签}` 引用

### 常用格式示例

本模板在各章节文件中展示了以下常用格式的使用方法：

- 单图和多图并排排版
- 三线表和复杂表格
- 数学公式（行内公式、独立公式、多行公式、矩阵）
- 算法伪代码
- 代码块
- 定理、定义、证明等数学环境
- 参考文献引用

## 格式规范

本模板遵循以下格式规范：

- 纸张：A4
- 正文字体：中文宋体，英文 Times New Roman
- 字号：正文小四号，标题三号
- 页边距：上下2.5cm，左右2.8cm
- 页码：前言部分使用罗马数字，正文部分使用阿拉伯数字
- 参考文献：采用 GB/T 7714 国标格式

## 许可证

本模板基于 LaTeX Project Public License (LPPL) 发布。

## 常见问题

### Q: 编译时出现字体找不到的错误？

A: 请确保系统安装了 Times New Roman 字体，或者修改 `PostDocRep.cls` 中的字体设置。

### Q: 参考文献显示不正确？

A: 请确保运行了 bibtex 命令，并检查 `bib/tex.bib` 中的文献条目格式是否正确。

### Q: 图片无法显示？

A: 请检查图片路径是否正确，确保图片文件存在于 `figures/` 目录中。

## 更新日志

- 2026-04: 初始版本，基于 Overleaf 博士后研究报告模板，针对浙江大学格式要求进行适配