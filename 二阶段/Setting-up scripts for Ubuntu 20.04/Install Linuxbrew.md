# Install Linuxbrew
使用清华的[镜像](https://mirrors.tuna.tsinghua.edu.cn/help/homebrew/).

#与该文章类似[文章链接](https://mirrors.tuna.tsinghua.edu.cn/help/homebrew/)

```shell script
echo "==> Tuna mirrors of Homebrew/Linuxbrew"  #使用清华镜像，在终端输入以下几行命令设置环境变量
export HOMEBREW_BREW_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git"
export HOMEBREW_CORE_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git"
export HOMEBREW_BOTTLE_DOMAIN="https://mirrors.tuna.tsinghua.edu.cn/homebrew-bottles"


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