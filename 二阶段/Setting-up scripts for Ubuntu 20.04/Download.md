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

# make sure $HOME/bin in your $PATH
if grep -q -i homebin $HOME/.bashrc; then
    echo "==> .bashrc already contains homebin"
else
    echo "==> Update .bashrc"

    HOME_PATH='export PATH="$HOME/bin:$HOME/.local/bin:$PATH"'
    echo '# Homebin' >> $HOME/.bashrc
    echo $HOME_PATH >> $HOME/.bashrc
    echo >> $HOME/.bashrc

    eval $HOME_PATH
fi

# Clone or pull other repos
for OP in dotfiles; do
    if [[ ! -d "$HOME/Scripts/$OP/.git" ]]; then
        if [[ ! -d "$HOME/Scripts/$OP" ]]; then
            echo "==> Clone $OP"
            git clone https://github.com/wang-q/${OP}.git "$HOME/Scripts/$OP"
        else
            echo "==> $OP exists"
        fi
    else
        echo "==> Pull $OP"
        pushd "$HOME/Scripts/$OP" > /dev/null
        git pull
        popd > /dev/null
    fi
done

# alignDB
# chmod +x $HOME/Scripts/alignDB/alignDB.pl
# ln -fs $HOME/Scripts/alignDB/alignDB.pl $HOME/bin/alignDB.pl

echo "==> Jim Kent bin"
cd $HOME/bin/
RELEASE=$( ( lsb_release -ds || cat /etc/*release || uname -om ) 2>/dev/null | head -n1 )
if [[ $(uname) == 'Darwin' ]]; then
    curl -L https://github.com/wang-q/ubuntu/releases/download/20190906/jkbin-egaz-darwin-2011.tar.gz
else
    if echo ${RELEASE} | grep CentOS > /dev/null ; then
        curl -L https://github.com/wang-q/ubuntu/releases/download/20190906/jkbin-egaz-centos-7-2011.tar.gz
    else
        curl -L https://github.com/wang-q/ubuntu/releases/download/20190906/jkbin-egaz-ubuntu-1404-2011.tar.gz
    fi
fi \
    > jkbin.tar.gz

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

mv $HOME/bin/x86_64/* $HOME/bin/
rm jkbin.tar.gz

if [[ $(uname) == 'Darwin' ]]; then
    curl -L http://hgdownload.soe.ucsc.edu/admin/exe/macOSX.x86_64/faToTwoBit
else
    curl -L http://hgdownload.soe.ucsc.edu/admin/exe/linux.x86_64/faToTwoBit
fi \
    > faToTwoBit
mv faToTwoBit $HOME/bin/
chmod +x $HOME/bin/faToTwoBit

```