# Clion使用教程

![toolchains](https://github.com/WlqFigureBed/FigureBed-one/raw/master/img/20210911113253.png)

[官方教程网址](https://www.jetbrains.com/help/clion/quick-tutorial-on-configuring-clion-on-windows.html#Cygwin)

`File` -> `Settings` -> `Build,Execution,Deployment` -> `Toolchains`

![Toolchains](https://github.com/WlqFigureBed/FigureBed-one/raw/master/img/20210912145751.png)

MinGw、Cygwin、WSL其中只要配置其中一个即可，三种本质都是提供如下工具：

- 编译：c、c++
- 调试：gdb
- 自动化编译工具：cmake

![cmake工作流程](https://github.com/WlqFigureBed/FigureBed-one/raw/master/img/20210912153510.png)

**makefile**：对于十分复杂的工程，仅仅有工程的源码是远远不够的，还需要清楚工程中各个文件之间的关系，此时需要makefile文件，来定义一系列的规则，指定文件的编译顺序等。

**cmake**：例如，一个项目在Windows上用VS编译，在Linux上用make编译，在OS X上用XCODE，那么就需要三个文件，分别放置VS的sln文件，Linux的makefile，OS X的XCODE。有了cmake之后，就不需要这三个文件了，只需要一个`CMakeLists.txt`文件即可实现**跨平台**自动编译，自动生成对应平台所需的文件，例如如果是Linux平台就会生成makefile文件，依此类推。

## MinGW

- 点击进入[网址](https://sourceforge.net/projects/mingw-w64/files/)，往下滑
  - posix、win32：选前者，如果开发windows程序选后者
  - sjlj、seh、dwarf：sjlj支持32位和64位，稳定。seh支持64位，dwarf支持32位，性能好。

![下载示意图](https://github.com/WlqFigureBed/FigureBed-one/raw/master/img/20210911113259.png)

- 下载后解压，复制bin目录地址，`右键计算机→属性（Win+Pause/Break）→ 高级系统设置→高级→环境变量`，修改Path变量，添加一条，将bin目录地址复制进去。

- 测试：cmd，输入`gcc -v`。有输出即可！

- 简单使用

  ```cpp
  #include <iostream>
   
  using namespace std;
   
  int main(void)
  {
      cout << endl;
      cout << "Goodbye, 2019!" << endl;
      cout << "Hello, 2020!" << endl;
      cout << "Hello, Windows!" << endl;
  	
      return 0;
  }
  ```

  ![a.cpp](https://github.com/WlqFigureBed/FigureBed-one/raw/master/img/20210911113306.png)

```c
#include <stdio.h>
 
int main(void)
{
    printf("\nGoodbye, 2019! \nHello, 2020! \nHello, Windows!\n");
	
    return 0;
}
```

![b.c](https://github.com/WlqFigureBed/FigureBed-one/raw/master/img/20210911113310.png)

## Cygwin

参见[Clion官方教程网址](https://www.jetbrains.com/help/clion/quick-tutorial-on-configuring-clion-on-windows.html#Cygwin)

Cygwin就是一个Windows软件，该软件就是在Windows上仿真Linux操作系统。

![初次启动Cygwin](https://github.com/WlqFigureBed/FigureBed-one/raw/master/img/20210911113314.png)

## WSL

[Windows官方教程](https://docs.microsoft.com/en-us/windows/wsl/install-win10#manual-installation-steps)

- [windows terminal 美化](https://www.jianshu.com/p/5892c38be655)

- wsl

  ```shell
  # 安装zsh
  sudo apt-get update
  sudo apt-get upgrade
  
  sudo apt-get install -y zsh
  chsh #修改默认shell为 /bin/zsh
  echo $SHELL # 查看修改后的shell
  ```

  ```shell
  # 安装oh-my-zsh
  sudo apt install wget
  sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
  ```

  注意：最后一个命令由于被墙了，无法下载，如下解决：

  - 进入网址：https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh

  - 复制全部内容

  - ```shell
    nano install.sh
    # ctrl + v 粘贴脚本
    # ctrl + s 保存文件
    sh install.sh  # bash install.sh
    ```

  - 如上，安装完毕

  ```shell
  # 安装 Powerlevel10k 主题
  # 安装字体：https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Regular.ttf
  sudo apt install git 
  git clone --depth=1 https://gitee.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
  ```

  重启shell，照着配置下即可！可参考[这篇](https://www.zrahh.com/archives/167.html)

  ```shell
  # 插件安装
  # 1. autojump
  apt install autojump
  
  # 2. zsh-autosuggestions
  git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
  
  # 3. zsh-syntax-highlighting
  git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
  
  vim ~/.zshrc
  # plugins=(git autojump zsh-autosuggestions zsh-syntax-highlighting)
  # bindkey '' autosuggest-accept
  # source $ZSH/oh-my-zsh.sh
  ```


- 配置c++环境

  ```shell
  apt install gdb
  apt install g++
  apt install gcc
  apt install cmake
  ```


# CMake使用教程 todo 21.9.12
