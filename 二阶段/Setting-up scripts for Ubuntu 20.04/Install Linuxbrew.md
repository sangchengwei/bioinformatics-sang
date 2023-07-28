# Install Linuxbrew
使用清华的[镜像](https://mirrors.tuna.tsinghua.edu.cn/help/homebrew/).

#与该文章类似[文章链接](https://mirrors.tuna.tsinghua.edu.cn/help/homebrew/)

```shell script
echo "==> Tuna mirrors of Homebrew/Linuxbrew"  #使用清华镜像，在终端输入以下几行命令设置环境变量
export HOMEBREW_BREW_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git"
export HOMEBREW_CORE_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git"
export HOMEBREW_BOTTLE_DOMAIN="https://mirrors.tuna.tsinghua.edu.cn/homebrew-bottles"

这行命令是用于设置环境变量 HOMEBREW_BREW_GIT_REMOTE 的值。在这个命令中，环境变量的值被设置为 https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git
这个环境变量在后续的操作中可能会被使用，具体使用方式取决于相关的应用程序或脚本。


git clone --depth=1 https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/install.git brew-install
/bin/bash brew-install/install.sh
这组命令用于在 macOS 或 Linux 系统上使用特定镜像安装 Homebrew，以加快下载速度。Homebrew 是一个流行的 macOS 和 Linux 软件包管理器，可轻松安装和管理各种软件包。
1.git clone：这个命令用于克隆一个 Git 代码仓库。
--depth=1：这个选项指定只克隆最新的提交历史（深度 1），而不包括完整的仓库历史。这样可以减少下载的数据量，加快克隆过程。
https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/install.git：这是要克隆的 Git 仓库的 URL。在这里，它是 Homebrew 安装程序的地址，托管在清华大学的镜像上，这是一个为中国用户提供更快下载速度的镜像。
 git clone如果我们克隆仓库这个仓库，会把所有的历史协作记录都clone下来，这样整个文件会非常大，其实对于我们直接使用仓库，而不是参与仓库工作的人来说，只要把最近的一次commit给clone下来就好了。这就好比一个产品有很多个版本，我们只要clone最近的一个版本来使用就行了。

/bin/bash brew-install/install.sh
/bin/bash：这指定要用于执行脚本的 Shell。
brew-install/install.sh：这是要执行的脚本的路径。该脚本是在前一步中克隆的 Homebrew 仓库中的一部分。


rm -rf brew-install
这段命令的意思是删除名为 "brew-install" 的目录及其内容。
rm: 这是删除 (remove) 的命令。

-rf: 这是 rm 命令的选项。其中：

-r: 表示递归地删除目录及其内容。
-f: 表示强制删除，不会询问确认。
brew-install: 这是要删除的目录的名称。在前面的命令中，我们使用 git clone 命令将 Homebrew 的安装程序克隆到了一个名为 "brew-install" 的目录中。现在，这个命令将删除这个目录及其所有内容，包括其中的文件和子目录。

#安装成功后需将 brew 程序的相关路径加入到环境变量中：
#以下针对 Linux 系统上的 Linuxbrew：

test -d ~/.linuxbrew && PATH="$HOME/.linuxbrew/bin:$HOME/.linuxbrew/sbin:$PATH"
test -d /home/linuxbrew/.linuxbrew && PATH="/home/linuxbrew/.linuxbrew/bin:/home/linuxbrew/.linuxbrew/sbin:$PATH"

test -d ~/.linuxbrew && PATH="$HOME/.linuxbrew/bin:$HOME/.linuxbrew/sbin:$PATH"：

test -d ~/.linuxbrew: 这是一个条件测试语句，用于检查当前用户的主目录（~）下是否存在 .linuxbrew 目录。条件测试中的 -d 表示检查是否是一个目录。
&&: 这是逻辑 AND 运算符，它表示在前一个条件测试成功（即目录存在）时，执行后面的命令。
PATH="$HOME/.linuxbrew/bin:$HOME/.linuxbrew/sbin:$PATH"：这个命令用于将 Linuxbrew 安装路径添加到环境变量 PATH 中。$HOME/.linuxbrew/bin 和 $HOME/.linuxbrew/sbin 是 Linuxbrew 的二进制文件和脚本所在的路径，$PATH 是原来的 PATH 环境变量。这个命令的作用是将 Linuxbrew 的路径放在原来 PATH 的前面，以便让系统优先使用 Linuxbrew 安装的软件。
test -d /home/linuxbrew/.linuxbrew && PATH="/home/linuxbrew/.linuxbrew/bin:/home/linuxbrew/.linuxbrew/sbin:$PATH"：

test -d /home/linuxbrew/.linuxbrew：这是一个条件测试语句，用于检查 /home/linuxbrew/ 目录下是否存在 .linuxbrew 目录。
&&：逻辑 AND 运算符，表示在前一个条件测试成功（即目录存在）时，执行后面的命令。
PATH="/home/linuxbrew/.linuxbrew/bin:/home/linuxbrew/.linuxbrew/sbin:$PATH"：这个命令与第一行类似，用于将 /home/linuxbrew/ 目录下的 Linuxbrew 安装路径添加到环境变量 PATH 中。
这两行命令都用于检查 Linuxbrew 是否已经安装，并将 Linuxbrew 的路径添加到 PATH 环境变量中。根据实际安装的位置，其中一个命令会生效，而另一个则会被跳过。这样可以确保在安装了 Linuxbrew 的情况下，系统能够正确地找到并使用 Linuxbrew 安装的软件。