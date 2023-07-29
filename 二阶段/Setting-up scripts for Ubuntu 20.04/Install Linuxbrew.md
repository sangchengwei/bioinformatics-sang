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


if grep -q -i Homebrew $HOME/.bashrc; then
    echo "==> .bashrc already contains Homebrew"
else
    echo "==> Update .bashrc"

 这段脚本片段用于检查用户的 .bashrc 文件是否包含关键词 "Homebrew"，并根据结果输出不同的消息。

让我们逐个解释每个部分的含义：

if grep -q -i Homebrew $HOME/.bashrc; then：

if: 是条件语句的关键字，用于判断条件是否成立。
grep: 是用于在文本中搜索指定字符串的命令。-q 选项用于静默搜索（即不输出结果），-i 选项用于忽略大小写。
Homebrew: 是要搜索的关键词，这里是不区分大小写的搜索。
$HOME/.bashrc: 是要搜索的文件路径，这里是用户的 .bashrc 配置文件。
整个条件语句的含义是：在用户的 .bashrc 文件中搜索关键词 "Homebrew"（不区分大小写），如果找到，则条件成立。

echo "==> .bashrc already contains Homebrew"：
如果上面的条件成立，即 .bashrc 文件中包含关键词 "Homebrew"，则执行此行命令。echo 命令用于在终端输出文本信息，这里输出消息 "==> .bashrc already contains Homebrew"。

else：
如果上面的条件不成立，即 .bashrc 文件中没有找到关键词 "Homebrew"，则执行此行命令。

echo "==> Update .bashrc"：
如果条件不成立，则执行此行命令。echo 命令用于在终端输出文本信息，这里输出消息 "==> Update .bashrc"。

整个脚本片段的作用是：检查用户的 .bashrc 文件是否包含关键词 "Homebrew"，如果包含，则输出 "==> .bashrc already contains Homebrew"，否则输出 "==> Update .bashrc"。这样可以向用户提供有关 .bashrc 文件的一些提示信息。


# 在$HOME/.bashrc中配置PATH环境变量
    echo >> $HOME/.bashrc
    echo '# Homebrew' >> $HOME/.bashrc
     #将 homebrew写入该文件夹

     echo "export PATH='$(brew --prefix)/bin:$(brew --prefix)/sbin'":'"$PATH"' >> $HOME/.bashrc
    #将指定路径$(brew --prefix)/bin:$(brew --prefix)/sbin写入默认环境变量$PATH中，再把写好的环境变量写入$HOME/.bashrc文件夹 

通过执行这个命令，可以将 Homebrew 的安装路径添加到用户的 .bashrc 配置文件中，使得 Homebrew 安装的软件包可以在终端中直接运行，同时保留原来的 PATH 环境变量设置。这样用户在终端中运行 Homebrew 安装的软件时，不再需要输入完整路径，而可以直接使用软件包的名称。
这行命令用于将 Homebrew 安装路径添加到用户的 .bashrc 配置文件中，从而使得 Homebrew 安装的软件包在终端中可以直接运行。

让我们逐个解释每个部分的含义：

echo: 是一个命令，用于在终端输出文本信息。

"export PATH='$(brew --prefix)/bin:$(brew --prefix)/sbin'":'"$PATH"': 这是要输出的文本信息。其中包含了两部分：

export PATH='$(brew --prefix)/bin:$(brew --prefix)/sbin': 这是一个 export 命令，用于将路径设置为环境变量 PATH 的值。$(brew --prefix) 是一个命令替换，它将执行 brew --prefix 命令并将结果（Homebrew 的安装路径）替换进去。/bin 和 /sbin 是 Homebrew 安装的软件包所在的路径。通过这个命令，将 Homebrew 的安装路径添加到 PATH 环境变量中，使得终端可以直接找到并执行 Homebrew 安装的软件包。

"$PATH": 这是另一个命令替换，它将当前的 PATH 环境变量的值替换进去。在添加 Homebrew 安装路径后，这里是为了保留原来的 PATH 环境变量的值，使得系统仍然可以找到其他系统路径中的可执行文件。

