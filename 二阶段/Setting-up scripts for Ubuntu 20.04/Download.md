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
 
 ##  https://raw.githubusercontent.com/wang-q/dotfiles/master/download.sh内容：