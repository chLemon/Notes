# 下载与安装
http://www.tug.org/texlive/
# 基本使用
```
\documentclass{article}           #引入文档类，article，用于论文撰写相关操作

\begin{document}               #begin和end对应，在中间撰写

Hello \LaTex.

\end{document}
```
记事本就可以
大括号用来写参数
一般\开头的，叫命令

写好后，cmd里编译
latex xxx.tex

生成dvi文件，用dvipdfmx命令，将dvi转换为pdf
dvipdfmx xxx.dvi

或者，还可以通过xelatex命令直接将tex文件编译成pdf文件，该命令支持UTF-8，可以生成中文文档
xelatex xxx.tex

如果需要支持中文，需要保证文件用UTF-8编码（另存为下面可以设置），还需要引入宏包\usepackage{ctex}

# IDE
textstudio

## 保存

会生成很多中间文件，所以一般都会新建一个文件夹去保存。



Ctrl+鼠标滚轮：放大字体

# 源文件的基本结构
```
% 导言区
\documentclass{article}%book,report,letter             引入一个文档类
导言区主要用于全局设置
\title{文档标题}
\author{作者}
\date{\today}

% 正文区（文稿区）
\begin{document}        引入一个环境，环境名称document
    \maketitle
    %能有一个document环境
    $$
\end{document}
```
%表示注释 $符号内数学模式，外文本模式
换行，加个空行，多个空行视为一个
双$：行间公式
单$：行内公式

# 中文处理
1. 编码必须是UTF-8
2. xelatex编译
3. 加入\usepackage{ctex}，引入宏包


# 导言区命令定义
\newcommand\degree{^\circ}

$\angle C=90\degree$

书写中文的时候也可以指定字体，如
\title{\heiti 题目}        黑体

\begin{equation}
用于产生带编号的行间公式
\end{equation}

命令行输入 texdoc ctex 打开ctex的宏包手册，查看使用方法

可以注释掉\usepackage{ctex}，使用\documentclass{ctexart}，还有ctexbook和ctexrep

texdoc可以查看帮助文件，如lshort-zh

# LaTex的字体设置
一个字体有5种属性：
## 字体编码
正文字体编码
数学字体编码

## 字体族
罗马字体
无衬线字体
打字机字体
```
字体族设置命令，设置为罗马字体，字体命令，作用于字体的参数
\textm{Roman Family}

\textsf{Sans Serif Family}

\texttt{Typewriter Family}

字体声明，声明之后的字体为罗马字体
\rmfamily
\sffamily
\ttfamily

可以使用大括号进行分组，以限定作用范围

```

## 字体系列
粗细
宽度
```
\textmd{普通Medium Series}
\textbf{粗体Boldface Series}

\mdseries
\bfseries

```

## 字体形状
直立
斜体
伪斜体
小型大写
```
\textup{Upright Shape}
\textit{}
\textsl{}
\textsc{}

\upshape
\itshape
\slshape
\scshape

中文字体
\songti
\heiti
\fangsong
\kaishu

中文的粗体和斜体
\textbf{粗体}   黑体
\textit{斜体}   楷书

```

## 字体大小
```
字体大小是与normalsize相对的大小
normalsize的设置是在文档类声明时候可以传入参数
\documentclass[10pt]{article}
设置normalsize大小为10磅，一般只有10、11、12磅

\tiny
\scriptsize
\footnotessize
\small
\normalsize
\large
\Large
\LARGE
\huge
\HUGE

中文字号设置命令
\zihao{-0} 你好！
小初
\zihao{5}
五号

详细见文档

```
## 思想
LaTeX的思想是格式与内容的分离，因此建议在导言区定义一个新的命令
```
\newcommand{\myfont}{\textit{\textbf{\textsf{Fancy Text}}}}
```
在正文中用定义的命令进行字体设置
\myfont

# 篇章结构
构建提纲

构建小节
\section{引言}
\section{结论}

构建子小节
\subsection{数据}

下一级
\subsubsection{实验条件}

换行\\
空行产生新的段落
产生新的段落\par
通常用插入空行来实现

\ctexset命令可以用来更改标题格式

\chapter
在ctexbook里，可以按照章节生成文档大纲（此时没有subsubsection命令）

产生目录
\tableofcontents

# 特殊字符
## 空白符号
英文中多个空格是一个，中文中不起作用

空行分段

禁止中文全角空格

当前字体中M的宽度，1em
\quad

2em
\qquad

约1/6个em，逗号或命令
\, 
\thinspace

0.5个
\enspace

反斜杠+空格
\ 

产生硬空格（不能分割的空格）
~

产生指定宽度的空白，1pc=12pt
\kern 1pc
\hskip -1em
\hspace{1pt}

占位宽度
\hphantom{xyz}

弹性长度，撑满整个空间
\hfill

## 控制符
转义的意思，但是\\是换行，所以要用textbackslash
\#
\$
\%
\{
\}
\~{}              这个是上方的小~
\_{}              下划线
\^{}               上方的小^
\textbackslash
\&

