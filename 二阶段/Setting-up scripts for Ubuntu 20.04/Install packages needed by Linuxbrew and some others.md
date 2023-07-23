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
  原因喝目的是：通常，操作系统默认使用官方或默认的软件源地址，但有时这些默认地址可能与用户的地理位置较远或网络连接质量较差，导致软件包下载速度慢或出现连接问题。为了改善这种情况，用户可以将软件源切换到临近的镜像源。
