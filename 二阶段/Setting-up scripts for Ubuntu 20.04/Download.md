# download 
* Fill $HOME/bin, $HOME/share and $HOME/Scripts.
 这句话是一种指示或要求，其意思是在用户的主目录（$HOME）下创建三个目录：bin、share 和 Scripts。

```shell script
这段命令是一系列用于下载并运行一个名为 download.sh 的脚本的命令。

curl -LO https://raw.githubusercontent.com/wang-q/dotfiles/master/download.sh: 这个命令使用 curl 工具从指定的 URL（https://raw.githubusercontent.com/wang-q/dotfiles/master/download.sh）下载名为 download.sh 的脚本文件。其中：

-L 选项告诉 curl 跟随重定向，即如果有重定向链接，则自动跳转到实际文件所在的链接。
-O 选项告诉 curl 将下载的文件保存为与服务器上的文件名相同的文件。
执行这个命令后，会在当前目录下下载一个名为 download.sh 的脚本文件。

bash download.sh: 这个命令运行了刚刚下载的 download.sh 脚本。通过 bash 命令执行该脚本，可能会执行一系列操作，比如配置文件的设置、软件的安装等，具体取决于脚本的内容。脚本的内容可以在 download.sh 文件中查看。

source $HOME/.bashrc: 这个命令重新加载了用户的 .bashrc 配置文件。在脚本运行过程中，可能对环境变量或其他配置项进行了修改，通过 source 命令重新加载 .bashrc 文件，使得修改后的配置项立即生效，无需重新启动终端。

综合来说，这段命令的目的是从指定的 URL 下载一个名为 download.sh 的脚本，并运行该脚本。脚本的内容可能包含了配置和安装操作。最后，通过重新加载 .bashrc 文件使得可能修改的配置项立即生效。
```
 
##  出现的问题 
  无法下载：需要在Linux系统中设置代理
  ### 设置代理-clash for windows
export hostip=$(cat /etc/resolv.conf |grep -oP '(?<=nameserver\ ).*')
alias vpn='export https_proxy="http://${hostip}:7890";export http_proxy="http://${hostip}:7890";export all_proxy="socks5://${hostip}:7890";'
alias unvpn='unset all_proxy'
  **  通过设置上述别名，用户可以方便地切换使用代理或取消代理，从而在 Linux 系统中使用 Clash for Windows 客户端的代理功能。用户只需在终端中输入 vpn 命令即可设置代理，输入 unvpn 命令即可取消代理。  **

 # 定义用户的环境变量
 .bashrc 是 Bash Shell 的一个配置文件，它位于用户的主目录下。在 Linux 系统中，每个用户都可以在自己的主目录中找到一个名为 .bashrc 的文件。

.bashrc 文件包含一系列 Bash Shell 的设置和配置，可以用于定义用户的环境变量、别名、命令行提示符等。当用户登录时，Bash Shell 会读取并执行 .bashrc 文件中的命令，从而对用户的 Shell 环境进行自定义配置。

 ##  https://raw.githubusercontent.com/wang-q/dotfiles/master/download.sh内容：