## 排版符号
特殊符号
## 标志符号
额
## 引号
左单引号
` 1上面的那个
右单引号
‘ 一个引号

双引号都是2个

## 连字符
```
-
--
---
```

## 非英文字符
## 重音符号
拼音之类的

# 插图
导言\usepackage{graphicx}
语法\includegraphics[<选项>]{<文件名>} 可选参数有缩放比例、旋转等
格式EPS,PDF,PNG,JPEG,BMP
\graphicspath{{路径1/}，{路径2}}

可选参数：
scale缩放因子
height固定值的高度
width宽度
height=0.1\textheight
angle旋转角度

# 表格
tabular环境
\begin{tabular}{l c c c r}
列格式说明符
l左对齐
c居中
r右对齐
p{1.5cm}指定宽度的列，会自动换行
里面输入内容，&分割不同列 \\换行

在参数中加入|插入表格竖线
内容中用\hline加入表格横线
2个产生双线

更复杂的表格 booktab、longtab、tabu

# 浮动体
figure
table
【htbp】排版位置参数
h此处，here，代码所在的上下文位置
t页顶，top，代码所在页或之后页的顶部
b页底，bottom，代码所在页或之后页的底部
p独立一页page，浮动页面
\centering设置居中
\caption{标题}     会自动编号

\label{设置标签}
\ref{引用标签}

# 数学公式
## 行内公式
### 美元符号
### 小括号
\(a+b\)
### math环境
\begin{math}a+b\end{math}
## 上标
x^{20}
## 下标
下划线
## 希腊字母
\alpha
\beta
大写字母开始的就是大写
\Alpha
## 数学函数
\log x
\sin x
\ln x

\sqrt[4]{a}  开根号
## 分式
\frac{1}{2}

## 行间公式
### 双$
### 中括号
\[ a+b\]
### displaymath环境
### equation环境
自动编号
\label添加标签
### equation*环境
不带编号
此时交叉引用的编号是小节编号

# 批量注释
ctrl+T
# 矩阵排版
\usepackage{amsmath}
matrix环境
\begin{matrix}
and符号分割，双反斜杠换行

pmatrix两端加小括号
b中括号
B大括号
v单竖线
V双竖线

省略号：
\dots          横的
\vdots   斜的
\ddots   竖的

右下角乘号的排版：
\times
要写在\bmatrix环境的外面

很多 用的时候查吧  真是的

smallmatrix行内小矩阵

# 多行公式
```
#引入两个宏包
\usepackage{amsmath}
\usepackage{amssymb}

#使用gather环境
\begin{document}
    \begin{gather}
        a + b = b + a\\
        abba \notag
    \end{gather}
```

双斜杠换行。每行公式都会进行编号

也可以使用gather*，带星号的gather不会进行编号

也可以在双反斜杠前加```\notag```命令阻止编号

```
% 也可以使用align环境和align*环境，内部可以用 & 进行对齐
&后对齐

也可以用split环境实现一个公式的多行排版
\begin{equation}
\begin{split}
\\换行，&对齐
\end{split}
\end{equation}

% cases环境实现分段函数的情况
同样在equation内
D(x) = \begin{cases}
1, \text{如} x > 0  \\
0, ...
...

\in 属于符号
\mathbb 花体字符，需要amssymb宏包支持

```

# 参考文献

## 简单的：一次管理，一次使用

```
thebibliography环境

\begin{thebibiography}{99}
    \bibitem{artical1} 有个必选参数，指定参考文献的引用标志。每条参考文献。\emph{强调参考文献中的某些内容}
    \texttt
    \cite{article1}，引用参考文献
```

## 一次管理，多次使用

设置——构建——默认文献工具——改为BibTex

创建一个新文件，在该文件中编写参考文献的详细信息。

```
@BOOK{mittelbach2004,    @BOOk表示是一本书，第一个参数是引用标志，其他详细信息用key-value的形式，用逗号分隔
title = {asd},
year = {asd},
...
}
```

然后将该文件保存为以.bib结尾的参考文献数据库文件。

```
导言区
\bibliographystyle{plain}  指定参考文献的排版样式

正文中需要参考文献的地方
\bibliography{test}    test是参考文献数据库的名称，可以不带扩展名。不同数据库之间用逗号分隔
这里不会出现没被正文引用的参考文献，可以用\nocite{*}显示全部

引用依旧是\cite{标志}
```

文献数据库文件的维护。谷歌学术引用里有BibTeX



菜单栏——工具——清理编译过程、辅助文件

每次新编译都需要

natbib宏包提供了很多排版格式

# biblatex/biber

新的参考文献排版引擎

样式文件bbx文件，引用样式文件cbx文件，用LaTeX编写，维护相对简单。支持本地化排版

默认文献工具需要改为Biber

```
\usepackage[style=numeric,backend=biber]{biblatex}
\addbibresource{test.bib} 引入数据库，不可以省略后缀

正文中
\cite{}无格式引用
\parencite{}带方括号引用
\supercite{}上标引用

\nocite{*}
\printbibliography[title={参考文献}


```

```
符合国标7714标准的样式文件
gitlab.com/CasperVector/biblatex-caspervector

导言区
\usepackage[style=caspervector,backend=biber,utf8]{biblatex}

```

如果不希望中英文混排



设置——命令——Biber

```
biber.exe -l zh__pinyin %

\usepackage[style=caspervector,backend=biber,utf8,sorting = centy]{biblatex}   c:中文，e英文n作者姓名，t标题，y出版年  或ecnty
```



太复杂的可以考虑写bat文件【有这个必要吗？】

# 定义与重定义

类似函数