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
桑程巍

## https://raw.githubusercontent.com/wang-q/ubuntu/master/prepare/1-apt中内容：
```shell script

echo "====> Install softwares via apt-get 通过apt-get安装软件<====" 

1. echo这是一个命令，用于在终端输出文本,用于输出信息、调试脚本或提供用户界面；
2."====> Install softwares via apt-get: 这是要输出的文本内容。它是一个提示或说明性的消息，表示接下来将通过apt-get命令安装软件。
3.apt-get，Advanced Package Tool，是一条linux命令，适用于deb包管理式的操作系统，主要用于自动从互联网的软件仓库中搜索、安装、升级、卸载软件或操作系统。

echo "==> Disabling the release upgrader禁用发布升级程序"
sudo sed -i.bak 's/^Prompt=.*$/Prompt=never/' /etc/update-manager/release-upgrades
