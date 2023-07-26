# Install packages needed by Linuxbrew and some others

```shell script
* 以下在终端的Ubuntu中运行 *

echo "==> When some packages went wrong, check http://mirrors.ustc.edu.cn/ubuntu/ for updating status."
bash -c "$(curl -fsSL https://raw.githubusercontent.com/wang-q/ubuntu/master/prepare/1-apt.sh)" 

echo "==>
在Shell脚本或命令行中，echo 是一个用于输出文本的命令。echo 命令后面可以跟随要输出的文本，文本必须用引号括起来，以便将其视为一个整体
echo命令将文本"==> When some packages went wrong, check http://mirrors.ustc.edu.cn/ubuntu/ for updating status." 输出到标准输出（通常是显示在终端上的输出）。它可能用于向用户提供一条提示或指导，告诉用户在某些软件包出现问题时检查指定的镜像站点以更新状态。

$(...)：这是Shell中的命令替换语法，它会执行括号内的命令，并将命令的输出作为替换结果

bash -c "..."：这是bash命令的一种用法，它允许在命令行上执行一段脚本。在这里，"..." 部分是先前的命令替换，所以整个表达式就是在bash中执行了先前下载的远程脚本内容。

 curl:
 curl 可以通过HTTP、HTTPS、FTP、SCP、SFTP等协议来传输数据，支持多种网络通信协议。它可以用于下载文件、上传文件、执行HTTP请求、测试API接口等。
 -fsSL:
-f (--fail) 表示在服务器错误时，阻止一个返回的表示错误原因的 html 页面；-s，--silent：安静模式。不显示进度表或错误信息，使curl静音，它仍然会输出您请求的数据，甚至可能输出到终端stdout，除非您对它进行重定向；--show-error：当与-s，--silent一起使用时，它会使curl在失败时显示错误消息；-L,--location:如果服务器报告请求的页面已移动到其他位置（用location:header和3xx 响应代码），此选项将使curl在新位置上重新执行请求。
```

