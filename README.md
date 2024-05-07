# bjtu本科毕设补充包

务必用`xelatex`编译，如果你用overleaf可以从左上角menu里选择编译器为`xelatex`

本模版是我在前人[@ipChrisLee](https://github.com/ipChrisLee)基础上改的补充包，fork并改自[ipChrisLee/thesis: LaTeX Thesis template of ipLee (github.com)](https://github.com/ipChrisLee/thesis)。

增加了2024年毕设的`诚信声明`和`外文原文与译文`，有任何格式问题请随时提issue或者PR。

外文原文放到`sections/English.tex`中，中文翻译放到`sections/Chinese.tex`中，章节编号、图表的称呼和编号都会自动切换。

不熟悉latex建议用word！

以下为原readme：

# Thesis template of ipLee

ipLee自用的thesis类模板，fork并更改自[https://github.com/chenzewei01/bjtuThesis](https://github.com/chenzewei01/bjtuThesis)。

理论上可以用在BJTU的毕设论文，但是需要简单更改一些内容。

出于部分原因，我不想再维护一个BJTU毕设论文的LaTeX模板仓库，并且我认为这应该是BJTU的任务，不是任何同学的任务。

当然，我不反对任何人基于本仓库维护一个BJTU毕设论文的LaTeX模板或者做任何别的事，敬请自便。



# 模板结构

```
.
├── figures				%*	图片
│   └── bjtu.png
├── main.tex			%*	主tex文档
├── README.md			%	本文件
├── tex_ref				%	引用相关文件
│   ├── chinesebst.bst	%	引用格式
│   └── refs.bib		%*	引用列表
├── tex_src				%	文档源文件
│   ├── abstract_cn.tex	%*	中文摘要
│   ├── abstract_en.tex	%*	英文摘要
│   ├── chap01.tex		%*	第一章
│   ├── fun.tex			%	特殊函数
│   ├── info.tex		%*	信息
│   └── package.tex		%*	引入包
├── thesis.cfg			%	cfg
└── thesis.cls			%	cls
```

其中`*`的内容需要自行更改。



# 常见语法

## 表格

```latex
\begin{table}[htbp]
  \centering
  \caption{MIPS ISA定义的通用寄存器}
  \label{tab:mips_isa_gpr}
  \begin{tabular}{|l|c|l|}
    \headhline
    编号 & 寄存器名称 & 常见用途 \\ 
    \hline
    \$0 & \$zero & 常量0 \\
    \hline
    \$1 & \$at & 汇编程序中的保留寄存器 \\
    \hline
  \end{tabular}
\end{table}
```

其中`\caption`是标题，`\label`是用来cite的label，可以在文章中使用`\ref{}`来引用表格。



## 有序列表

```latex
\begin{enumerate}[]
  \item R型指令
  
  R型指令格式为\verb|op rd, rs, rt|。

  其中op表示操作码，rd表示目标寄存器，rs和rt表示源寄存器。这种指令格式的指令主要用于寄存器之间的操作，如加、减、与、或等。常见的R型指令包括：\verb|add, sub, and, or|。

  \item I型指令
  
  I型指令格式为\verb|op rt, rs, imm|。

  其中op表示操作码，rt表示目标寄存器，rs表示源寄存器，imm表示立即数。这种指令格式主要用于数据传输和算术逻辑运算等操作。常见的I型指令包括：\verb|addi, lw, sw, beq|。

  \item J型指令
  
  J型指令格式为\verb|op addr|。

  其中op表示操作码，addr表示跳转地址。这种指令格式主要用于跳转操作。常见的J型指令包括：\verb|j, jal|。
\end{enumerate}
```



## 无序列表

```latex
\begin{itemize}
  \item IF阶段：从存储中读取指令。
  \item ID阶段：对指令进行解码，确定操作数、操作数的值和操作类型。
  \item EX阶段：根据指令类型执行操作。
  \item WB阶段：根据ID阶段得到的目的寄存器信息、EX阶段得到的操作结果，更新目的寄存器的值。
\end{itemize}
```



## 代码块

```latex
\begin{lstlisting}[]
  beq $t1, $t2, label
  add $t3, $t1, $t2
  addi $t3, $t1, 1
  ...
label: 
  sub $t4, $t1, $t2
\end{lstlisting}

\begin{lstlisting}[language=Verilog]
import "DPI-C" function int abs_c(int a);
module fun_caller(
  input  [31:0] num,
  output [31:0] absNum
);
  assign absNum = abs_c(num);
endmodule
\end{lstlisting}
```



## 图片

png图片（jpg图片等同理）：

```latex
\begin{figure}[ht]\centering\includegraphics[width=\textwidth]{img_res/workflow_sim.drawio.png}\caption{仿真流程}\label{fig:workflow_sim}\end{figure}
```

svg图片：

```latex
\begin{figure}[!ht]\centering\includesvg[inkscapeformat=png,width=\textwidth]{img_res/simple_fsm_wave.svg}\caption{简单FSM对应波形图}\label{fig:wave_simple}\end{figure}
```

同理，`\caption`是标题，`\label`可以用于引用。

## 超链接

```latex
\href{www.baidu.com}{百度}
```

# TODO List

1. 将仓库改为GitHub模板仓库。
2. 增加引用文献的类型。


# Bug List

这里记录一些已知但还未修复的BUG：

1. 在引用列表（也就是`refs.bib`）文件中，不能使用`_`符号，必须使用`\_`代替。
2. 引用里的长链接不能换行。

# bjtu-bachelor-thesis

本模板是北京交通大学本科毕业设计的非官方LaTeX模板，尽量还原了官方给出的word模板样式。尽管不能做到完全一致，但在肉眼看上去基本没有差别。我的LaTeX水平极其有限，因此这个模板追求的是能跑起来就行，里面代码是非常丑陋的。也希望如果有比较精通LaTeX模板的同学，能继续加以修改，让更多的人能够摆脱word的困扰。当然，如果学校能提供一份官方的LaTeX模板则是最好，目前研究生院已经提供了，还希望本科生院也能加把劲。

本模板是基于 https://github.com/billhu0228/BJTUThesisTemplete 的模板修改而来，感谢billhu0228。

注：
1. 请使用XeLaTeX编译，反馈QQ群：1021063106
2. 附带的几个字体文件，是因为LaTeX中易系列的字体其实是跟word里的有一些差别，通篇看上去其实区别还是挺大的
3. 本模板尚未经过验证，可能会有bug，如果你遇到了，请及时反馈，我会尽快修复。
4. overleaf模板地址：[点这里](https://www.overleaf.com/read/cjkrjfvczbvc)，这是一个个人模板，你可以登录overleaf之后，创建一份copy，就可以使用了。因为这个模板可能还会有修改，因此暂且不会上传到gallery，等到没有问题之后再上传。
5. 基于第3条，overleaf上的模板可能会有变动，而我修改overleaf上的模板，是无法把改动同步到基于模板派生出来的文档的。因此，需要你手动把新的.cls或者.tex文件更新一下。

## FAQ

### 有奇怪的找不到包的问题怎么办？

可能你装的tex live有问题。对于一般用户，建议使用overleaf，可以节省大部分配环境的时间。

### pdf是否会比word格式查重率更高？

**有可能会，但影响非常小。** pdf查重率更高的原因是，知网的查重系统可能无法正确识别页眉等部分，对于像“北京交通大学毕业设计”这样的字也一起识别成正文，从而导致整体查重率偏高。就作者个人经验来说，60页的论文，其中有几页的页眉被标红了，剩下的并没有。此外，对于封面、权利授权书、参考文献、公式等，查重系统均可正常识别。问了三个使用本模板的同学，有两个查重率低于1%（其中一个是理学院），另一个约为12%，也均在学校要求范围内。因此，如果你的论文内有较多的公式，可以考虑使用本模板，可以帮你节约一些浪费在word排版上的生命。

### 封面间距奇怪怎么办？

目前没有很好的解决方案，这个项目的cls文件确实不能很好地兼容各种行数的标题（例如，中文1行英文两行，中文两行英文三行，这两种展现情况会有比较大的差异），需要使用者自行调整。调整方法也非常简单，找到`bjtu-bachelor-thesis.cls`这个文件的大约269行，调整各个`\vspace`后面的数值就可以了。`\vfill`也可以尝试加上或者去掉。此外，对于两行中文三行英文的标题，英文第一行和第二行之间的间距会奇怪地变大，这里原因未知，目前有很简单粗暴的解决方案，就是在`template.tex`中的`\etitle`添加一个负的间距，例如

```tex
\etitle{AAAAA \\[-0.8em] BBBBB \\ CCCCC}
```

具体数值可以自己调整。如果有更好的解决方案，欢迎提pr。

### 排版问题，如何将表格或图片的位置进行固定？

在排版的时候，可能会发现这样的情况，例如你有

```tex
AAAA
\begin{figure}[htpb]
\end{figure}
BBBB
CCCC
````

然后排出来的版面却是这样的

```tex
AAAA
BBBB
{figure}
CCCC
````

对于这种问题，可以将`htpb`换成`H`。但大概率会引入非常离谱的间距，这是因为latex默认是按照上下两端对齐来排版的，如果字不够填满一页，就会加大行间距，显得非常怪。对于这种问题，可以手动在排出来那一页的末尾加`\newpage`强行换页，行间距就正常了。当然，也可以尝试将图片的高度缩小，或者多填点字。

### 为什么我插入到.bib中的引用不显示？

请先确认下是否在正文中引用过了，biblatex的默认行为是只有引用过的文献才会显示在参考文献页面。当然，如果你需要显示全部文献（即使没有引用到），可以取消注释229行附近的`\nocite`，但不推荐这么做，可能会被答辩老师怼。

### 如何找bibtex引用？

知网默认是不提供bibtex引用格式的。可以通过谷歌学术、百度学术来获取你需要论文的bibtex引用，或者是直接去对应期刊网站上找cite。另外，还可以使用在线生成器，例如 https://www.bibme.org/bibtex 。

### 版权授权页，如何插入电子签名？

目前本项目的latex源码不支持在签名处插入图片（尝试调整了几个版本，效果都比较差），我最后的解决方案是，在最终pdf上使用pdf编辑器（acrobat等）直接插入图片。当然，如果有更好的解决方案，也欢迎提pr。

