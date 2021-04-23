# Python 使用

## 安装

在windows终端命令行

```powershell
where python
```

![](.\image\python安装_1.png)



## pip配置

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



## pip基本使用方法

- 在使用 pip安装 python模块前，需要升级pip到最新版本。打开cmd，执行:

  ```powershell
  python -m pip install pip --upgrade
  ```

  pip会自动卸载老版本并安装最新版本

  **注意**，不要直接使用 pip install pip --upgrade 对pip本身进行升级，在卸载过程中会报EnvironmentError错误。

  修复方法为在cmd中执行:

  ```powershell
  python -m ensurepip
  ```

-  查看已安装包列表

  ```powershell
  py -m pip list
  ```

- 根据包名安装模块

  ```powershell
  py -m pip install SomePackage            # latest version
  py -m pip install SomePackage==1.0.4     # specific version
  py -m pip install 'SomePackage>=1.0.4'     # minimum version
  ```

  **注意**：不建议直接使用 pip的 exe(即 `pip install` ）的方式来安装模块
  
  

## 虚拟环境

虚拟环境是在使用Python同时开发多个Python应用时，用来隔离各个应用之间的模块依赖，解决依赖模块版本冲突的问题。根据[官网](https://docs.python.org/zh-cn/3.7/glossary.html#term-virtual-environment)定义：

> virtual environment – 虚拟环境
>
> 一种采用协作式隔离的运行时环境，允许 Python 用户和应用程序在安装和升级 Python 分发包时不会干扰到同一系统上运行的其他 Python 应用程序的行为。

在Python3中，用于创建和管理虚拟环境的模块称为 [`venv`](https://docs.python.org/zh-cn/3.7/library/venv.html#module-venv)，是Python3的内置模块。如果是Python2的用户则需要使用 [virtualenv](https://virtualenv.pypa.io/en/latest/index.html) 模块创建虚拟环境。

### 创建虚拟环境

- 在windows10、Python3.7中，使用venv创建虚拟环境的基础命令为：

  ```shell
  # 创建虚拟环境，并将其置于当前目录下的demo-venv文件夹中
  python -m venv demo-venv
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

  可以发现虚拟环境中默认只提供了两个Python模块—— pip 和 setuptools

  一般虚拟环境中的pip不是最新版本，需要执行 `python -m pip install --upgrade pip`进行升级