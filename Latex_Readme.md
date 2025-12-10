`Model`文件里面的`LaTex_Learn.tex`提供了一份从IEEE下载的会议模版，并且利用Ai加了一下注释，方便理解与学习。

你好，朋友

**LaTeX 不是打字机，它是程序员思维在写作上的延伸。** 
LaTeX是为了让我们专注于**逻辑（Logic）**和**内容（Content）**，而不是被格式（Format）牵着鼻子走。

---

### 第一阶段：利其器（环境选择）

刚开始不要在“安装环境”上浪费半天时间。你的任务是发论文、写毕业大论文，不是做 IT 运维。

1.  **入门首选：Overleaf**
    *   **理由：** 它是云端的，不用配置环境，打开网页就能写。最重要的是，导师（如果有心改的话）和同门可以实时协作。
    *   **建议：** 注册一个账号，直接搜 "IEEE Conference Template" 或 "IFAC Template"，五秒钟你就可以开始写第一段话了。

2.  **进阶必备：VS Code + LaTeX Workshop**
    *   **理由：** 等你写毕业大论文（几万字）或者网不好时，本地编译更快。VS Code 的补全功能和快捷键是无敌的。
    *   **配置：** 安装 TeX Live (Windows) 或 MacTeX (Mac)，然后在 VS Code 里装 LaTeX Workshop 插件。

---

### 第二阶段：定骨架（模板与结构）

1.  **不要从零开始**
    *   去期刊官网下载 `.cls` 文件（类文件）。例如 IEEE 的 `IEEEtran.cls`。
    *   **毕业大论文**：直接去 GitHub 搜你们学校的名字 + Thesis + LaTeX。前人栽树，后人乘凉，99% 的高校都有学长写好的模板。

2.  **文件结构要清晰（工程化思维）**
    不要把几千行的代码塞在一个 `.tex` 文件里。学控制的都知道“模块化”的重要性。
    *   `main.tex` (主控文件，只负责引用)
    *   `chapters/` (文件夹，放各章节)
        *   `intro.tex`
        *   `model.tex`
        *   `control_design.tex`
        *   `simulation.tex`
    *   `figures/` (放图片)
    *   `refs.bib` (参考文献)

    在 `main.tex` 里用 `\input{chapters/model}` 来拼接文章。

---

### 第三阶段：攻核心（数学公式）

这是我们的“饭碗”。控制工程离不开矩阵、微分方程和优化问题。

1.  **告别鼠标，拥抱语义**
    *   **公式环境：** 别总用 `$$...$$`，那是老派写法。用 `\begin{equation} ... \end{equation}`，这样能自动编号，方便引用。
    *   **多行公式：** 推导李雅普诺夫（Lyapunov）函数导数时，公式往往很长。务必使用 `\begin{align} ... \end{align}`，用 `&` 对齐等号。

2.  **常用宏包 (Packages)**
    在导言区（`\documentclass` 和 `\begin{document}` 之间）加上：
    ```latex
    \usepackage{amsmath}  % 数学核心
    \usepackage{amssymb}  % 各种符号
    \usepackage{bm}       % 粗体，控制里向量矩阵要加粗！
    ```

3.  **定义快捷命令（Macros）——这是高效的关键！**
    你是不是厌倦了每次输入 $\mathbb{R}^{n \times n}$ 都要打 `\mathbb{R}^{n \times n}`？
    在导言区定义自己的“宏”：
    ```latex
    \newcommand{\R}{\mathbb{R}} 
    \newcommand{\bx}{\mathbf{x}} % 状态向量 x
    \newcommand{\bu}{\mathbf{u}} % 控制输入 u
    \newcommand{\norm}[1]{\left\lVert#1\right\rVert} % 范数
    ```
    以后写 $\dot{\mathbf{x}} = A\mathbf{x} + B\mathbf{u}$，只需要打：
    `\dot{\bx} = A\bx + B\bu`。这能节省你 30% 的生命。

---

### 第四阶段：画图表（从 MATLAB 到 LaTeX）

这是区分“新手”和“老手”的分水岭。**绝对不要**在论文里放模糊的截图（jpg/png）。

1.  **矢量图是信仰**
    *   控制工程的仿真图必须是**矢量图**（.eps 或 .pdf）。放大 500% 也不能有锯齿。
    *   **MATLAB 导出法：**
        *   方法 A（推荐）：在 Figure 窗口，文件 -> 导出设置 -> 渲染 -> 勾选“向量格式”，导出为 PDF 或 EPS。
        *   方法 B（大神流）：使用第三方工具 `matlab2tikz`。它会把 MATLAB 图转换成 LaTeX 代码。虽然编译慢，但字体和论文正文完美统一，美观度 Max。

2.  **系统框图**
    *   如果你有时间，学习 **TikZ** 宏包。用代码画框图，极其专业。
    *   如果为了效率，用 Visio 或 Draw.io 画好，导出为 PDF，裁掉白边（Crop），然后插入 LaTeX。

    **插入图片标准代码：**
    ```latex
    \begin{figure}[htbp]
        \centering
        \includegraphics[width=0.8\linewidth]{figures/step_response.pdf}
        \caption{Step response of the closed-loop system.}
        \label{fig:step_resp} % 给图打个标签，以后引用它
    \end{figure}
    ```

---

### 第五阶段：理文献（BibTeX 是你的第二大脑）

千万不要手动敲参考文献格式！那是 Word 用户的噩梦。

1.  **工作流：**
    *   去 Google Scholar 或 IEEE Xplore 搜文章 -> 点击“引用（Cite）” -> 点击 "BibTeX" -> 复制那段代码。
    *   粘贴到你的 `refs.bib` 文件里。
2.  **文献管理软件：**
    *   推荐 **Zotero**。装个 `Better BibTeX` 插件，可以自动把你的文献库同步导出为 .bib 文件。
3.  **文中引用：**
    *   当你需要引用 Kalman 的文章时，只需要打 `\cite{Kalman1960}`。LaTeX 会自动根据期刊要求，把它变成 [1] 或者 (Kalman, 1960)。

---

### 第六阶段：避坑与高效习惯（老学长的叮嘱）

1.  **交叉引用（Cross-Reference）：**
    *   **永远不要**在正文里手写“如公式 (3) 所示”。因为你一旦在前面加了个新公式，(3) 就变成 (4) 了，你会改死。
    *   **正确做法：**
        *   公式后加标签：`\label{eq:state_space}`
        *   正文引用：`As shown in \eqref{eq:state_space}...`
        *   图片、章节同理。

2.  **善用注释：**
    *   用 `%` 注释掉你拿不准的句子，而不是删掉它们。
    *   写作时，可以用 `% TODO: check this parameter` 来提醒自己。

3.  **版本控制：**
    *   如果你用 VS Code，学会用 **Git**。
    *   “Final_v2_真的不改了_v3.tex” 这种文件名是很丢人的。Git 能让你回溯到任何一个历史版本。

4.  **排版微调留到最后：**
    *   图片跑到下一页去了？表格溢出了？**先别管！**
    *   LaTeX 的自动排版算法比你聪明。先把内容写完，最后再处理 `\newpage` 或调整图片位置参数 `[htbp]`。

### 最后

当你第一次看到编译出来的 PDF 里，那一个个精美的 $\int$ 和 $\Sigma$，以及那完美的对齐，你会发现，所有的折腾都是值得的。

加油，祝你的论文早日 Accept！

