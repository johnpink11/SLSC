# ACL LaTeX Template (Structured)

基于官方 *ACL 会议 LaTeX 模板改造，将原单一文件拆分为主文件 + 子文件的结构，便于管理和协作。

## 项目结构

```
latex/
├── main.tex              # 主文件：preamble、标题、编译入口
├── references.bib        # 参考文献
├── acl.sty               # ACL 样式文件
├── acl_natbib.bst        # 参考文献样式
└── sections/
    ├── authors.tex       # 作者信息
    ├── abstract.tex      # 摘要
    ├── introduction.tex  # 引言
    ├── ...               # 其他章节
    ├── limitations.tex   # 局限性（ACL 必需）
    ├── acknowledgments.tex
    └── appendix.tex
```

## 使用方法

每个章节单独维护在 `sections/` 目录下，在 `main.tex` 中通过 `\input{sections/xxx}` 引入。

编译命令：

```bash
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```

或使用 latexmk：

```bash
latexmk -pdf main.tex
```

## 切换版本

在 `main.tex` 中修改：

```latex
\usepackage[review]{acl}   % 审稿版（带行号、匿名）
\usepackage{acl}            % 终稿版
```