## https://raw.githubusercontent.com/wang-q/ubuntu/master/prepare/1-apt中内容：
```shell script
#!/usr/bin/env bash
#!：这是shebang的起始标记，它告诉操作系统下面的路径是解释器的路径
bash：是指定要使用的解释器的名称。在这种情况下，是Bash解释器。
通过设置PATH环境变量，系统可以在命令行或脚本中直接使用可执行文件的名称，而不需要指定完整的路径。当输入一个命令时，系统会根据PATH中列出的目录依次搜索对应的可执行文件，并在找到匹配的文件后执行它。


echo "====> Install softwares via apt-get <===="
echo命令，用于在终端输出一条消息。具体来说，它会输出文本"====> Install softwares via apt-get <====" 到终端。
apt-get  Advanced Package Tool (APT) 系统的一部分，用于简化在系统上安装、更新、升级和删除软件包的过程。


echo "==> Disabling the release upgrader"  禁用版本升级程序
sudo sed -i.bak 's/^Prompt=.*$/Prompt=never/' /etc/update-manager/release-upgrades

这段命令使用 sudo 权限运行 sed 命令来修改 /etc/update-manager/release-upgrades 文件的内容。逐个解释这个命令：

sudo: superuser do 是一个用于以超级用户（root）权限执行命令的关键字。在Linux系统中，只有管理员可以修改某些系统文件，因此需要使用 sudo 来获得足够的权限来执行操作。

sed: 是一个流式文本编辑器，用于处理和转换文本数据。在这个命令中，sed 将用于对文件内容进行替换操作。

-i.bak: 是 sed 命令的选项。-i 表示直接修改文件，而不是将输出显示在终端。.bak 则表示在修改文件时，同时备份原始文件，备份文件的后缀名为 ".bak"。

's/^Prompt=.*$/Prompt=never/': 这是 sed 的替换命令，用于查找文件中以 "Prompt=" 开头的行并将其替换为 "Prompt=never"。具体来说：

^Prompt=.*$: 这是一个正则表达式，用于匹配以 "Prompt=" 开头的完整行。^ 表示行的开头，Prompt= 表示具体的文本，.* 表示零个或多个任意字符，$ 表示行的结尾。
Prompt=never: 这是要替换成的内容，即将匹配到的行替换为 "Prompt=never"。
/etc/update-manager/release-upgrades: 这是要被修改的目标文件的路径。在这个例子中，sed 命令将会修改 /etc/update-manager/release-upgrades 文件的内容。

综合起来，这个命令的作用是在 /etc/update-manager/release-upgrades 文件中查找以 "Prompt=" 开头的行，并将其替换为 "Prompt=never"。同时，在修改文件内容之前，会备份原始文件并保存为 /etc/update-manager/release-upgrades.bak。
简言之： sed –i.bak ‘s/hello/A/’ file.txt
把修改内容保存到file.txt，同时会以file.txt.bak文件备份原来未修改文件内容，以确保原始文件内容安全性，防止错误操作而无法恢复原来内容。


echo "==> Switch to an adjacent mirror"将镜像源转为临近镜像源
  原因和目的是：通常，操作系统默认使用官方或默认的软件源地址，但有时这些默认地址可能与用户的地理位置较远或网络连接质量较差，导致软件包下载速度慢或出现连接问题。为了改善这种情况，用户可以将软件源切换到临近的镜像源。


# https://lug.ustc.edu.cn/wiki/mirrors/help/ubuntu   **Ubuntu 镜像使用帮助**
  cat <<EOF > list.tmp
#编辑文档内容，把Ubuntu系统自带的源修改为国内的源，将下面内容写入list.tmp文件

cat: 是一个命令，用于在终端中查看文件内容。但在这个上下文中，它的作用是将输入的文本内容输出到文件。

<<EOF: 是一个重定向操作符，它告诉系统将后续的输入文本作为标准输入（stdin）。EOF 可以是任何自定义的终止符，但通常使用 EOF (大写) 来表示 End of File。

>: 是输出重定向符号，它将前面的命令执行结果输出到指定的文件。

list.tmp: 是要保存文本内容的目标文件名。在这个例子中，文本内容将被保存到名为 list.tmp 的文件中。


deb https://mirrors.ustc.edu.cn/ubuntu/ focal main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal main restricted universe multiverse
#镜像源文件类型——仓库地址 ——发行版本，即所使用的Ubuntu版本 20.04：focal——软件包分类

1. deb行是相对于二进制软件包的，您可以使用进行安装apt。
2. deb-src相对于源代码包（由下载apt-get source $package），然后进行编译。
仅当您要自己编译某些软件包或检查源代码中是否有错误时，才需要源软件包。普通用户不需要包含此类存储库。
3.main:完全的自由软件。
restricted:不完全的自由软件。
universe:ubuntu官方不提供支持与补丁，全靠社区支持。
muitiverse：非自由软件，完全不提供支持和补丁。


deb https://mirrors.ustc.edu.cn/ubuntu/ focal-security main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal-security main restricted universe multiverse

deb https://mirrors.ustc.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal-updates main restricted universe multiverse

deb https://mirrors.ustc.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal-backports main restricted universe multiverse

1. Backport：是将一个软件的补丁应用到比此补丁所对应的版本更老的版本的行为。这是软件开发过程中维护步骤的一部分。最简单也可能是最常见的例子，就是针对某个软件的某个漏洞的补丁。某个软件的新版本发现了漏洞，通过修补源代码后可以修复；但此软件的旧版本因为源代码不同，而不能通过同样的修补来修复，这时就需要针对旧版本的软件来进行源代码修补了。


## Not recommended  预发布软件源，不建议启用
# deb https://mirrors.ustc.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse

EOF


if [ ! -e /etc/apt/sources.list.bak ]; then
    sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
fi
sudo mv list.tmp /etc/apt/sources.list

首先，检查是否存在 /etc/apt/sources.list.bak 文件，如果不存在，则备份当前的 /etc/apt/sources.list 文件为 /etc/apt/sources.list.bak。
然后，将名为 list.tmp 的文件移动（替换）为 /etc/apt/sources.list 文件，从而更新软件源配置。
该脚本片段可能用于在修改软件源配置前进行备份，以便在修改不成功或出现问题时，能够还原到原始的软件源配置。在完成备份后，再将新的软件源配置应用到 /etc/apt/sources.list 文件。
1. /etc/apt/sources.list是储存镜像源的文件
2. ！-e表示取非，如果filename存在exist，则为假。
3.Copy备份 备份source源文件，复制一份/etc/apt/sources.list 文件，以作备用,其中 sources.list.bak是备份文件名
4. mv /xxx/file/* /xxx/new/
上面的命令代表了将file文件夹下的所有文件都移动到new文件夹下。


#上面几步用于修改镜像源



# Virtual machines needn't this and I want life easier.
# https://help.ubuntu.com/lts/serverguide/apparmor.html   Ubuntu 服务器文档


if [ "$(whoami)" == 'vagrant' ]; then
    echo "==> Disable AppArmor"
    sudo service apparmor stop
    sudo update-rc.d -f apparmor remove
fi
#如果用户为vagrant，则禁用AppArmor
if [ "$(whoami)" == 'vagrant' ]; then: 这是一个条件判断语句，用于检查当前登录的用户是否为 vagrant。$(whoami) 表示获取当前用户的用户名。如果当前用户名是 vagrant，则执行接下来的命令块。

echo "==> Disable AppArmor": 这是一个 echo 命令，用于在终端输出文本信息。在这里，它输出一条消息 "==> Disable AppArmor"。

sudo service apparmor stop: 这是一个 service 命令，用于管理系统服务。apparmor 是一个 Linux 安全模块，用于强化应用程序的安全性。这里的命令是停止 apparmor 服务，即禁用它。

sudo update-rc.d -f apparmor remove: 这个命令用于从系统的启动过程中移除 apparmor 服务。它会禁止 apparmor 在系统启动时自动加载。

整个脚本片段的含义是：如果当前登录的用户是 vagrant，则在终端输出一条消息 "==> Disable AppArmor"，然后停止 apparmor 服务，并从系统启动过程中移除它。这样可以在 vagrant 用户下禁用 apparmor，可能是因为在虚拟机中进行开发或测试时不需要 apparmor 的安全限制。


echo "==> Disable whoopsie"
sudo sed -i 's/report_crashes=true/report_crashes=false/' /etc/default/whoopsie
sudo service whoopsie stop
首先，在终端输出一条消息 "==> Disable whoopsie"，然后修改 /etc/default/whoopsie 文件中的配置，将错误报告功能禁用，最后停止 whoopsie 服务，确保在当前会话中该服务已被停止。这样可以阻止系统错误的自动报告，并禁用 whoopsie 服务。
1.whoopsie是“Ubuntu错误报告”守护程序，默认安装在桌面/服务器安装中。
当某件事崩溃时，whoopsie会做两件事：
收集Apport生成的崩溃报告；将它们发送到Ubuntu /Canonical（具体到https://daisy.ubuntu.com）
2. 用sed -i 's/原字符串/新字符串/' ab.txt ,对每行匹配到的第一个字符串进行替换


echo "==> Install linuxbrew dependences"  安装linuxbrew依赖包
sudo apt-get -y update
sudo apt-get -y upgrade
sudo apt-get -y install build-essential curl file git
sudo apt-get -y install pkg-config libbz2-dev zlib1g-dev libzstd-dev libexpat1-dev
# sudo apt-get -y install libcurl4-openssl-dev libncurses-dev 这个指令则是跳过系统提示,直接安装

1.apt-get update更新软件列表
访问服务器，更新可获取软件及其版本信息，但仅仅给出一个可更新的list
2.具体更新需要通过apt-get upgrade，apt-get upgrade可将软件进行更新
这个命令，会把本地已安装的软件，与刚下载的软件列表里对应软件进行对比，如果发现已安装的软件版本太低，就会提示你更新。如果你的软件都是最新版本，会提示：升级了0个软件包，新安装了0个软件包，要卸载0个软件包，有0个软件包未被升级。
-y: 是一个选项，用于在更新软件包列表时自动回答 "yes"，即自动确认更新，不需要用户手动输入确认。


echo "==> Install other software"
sudo apt-get -y install aptitude net-tools parallel vim screen xsltproc numactl


echo "==> Install develop libraries"
# sudo apt-get -y install libreadline-dev libedit-dev
sudo apt-get -y install libdb-dev libxml2-dev libssl-dev libncurses5-dev libgd-dev
# sudo apt-get -y install gdal-bin gdal-data libgdal-dev # /usr/lib/libgdal.so: undefined reference to `TIFFReadDirectory@LIBTIFF_4.0'
# sudo apt-get -y install libgsl0ldbl libgsl0-dev


