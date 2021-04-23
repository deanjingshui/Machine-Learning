#  Jupyter Notebook 使用

## 介绍

 Jupyter Notebook是一个开源的Web应用程序，允许用户创建和共享包含代码、方程式、可视化和文本的文档。它的用途包括：数据清理和转换、数值模拟、统计建模、数据可视化、机器学习等等。 

[官网介绍](https://jupyter-notebook.readthedocs.io/en/stable/notebook.html#introduction)

 Jupyter工程还提供了[JupyterLab](https://jupyter.org/try)作为新一代的用户界面 

## 为何要用它

在数据挖掘、机器学习领域，器提供了很好的 **交互性**，提高了研究效率。

## 安装

使用pip安装 Jupyter Notebook ，打开终端（比如Windows 的 cmd）输入：

```bash
py -m pip install --upgrade pip
py -m pip install jupyter
```

安装 Jupyterlab

```bash
py -m pip install jupyterlab
```

## 使用

#### 启动 Notebook Server

打开终端输入：

```bash
jupyter notebook
```

![](.\image\启动server.png)

启动成功后，会自在浏览器中打开页面

- 在不指定 **–ip** 和 **–port**参数的情况下，notebook服务器默认的ip和端口为http://localhost:8888/。如果需要打开两个notebook服务器，则需要更改端口号。
- 在不指定 **–notebook-dir** 参数的情况下，notebook的根路径为当前目录。

```bash
# 在当前文件夹\jupyter_notebook_home位置打开notebook，端口8889
jupyter notebook --notebook-dir .\jupyter_notebook_home --port 8889
```

## Notebook 文档结构

Notebook文档包含一些列cell，每个cell都是一个多行文本输入框，并且其中的代码可以通过**Shift+Enter**快捷键或者点击工具栏上的**Play**按钮执行。cell有三种类型：**code cells**、**markdown cells**以及 **raw cells**。

- code cells
  - 代码编辑区，支持 **语法高亮** 和 **tab自动补全**。使用的编程语言与 Notebook的 Kernel相关。Jupyter Notebook 默认使用 IPython Kernel，支持python。
  - 当运行code cell时，其中的代码将在Notebook文档关联的Kernel执行，代码的计算结果会在cell的输出框中进行展示。
  - cell不仅可以展示文本输出，还支持 matplotlib 图片和 HTML表格等。可参考[Rich Output](https://nbviewer.jupyter.org/github/ipython/ipython/blob/master/examples/IPython Kernel/Rich Output.ipynb)示例文档。
- markdown cells
  - 支持markdown语法的文本编辑区，可以方便的使用markdown语法进行文档编写。参考[Working with Markdown Cells](https://nbviewer.jupyter.org/github/jupyter/notebook/blob/master/docs/source/examples/Notebook/Working With Markdown Cells.ipynb)示例文档。
- raw cells
  - 原始文本编辑区，在此处写入的文本格式和内容都不会被修改。

## Notebook 的基础使用

参考[Notebook Basics](https://nbviewer.jupyter.org/github/jupyter/notebook/blob/master/docs/source/examples/Notebook/Notebook Basics.ipynb)示例文档

## Notebook 的常用快捷键

Notebook文档在编辑时，可以通过点击**Esc**进入命令模式，点击**Enter**进入编辑模式。

- 命令模式中被选中的cell左边界为蓝色：

  ![](.\image\命令模式.png)

- 编辑模式中被选中的cell左边界为绿色：

  ![](.\image\编辑模式.png)

- 在命令模式下常用的快捷键：
  - 导航：
    - `k`/`Up`，`j`/`Down`选中上面/下面的cell，与`shift`联合使用可以连续多选
    - `space`/`shift+space`向下/上滚动Notebook文档
  - 编辑：
    - `A`/`B`在上/下插入新的cell
    - `y`/`m`/`r`修改当前cell类型为code/markdown/raw
    - `x`/`c`/`v`剪切/复制/在其后粘贴cell
    - 双击`d`删除cell
    - `z`撤销上一步修改
  - 功能：
    - `ctrl+enter`运行当前cell
    - `shift+enter`运行当前cell并选中下一个cell
    - `alt+enter`运行当前cell并在其后插入新cell
    - `s`/`ctrl+s`保存Notebook文档
    - `h`打开快捷键菜单
- 在编辑模式下常用的快捷键：
  - 导航
    - `ctrl+left`/`ctrl+right`向左/右将光标移动到下一个单词
    - `ctrl+up`/`ctrl+down`将光标移动到cell的头/尾
  - 编辑
    - `ctrl+backspace`/`ctrl+delete`删除前/后的单词
    - `ctrl+shift+-`将cell在当前光标后分割
  - 功能
    - `esc`/`ctrl+m`退出编辑模式进入命令模式
    - `ctrl+enter`运行当前cell
    - `shift+enter`运行当前cell并选中下一个cell
    - `alt+enter`运行当前cell并在其后插入新cell

## 魔法函数

使用魔法函数可以简单的实现一些单纯python要很麻烦才能实现的功能。 

* % 行魔法函数，只对本行代码生效。

* %% Cell魔法函数，在整个Cell中生效，必须放于Cell首行。

* %lsmagic 列出所有的魔法函数

* %magic 查看各个魔法函数的说明

* ? 后面加上魔法函数名称，可以查看该函数的说明

 一些常用魔法函数的示例： 

![](https://pic3.zhimg.com/80/v2-e9877938d1aa3614c6d6e0e02cd3f952_1440w.jpg) 