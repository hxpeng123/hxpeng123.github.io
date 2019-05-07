---
layout: default
title: testt
subtitle: testt
date: 2019-02-11 22:36:30
author: hxpeng
---

# Mac机器上安装homebrew插件

## 最简单的安装方式

一句命令：

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

这个命令走的是github的资源，非常的慢，不用这个

## 手动安装

主要步骤：

下载官方安装文件并命名为brew_install。

```shell
curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install >> brew_install
```

接着，修改文件，
找到`BREW_REPO`行，
将双引号中的`https://github.com/Homebrew/brew`修改为`https://mirrors.ustc.edu.cn/brew.git`。
（新版本HomeBrew可能没有CORE_TAP_REPO这句代码，如果没有不用新增。 如果这个镜像有问题的话，可以换成其他源。）

使用ruby执行这个文件:

```shell
/usr/bin/ruby brew_install
```

这个时候会卡在

```shell
Cloning into '/usr/local/Homebrew/Library/Taps/homebrew/homebrew-core'...
```

这个地方，估计又是资源问题，解决办法就是手动更换国内镜像源。

执行：

```shell
git clone git://mirrors.ustc.edu.cn/homebrew-core.git/ /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core --depth=1
```

把homebrew-core包用中科院的镜像。

然后设置homebrew的远程镜像，

进入homebrew的根路径：

```shell
cd "$(brew --repo)"
```

执行命令替换git远程分支为中科院的：

```shell
git remote set-url origin https://mirrors.ustc.edu.cn/brew.git
```

同样的，进入homebrew-core的根目录：

```shell
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
```

替换远程分支：

```shell
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
```

然后执行更新命令：

```shell
brew update
```

再检查：

```shell
brew doctor
```

* * *

修改默认源

替换核心软件仓库

```shell
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
```

替换 Bottles 源（Homebrew 预编译二进制软件包）

```shell
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.bash_profile
source ~/.bash_profile
```

* * *

![mac_install_homebrew](/assets/mac_install_homebrew.png)
参考来自：
<https://juejin.im/post/5c738bacf265da2deb6aaf97>