```shell script
 #!/usr/bin/env bash   是一个特殊的注释行，通常位于脚本文件的第一行。这行注释在 Unix/Linux 系统中用于指定脚本的解释器。  #!/usr/bin/env 是一个称为 "shebang"（也叫 "hashbang"）的特殊字符序列，它在 Unix/Linux 系统中用于指定脚本解释器的路径。


echo "====> Download Genomics related tools <===="
   下载基因组学相关工具
mkdir -p $HOME/bin
mkdir -p $HOME/.local/bin
mkdir -p $HOME/share
mkdir -p $HOME/Scripts
#在HOME目录下创建新的4个文件夹，且不可重名

# make sure $HOME/bin in your $PATH
if grep -q -i homebin $HOME/.bashrc; then
     echo "==> .bashrc already contains homebin"
else
    echo "==> Update .bashrc"
    忽略大小写，检查用户的 .bashrc 文件中是否已经包含了 "homebin" 字符串，以便避免重复添加配置或在特定条件下执行不同的操作。

    HOME_PATH='export PATH="$HOME/bin:$HOME/.local/bin:$PATH"'
    echo '# Homebin' >> $HOME/.bashrc
    echo $HOME_PATH >> $HOME/.bashrc
    echo >> $HOME/.bashrc
在用户的 .bashrc 配置文件中添加一些配置，将 $HOME/bin 和 $HOME/.local/bin 目录添加到 $PATH 环境变量中，从而让用户的终端会话中可以直接运行这两个目录中的可执行文件。这通常用于方便用户在终端中运行自定义的脚本或程序。

    eval $HOME_PATH     
    将 $HOME/bin 和 $HOME/.local/bin 目录添加到了 $PATH 环境变量中，使得用户可以在终端中直接运行这两个目录中的可执行文件，而无需输入完整的路径。
fi
#若$HOME/.bashrc 文件夹含有Homebin，则显示“已经存在”；如果不包含，则升级homebin，将homebin和$HOME_PATH写入$HOME/.bashrc

# Clone or pull other repos   #复制或者调用其他回购协议
for OP in dotfiles; do
#OP是withncbi和dotfiles中的一个，一个个筛选

    if [[ ! -d "$HOME/Scripts/$OP/.git" ]]; then
    #如果"$HOME/Scripts/$OP/.git"不是目录，即没有这个目录，则

        if [[ ! -d "$HOME/Scripts/$OP" ]]; then
        #如果"$HOME/Scripts/$OP"不是目录，即没有这个目录，则直接克隆OP这个仓库为这个目录

            echo "==> Clone $OP"
            git clone https://github.com/wang-q/${OP}.git "$HOME/Scripts/$OP"
             #将网页中内容直接拷贝到文件中
        else
            echo "==> $OP exists"
            #若"$HOME/Scripts/$OP"为目录，则显示已经存在
        fi
    else
    #如果"$HOME/Scripts/$OP/.git"是目录，已经存在该目录，则
        echo "==> Pull $OP"   调用dotfiles  withncbi"
        pushd "$HOME/Scripts/$OP" > /dev/null
        #使用 pushd 和 popd 命令来执行存储目录路径并删除它的操作
        #pushd+文件目录， 向目录栈中添加相应的文件目录，同时当前工作目录调整到相应的目录下，将命令的输出信息输入到 /dev/null中并且不显示信息
        git pull
        #git pull的作用是从一个仓库或者本地的分支拉取并且整合代码。
        popd > /dev/null
        #popd 命令不仅会将当前目录切换到 上一个父目录，它还会从目录堆栈中删除这个子目录，即OP目录
    fi
done

#目的：如果含有withncbi或者dotfiles，则进入循环，
#如果没有$HOME/Scripts/dotfiles/.git目录也没有$HOME/Scripts/dotfiles目录，就把https://github.com/wang-q/dotfiles.git内容克隆到$HOME/Scripts/dotfiles文件夹中，
#如果已经有了$HOME/Scripts/dotfiles/.git目录，就把$HOME/Scripts/dotfiles内容转移到dev/dull，即把$HOME/Scripts/dotfiles内容全部丢弃，
#回到原来$HOME/Scripts/dotfiles上一级父目录$HOME/Scripts
#直到dotfiles、ncbi都筛查完，退出循环

补充：
!: 在条件语句中的感叹号表示逻辑 NOT，即取反。在这里，! -d 表示目录不存在的条件。

"$HOME/Scripts/$OP/.git": 这是要检查的目录路径，其中 $HOME 是表示用户主目录的环境变量，$OP 是一个变量，可能是脚本中定义的其他值。

if ... ; then: 这是条件语句的开头，表示如果条件成立则执行后面的代码块。

-d "$HOME/Scripts/$OP/.git": 这是条件测试，判断给定的目录是否存在。-d 表示测试目录是否存在。

如果指定的目录 "$HOME/Scripts/$OP/.git" 不存在，则条件为真（true），则执行 if 后面的代码块，否则不执行。

在这个脚本中，可能是用于检查特定的目录是否已经初始化为 Git 仓库。如果目录不存在或者没有 .git 子目录，可能会进行相关的 Git 初始化操作或其他逻辑处理。

# alignDB
# chmod +x $HOME/Scripts/alignDB/alignDB.pl
给该文件$HOME/Scripts/alignDB/alignDB.pl的执行权限

# ln -fs $HOME/Scripts/alignDB/alignDB.pl $HOME/bin/alignDB.pl
b 指向a, 即$HOME/bin/alignDB.pl指向$HOME/Scripts/alignDB/alignDB.pl,即两个目录下存放着相同的文件，不是复制是统一个文件的两个路径

echo "==> Jim Kent bin"
cd $HOME/bin/
#在$HOME/bin/目录使用
输出一条提示信息 "==> Jim Kent bin"，然后将当前工作目录切换到用户主目录下的 bin 目录。可能是为了进行一些与 Jim Kent bin 相关的操作或者执行相关的脚本。


RELEASE=$( ( lsb_release -ds || cat /etc/*release || uname -om ) 2>/dev/null | head -n1 )
#linux中"\"在是一个转义字符，“｜”是一个特殊字符，有“或”的功能 ||上一个命令执行失败后再执行下一个命令
#/etc/*release是系统安装时默认的发行版本信息，通常安装好系统后文件内容不会发生变化。
#用来显示LSB当前版本的描述信息 或 系统安装时默认的发行版本信息 或 打印操作系统和机器硬件CPU名

if [[ $(uname) == 'Darwin' ]]; then
#Darwin是由苹果电脑于2000年所释出的一个开放原始码操作系统。Darwin 是MacOSX操作环境的操作系统成份。
#苹果电脑于2000年把Darwin 释出给开放原始码社群。
#现在的Darwin皆可以在苹果电脑的PowerPC 架构和X86  架构下执行，而后者的架构只有有限的驱动程序支援。

    curl -L https://github.com/wang-q/ubuntu/releases/download/20190906/jkbin-egaz-darwin-2011.tar.gz
 #curl-L 跟随网站的跳转 直接下载这个安装包（curl: 这是 curl 命令的名称，用于发起 HTTP 请求。-L: 这是 curl 命令的选项之一，用于跟随重定向。）

else
    if echo ${RELEASE} | grep CentOS > /dev/null ; then
  #将命令的输出信息输入到 /dev/null中并且不显示信息
  #CentOS是免费的、开源的、可以重新分发的开源操作系统 ，CentOS(Community Enterprise Operating System，
    #中文意思是社区企业操作系统，是Linux发行版之一。CentOS Linux发行版是一个稳定的，可预测的，可管理的和可复现的平台

        curl -L https://github.com/wang-q/ubuntu/releases/download/20190906/jkbin-egaz-centos-7-2011.tar.gz
    else
        curl -L https://github.com/wang-q/ubuntu/releases/download/20190906/jkbin-egaz-ubuntu-1404-2011.tar.gz
    fi
fi \
    > jkbin.tar.gz
#如果uname == 'Darwin'，即系统是苹果系统则下载darwin-2011.tar.gz；如果不，则下载其他系统版本。
#不同系统下载不同版本的Jim Kent bin


echo "==> untar from jkbin.tar.gz"
tar xvfz jkbin.tar.gz x86_64/axtChain
tar xvfz jkbin.tar.gz x86_64/axtSort
tar xvfz jkbin.tar.gz x86_64/axtToMaf
tar xvfz jkbin.tar.gz x86_64/chainAntiRepeat
tar xvfz jkbin.tar.gz x86_64/chainMergeSort
tar xvfz jkbin.tar.gz x86_64/chainNet
tar xvfz jkbin.tar.gz x86_64/chainPreNet
tar xvfz jkbin.tar.gz x86_64/chainSplit
tar xvfz jkbin.tar.gz x86_64/chainStitchId
tar xvfz jkbin.tar.gz x86_64/faToTwoBit
tar xvfz jkbin.tar.gz x86_64/lavToPsl
tar xvfz jkbin.tar.gz x86_64/netChainSubset
tar xvfz jkbin.tar.gz x86_64/netFilter
tar xvfz jkbin.tar.gz x86_64/netSplit
tar xvfz jkbin.tar.gz x86_64/netSyntenic
tar xvfz jkbin.tar.gz x86_64/netToAxt
#使用 tar 命令来解压缩 jkbin.tar.gz 文件并提取其中的特定文件（x 表示提取（解压缩），v 表示在终端显示详细信息，f 表示指定输入文件为 jkbin.tar.gz，z 表示使用gzip进行解压缩。后面的参数是要提取的文件或文件夹的相对路径。）

mv $HOME/bin/x86_64/* $HOME/bin/
#将目录/$HOME/bin/x86_64中的所有文件移到当前目录($HOME/bin/)中
rm jkbin.tar.gz
#删除压缩包
#上面两块：先下载jkbin再解压，再删除压缩包

if [[ $(uname) == 'Darwin' ]]; then
    curl -L http://hgdownload.soe.ucsc.edu/admin/exe/macOSX.x86_64/faToTwoBit
else
    curl -L http://hgdownload.soe.ucsc.edu/admin/exe/linux.x86_64/faToTwoBit
fi \
#下载Linux版本的faToTwoBit
    > faToTwoBit
    #将下载的文件的输出重定向到名为 faToTwoBit 的文件。
mv faToTwoBit $HOME/bin/
#将名为 faToTwoBit 的文件移动到 $HOME/bin/ 目录中。
chmod +x $HOME/bin/faToTwoBit
#给 $HOME/bin/faToTwoBit文件夹的执行权限
```