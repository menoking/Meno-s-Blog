# 【Latex速成】零基础半小时入门Latex

> 原创 已于 2026-06-04 17:06:28 修改 · 公开 · 733 阅读 · 25 · 8 · 本内容遵循CC 4.0 BY-SA版权协议 版权声明：本文为博主原创文章，遵循 CC 4.0 BY 版权协议，转载请附上原文出处链接和本声明。 GEO检测 · 编辑
> 文章链接：https://menoking.blog.csdn.net/article/details/156433753

**目录**

[TOC]



## 总览示例

```erlang
\documentclass{article} % 文档类
\title{我的第一个 LaTeX 文档} % 标题
\author{作者} % 作者
\date{\today} % 日期
 
\begin{document}
\maketitle % 生成标题
 
\section{引言} % 一级标题
这是我的第一个 LaTeX 文档！\\ % 换行
这是一个简单的段落。
 
\section{数学公式}
这是一个行内公式：$E = mc^2$。\\ % 行内公式
这是一个行间公式：
\[
\int_a^b f(x) \, dx
\]
\end{document}
```

公式示例

```xml
<!-- 行内公式 -->
<p>行内公式：\( E = mc^2 \)</p>
 
<!-- 行间公式 -->
<p>行间公式：\[ \int_a^b f(x) \, dx \]</p>
 
<!-- 矩阵 -->
<p>矩阵：
    \[
    \begin{pmatrix}
        1 & 2 \\
        3 & 4
    \end{pmatrix}
    \]
</p>
 
<!-- 方程组 -->
<p>方程组：
    \[
    \begin{cases}
        x + y = 5 \\
        2x - y = 1
    \end{cases}
    \]
</p>
```

## 基础认识

### 导言区与正文区

在begin{document}和end{document}之间的就是正文区，而在这之前的就是导言区。

### 宏包

```bash
\usepackage{xxx, xxxx, xxxxx}
```

### 符号

> 
> 
> - 注释：%
> 
> - 转义字符：\
> 
> - 位置对齐：&
> 
> - 数学公式：$
> 
> - 上标，下标：^，_
> 
> - 内容：{}
> 
> 

### 标题

> 
> 
> - chapter- 章，一般只用于可以成书的文章
> 
> - section——节（一级标题）
> 
> - subsection——小节（二级标题）
> 
> - subsubsection ——小小节（三级标题）
> 
> 

### 换行、换页、缩进

> 
> 
> - 换行：\\(\newline、\linebreak、\\[offset))
> 
> - 分段：\par
> 
> - 分页命令：\newpage
> 
> - 首行缩进：\setlength{\parindent}{长度}
> 
>   - 注：这里长度的单位为一般为pt或em，pt是绝对单位；em是相对单位，表示1个中文字符宽度。
> 
> 

## 基本使用

### 数学公式

> 
> 
> - 行内公式：公式公式
> 
> - 单行编号公式：\begin{equation}\label{公式标签}公式\end (equation)
> 
>   - 自动引用\autoref{公式标签}（需要导入依赖包\usepackage{hyperref}）
> 
> - 无编号单行公式：公式公式
> 
>   或者&&公式&&
> 
> - 多行公式：使用\begin{split}...lend{split}（需要导入依赖包\usepackage{amsmath}，有的环境可能自带）
> 
> - 分段函数表示法：属于多行公式一种，使用\begin{cases}...lend{cases}（需要导入依赖包\usepackage{amsmath}）
> 
>   - 需要用正文样式输出的地方用\text{}
> 
> 

Latex中数学符号有专门的表示法，详情可见专门收集的Latex符号大全，例如：

