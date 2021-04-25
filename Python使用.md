# Python 使用

## 安装

在windows终端命令行查看

```powershell
where python
```

![](.\image\python安装_1.png)

### 安装目录详情

比如 `C:\Users\Davy\AppData\Local\Programs\Python\Python38`，也就是 Python 的安装路径，它是包含 `python.exe` 的目录。 

其它目录的作用：

- DLLs，动态链接库，里面是一些 `.dll` 和 `.pyd` 文件，一般不会直接和这个目录打交道

- Doc，文档，里面就是一个 `python381.chm`，快捷方式里包含了该文档路径，所以平常不会直接访问

- include，头文件，基本上不会用到

- **Lib**，这个目录最最重要，几乎所有的 **标准库源码** 都在这里面了，大部分平常都不会去动它们，除了其中一个子目录：
* **site-packages** 后续安装的 **第三方** 模块和包都会出现在这里，所以偶尔出现问题，我们会造访这里。
  
- libs，几乎不会直接用到，注意和 `Lib` 区分开。（因为 Windows 系统路径不区分大小写，所以 Lib 实际会展示成 lib ）

- **Scripts**，后续安装的第三方包如果提供了命令，可执行文件就会出现在这里。例如 `pip.exe` 就是在此目录下，而 Lib 目录下保存的是 pip 的源码。

- tcl，说来话长，略过

- Tools，自带的一些 Python 脚本，包括一些 `demo`，其中有些可以作为学习参考。

其实还有一个目录，launcher 的目录，它要管理所有的 Python 版本，所以它是超脱在外的，安装在了其它目录中：

![](.\image\py的安装目录.jpg) 

## pip

pip是 python自带的包管理工具