>> $HOME/.bashrc: 这是输出重定向操作符，它用于将上述文本信息追加到用户的 .bashrc 配置文件中。$HOME 是一个环境变量，表示当前用户的主目录路径，所以 >> $HOME/.bashrc 的作用是将输出添加到当前用户的 .bashrc 文件末尾。

通过执行这个命令，可以将 Homebrew 的安装路径添加到用户的 .bashrc 配置文件中，使得 Homebrew 安装的软件包可以在终端中直接运行，同时保留原来的 PATH 环境变量设置。这样用户在终端中运行 Homebrew 安装的软件时，不再需要输入完整路径，而可以直接使用软件包的名称。

    echo "export MANPATH='$(brew --prefix)/share/man'":'"$MANPATH"' >> $HOME/.bashrc
    #MANPATH man手册的默认路径
    通过执行这个命令，可以将 Homebrew 的 man 页面路径添加到用户的 .bashrc 配置文件中，使得系统可以正确找到和显示 Homebrew 安装的软件包的 man 手册页。这样，当用户在终端中使用 man 命令查看 Homebrew 安装的软件包的手册页时，系统将能够正确地找到和显示相应的文档。

    echo "export INFOPATH='$(brew --prefix)/share/info'":'"$INFOPATH"' >> $HOME/.bashrc
    #INPUTRC 默认键盘映象
通过执行这个命令，可以将 Homebrew 的 Info 页面路径添加到用户的 .bashrc 配置文件中，使得系统可以正确找到和显示 Homebrew 安装的软件包的 Info 手册页。这样，当用户在终端中使用 info 命令查看 Homebrew 安装的软件包的手册页时，系统将能够正确地找到和显示相应的文档。

    echo "export HOMEBREW_NO_ANALYTICS=1" >> $HOME/.bashrc
     #通过执行这个命令，可以向用户的 .bashrc 配置文件中添加一行配置，设置环境变量 HOMEBREW_NO_ANALYTICS 的值为 1，从而禁用 Homebrew 的分析功能。这样，当用户使用 Homebrew 的时候，Homebrew 将不会收集和发送分析数据，保护用户的隐私。

    echo 'export HOMEBREW_BREW_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git"' >> $HOME/.bashrc
     #通过执行这个命令，可以向用户的 .bashrc 配置文件中添加一行配置，设置 Homebrew 的 Git 远程仓库地址为清华大学的镜像地址，从而加快 Homebrew 的更新速度。

    echo 'export HOMEBREW_CORE_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git"' >> $HOME/.bashrc
     #这行命令用于向用户的 .bashrc 配置文件中添加一行配置，设置 Homebrew Core 的 Git 远程仓库地址为清华大学的镜像地址。
        Homebrew Core 是 Homebrew 中的一个核心仓库，它包含了许多常用的软件包和工具，是 Homebrew 的默认软件包仓库。Homebrew Core 中的软件包经过社区维护和验证，通常是稳定且经过测试的版本。用户可以使用 Homebrew 命令来从 Homebrew Core 安装和管理这些软件包。

    echo 'export HOMEBREW_BOTTLE_DOMAIN="https://mirrors.tuna.tsinghua.edu.cn/homebrew-bottles"' >> $HOME/.bashrc
     #通过执行这个命令，可以向用户的 .bashrc 配置文件中添加一行配置，设置 Homebrew Bottles 的镜像地址为清华大学的镜像地址，从而加快 Homebrew 下载预编译的软件包的速度。这样，在使用 Homebrew 安装软件时，Homebrew 将从清华大学的镜像服务器获取预编译的软件包，提高下载速度和安装效率
    echo >> $HOME/.bashrc
    #设置环境变量，用echo将path写入文件夹
fi
#环境变量
  一个主要作用是提供了一种标准化的配置方式，使得不同的程序可以在同一个系统上运行，并且可以共享一些公共的配置信息。这样，当需要更改某个配置时，只需修改环境变量的值，而无需修改每个使用这个配置的程序。因此，环境变量在计算机操作系统中扮演了重要的角色，对于系统和应用程序的配置和行为具有广泛的影响。

source $HOME/.bashrc
#source $HOME/.bashrc 是一个 Bash 命令，用于重新加载用户的 .bashrc 配置文件，使得其中的环境变量和配置项立即生效，无需重新启动终端。