[LaTex符号大全_包括LaTex数学符号运算符号函数符号希腊字母矩阵符号等常用符号 - ProcessOn](https://www.processon.com/latex-symbol) 

或者可以用专门的转换工具进行转换，如： [在线LaTeX公式编辑器-编辑器](https://www.latexlive.com/) 

### 插入图片

**依赖包** 

```undefined
\usepackage{graphicx}
```

**插入单张** 

```less
\begin{figure}[htbp]
    \centering
    \includegraphics[图片大小J[图片路径]
    \caption{图片标题、说明}
    \label{图片标签}
\end{figure}
```

例如：

```less
\begin{figure}
    \centering
    \includegraphics[width=1\linewidth]{xxx.png}
    \caption{Enter Caption}
    \label{fig:placeholder}
\end{figure}
```

图片大小格式为[height=XXXcm,width=YYYcm]，单位可以采用cm或in（inch），如果只规定高或宽其中一个，图片将保持高宽比插入，所以一般只需要规定图片宽度。路径为相对与tex文件的路径。

> htbp是LaTeX中用于控制浮动体位置的一个选项集。浮动体（如图片或表格）通常不会被直接放置在代码所在的位置，而是由 LaTeX根据排版需要放置在页面的其他位置。htbp 用于指定浮动体的偏好位置。这些选项的含义如下：
> 
> - h（here）：尽量将浮动体放置在代码所在的位置。然而，如果页面的顶部或底部能够更好地容纳浮动体，LaTeX可能会选择这样做。
> 
> - t（top）：将浮动体放置在页面的顶部。
> 
> - b（bottom）：将浮动体放置在页面的底部。
> 
> - p（page）：将浮动体放置在一个单独的页面上。
> 
> 这些选项可以组合使用，例如ht表示首选放置在页面顶部，但如果不行就放置在代码所在的位置。默认情况下，如果你不提供任何选项，LaTeX会使用tbp作为默认值。
> 例如，\begin{figure}[htbp］表示在尽量放在当前位置，如果不行就放在页面顶部，底部，或者单独一页。

**双栏文章跨栏插入** 

```less
\begin{figure*}[htbp]
    \centering
    \includegraphics[图片大小J[图片路径]
    \caption{图片标题、说明}
    \label{图片标签}
\end{figure*}
```

### 列表

LaTeX中的列表环境包含无序列表 `itemize` 、有序列表 `enumerate` 和描述 `description：` 

```cobol
\begin{enumerate}
    \item[(1)] 这是第一点; 
    \item[(2)] 这是第二点;
    \item[(3)] 这是第三点. 
\end{enumerate}
```

### 表格

表格示例

```cobol
\begin{table}[htb]
\begin {center}caption{Beecy.}
\label{table:1}
\begin{tabular} {|c|c|c|}
\hline \textbf{Algorithms} & \textbf{Complexity}&
\textbf{Overhead} \\
\hline algorithm 1 & high & low \\ \hline algorithm 2 & high & low \\ \hline algorithm 3 & low & low \\
\hline
\end{tabular}
\end{center}
\end{table}
```

由于Latex中表格表示过于复杂，我们同样常用工具生成，如： [LaTeX 表格 生成器 - 表格转换工具](https://tableconvert.com/zh-cn/latex-generator) 

## 参考文献

### 普通引用

角标

```less
\cite{lable1}，\cite{lable2}..
```

文献

```cobol
\begin{thebibliography}{99}%99表示引用上限
\Abibitem {lable1} Anita G , V. B V ,John P .Hybrid model with optimal features for non-invasive blood glucose monitoring from breath biomarkers[J].Biomedical Signal Processing and Control,2024,88(PC):
\bibitem {lable2}Zhining C ,Jianzhou W ,Li Y , et al.A hybrid electricity load prediction system basedonweighted fuzzy time series and multi-objective differential evolution[J].Applied Soft Computing,2023,149(PB):
\end{thebibliography}
```

### BiBTex管理

目录下新建任意.bib后缀文件，此文件为存放BiBTex格式文献的文件，可从谷歌学术等数据库直接复制。

> @article { **yu2019review** ,
> title= {A review of recurrent neural networks: LSTM cells and network architectures},
> author={Yu, Yong and Si, Xiaosheng and Hu, Changhua and Zhang, Jianxun},
> journal= {Neural computation},
> volume={31},
> number={7},
> pages={1235--1270},
> year={2019},
> publisher={MIT Press One Rogers Street, Cambridge, MA 02142-1209, USA journals-info~...}
> }

导言区添加

```undefined
\bibliographystyle{unsrt}
```

文末添加

```undefined
\bibliography{bib文件名}
```

角标引用

> \cite{ **yu2019review** }