> pip is the [package installer](https://packaging.python.org/guides/tool-recommendations/) for Python. You can use pip to install packages from the [Python Package Index](https://pypi.org/) and other indexes. 

### pip配置

由于公司网络限制，需要编辑pip的配置文件，配置pip源为公司的源，否则不能正常安装python模块。pip的配置文件：

* windows下 

  全局配置文件路径为 %APPDATA%\pip\pip.ini

  用户配置文件路径为 %HOMEPATH%\pip\pip.ini

  全局配置会覆盖用户配置，如没有手动创建文件夹与文件

* Linux下

   $HOME/.config/pip/pip.conf 
   
```ini
[global]
trusted-host=mirrors.tools.xxxxxx.com
index-url=http://mirrors.tools.xxxxxx.com/pypi/simple
```

在终端中执行 pip config list，可输出 pip的配置信息

```
pip config list
```

### pip基本使用方法

- 在使用 pip安装 python包前，需要升级pip到最新版本。打开cmd，执行:

  ```powershell
  python -m pip install pip --upgrade
  ```

  pip会自动卸载老版本并安装最新版本

  **注意**，不要直接使用 pip install pip --upgrade 对pip本身进行升级，在卸载过程中会报EnvironmentError错误。

  修复方法为在 cmd中执行:

  ```powershell
  python -m ensurepip
  ```

- 查看已安装包列表

  ```powershell
  py -3.8 -m pip list
  ```

  **注意**：用哪个版本的 Python运行 pip，模块就被关联到哪个版本，故最好使用 **py启动器** 指定具体的 Python版本。

- 根据包名安装模块

  ```powershell
  py -3.8 -m pip install Package            # latest version
  py -3.8 -m pip install SomePackage==1.0.4     # specific version
  py -3.8 -m pip install 'SomePackage>=1.0.4'     # minimum version
  ```

  **注意**：不建议直接调用 pip的 exe文件(即 `pip install` ）的方式来管理模块
  
  

## py launcher

> The "py" launcher lets you select which of multiple installed versions of Python to run.  

其针对 **Windows** 操作系统，方便用户具体指定要运行的哪一个版本的 Python。

**Windows** 操作系统下，PATH环境变量中有 python2.7、3.5、3.7多个版本，这会使用系统环境变量中你设置靠前的环境变量来执行，比如 PATH环境变量中，python2.7是靠前的，则是用python2.7运行，如果是python3.6靠前，则是用python3.6运行。

如何指定使用python2.7运行呢，只需这样既可:

```powershell
py -2.7 a.py
```

同理，我们想要用python3.6运行b.py，则只需要这样：

```powershell
py -3.6 b.py
```

### 安装

 在 windows下安装 Python时默认会安装 py launcher，如下图所示：![](.\image\py的安装.jpg) 

### 区分2个默认版本

* py的默认版本
* 系统的python默认版本

```powershell
C:\Users\dean>python
Python 3.7.0 (v3.7.0:1bf9cc5093, Jun 27 2018, 04:59:51) [MSC v.1914 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> quit()

C:\Users\dean>py --list
Installed Pythons found by py Launcher for Windows
 -3.9-64 *
 -3.8-64
 -3.7-64
 -3.6-64
 -3.5-64
 -2.7-64
```



## 虚拟环境

虚拟环境是在使用Python同时开发多个Python应用时，用来隔离各个应用之间的模块依赖，解决依赖模块版本冲突的问题。根据[官网](https://docs.python.org/zh-cn/3.7/glossary.html#term-virtual-environment)定义：

> virtual environment – 虚拟环境
>
> 一种采用协作式隔离的运行时环境，允许 Python 用户和应用程序在安装和升级 Python 分发包时不会干扰到同一系统上运行的其他 Python 应用程序的行为。

在Python3中，用于创建和管理虚拟环境的模块称为 [`venv`](https://docs.python.org/zh-cn/3.7/library/venv.html#module-venv)，是Python3的内置模块。如果是Python2的用户则需要使用 [virtualenv](https://virtualenv.pypa.io/en/latest/index.html) 模块创建虚拟环境。

### 创建虚拟环境

创建过程主要做 2件事，创建系统 python的一个副本（默认不会复制标准库与第三方库），修改 PATH环境变量。

- 在windows10下，以 Python 3.8这个版本使用 venv创建虚拟环境的基础命令为：

  ```powershell
  # 创建虚拟环境，并将其置于当前目录下的demo-venv文件夹中
  py -3.8 -m venv demo-venv
  ```

### 使用虚拟环境

- 激活创建好的虚拟环境：

  ```shell
  # 激活虚拟环境
  demo-venv\Scripts\activate.bat
  ```

  虚拟环境激活后，将在命令行显示正在使用的虚拟环境的名称：

* 查看虚拟环境中有哪些Python模块，运行：

  ```shell
  # 查看环境中的Python模块列表
  python -m pip list
  ```

  可以发现虚拟环境中初始只提供了两个Python模块—— pip 和 setuptools

  一般虚拟环境中的pip不是最新版本，最好执行 `python -m pip install --upgrade pip`进行升级
  
* 在虚拟环境中安装包，与非虚拟环境下一样（前提是先激活虚拟环境 ^_^）

  ```powershell
  # 查看环境中的Python模块列表
  python -m pip install somepackage
  ```

* 退出虚拟环境

  ```powershell
  deactivate
  ```

* 在 Pycharm中使用虚拟环境

  在创建项目时，找到之前已创建好的虚拟环境：

  ![](.\image\在IDE中使用虚拟环境.png)

  或者，新创建一个虚拟环境：

  ![1619339591473](D:\Code\Machine-Learning\image\在IDE中使用虚拟环境_2.png)

*  结合 pip 保存和复制虚拟环境 

  保存

  ```powershell
  python -m pip freeze > requirements.txt
  ```

  复制

  ```powershell
  python -m pip install -r requirements.txt
  ```

  

## anaconda

### 为什么使用它

省去自己安装科学计算所需的各种模块

### 安装

* [官网下载](https://www.anaconda.com/products/individual)

* 添加路径给PATH环境变量  由于我在安装 anaconda 过程中按照器建议没有添加环境变量，这里手动添加

  ```
  xxx\Anaconda3
  xxx\Anaconda3\Scripts
  xxx\Anaconda3\Library\bin
  ```


### 使用

conda是 anaconda中的环境管理器和包管理器 

* 环境虚拟管理

  activate 能将我们引入 anaconda设定的虚拟环境中, 如果你后面什么参数都不加那么会进入anaconda自带的 base环境 

  ```powershell
  activate
  ```

  ![](.\image\anaconda_1.png)

  创建自己的虚拟环境

  ```powershell
  conda create -n python36 python=3.6 
  ```

* 包管理

  安装第三方包

  ```powershell
  conda install SomePackage
  ```

  或者

  ```powershell
  pip install SomePackage
  ```

* Jupyter选用anaconda





## 参考

[Windows 系统安装 Python 3.8 详解](https://zhuanlan.zhihu.com/p/104537494)

[理解Python虚拟环境](https://zhuanlan.zhihu.com/p/108534526)

[一次性讲清楚Python虚拟环境](https://zhuanlan.zhihu.com/p/107168303)

[[Python]Anaconda安装和使用指南](https://zhuanlan.zhihu.com/p/36398337)