# Gtk stuff, Need by alignDB
# install them in a fresh machine to avoid problems



echo "==> Install gtk3"
#GTK+（GIMP Toolkit)是一套源码以LGPL许可协议分发、跨平台的图形工具包。最初是为GIMP写的，已成为一个功能强大、设计灵活的一个通用图形库，是GNU/Linux下开发图形界面的应用程序的主流开发工具之一。

#sudo apt-get -y install libcairo2-dev libglib2.0-0 libglib2.0-dev libgtk-3-dev libgirepository1.0-dev
#sudo apt-get -y install gir1.2-glib-2.0 gir1.2-gtk-3.0 gir1.2-webkit-3.0


echo "==> Install gtk3 related tools" 
# sudo apt-get -y install xvfb glade


echo "==> Install graphics tools"  三种画图工具
sudo apt-get -y install gnuplot graphviz imagemagick


#echo "==> Install nautilus plugins"
#sudo apt-get -y install nautilus-open-terminal nautilus-actions

# Mysql will be installed separately.
# Remove system provided mysql package to avoid confusing linuxbrew.
echo "==> Remove system provided mysql"
#MySQL是一种关联数据库管理系统，使用完整的管理系统统一管理，易于查询。在 WEB 应用方面 MySQL 是最好的 RDBMS(Relational Database Management System：关系数据库管理系统)应用软件之一。

# sudo apt-get -y purge mysql-common


echo "==> Restore original sources.list"
if [ -e /etc/apt/sources.list.bak ]; then
    sudo rm /etc/apt/sources.list
    sudo mv /etc/apt/sources.list.bak /etc/apt/sources.list
fi
整个脚本片段的含义是：首先，在终端输出一条消息 "==> Restore original sources.list"，然后检查是否存在备份文件 /etc/apt/sources.list.bak，如果存在，将原始的软件源配置文件 /etc/apt/sources.list 删除，并将备份文件 /etc/apt/sources.list.bak 重命名为 /etc/apt/sources.list，从而恢复原始的软件源配置。

这样可以确保在需要还原软件源配置时，能够将备份的配置文件重新放回其原来的位置，恢复到之前的状态。
在 Bash 中，条件测试表达式用方括号 [ ] 包围，同时方括号内部的参数和选项之间要有空格。-e (用于检查是否存在) 是方括号内部的选项之一。其他常用的条件测试选项还包括 -f（检查文件是否存在且为普通文件）、-d（检查是否为目录）、-x（检查文件是否可执行）等


echo "====> Basic software installation complete! <===="

```   