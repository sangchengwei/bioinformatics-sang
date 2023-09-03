```shell script
bash $HOME/Scripts/dotfiles/install.sh
source $HOME/.bashrc
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
vim +PluginInstall +qall
```
Edit `.gitconfig` to your own manually.

vim 是启动 Vim 文本编辑器的命令。
+PluginInstall 是 Vim 的参数，它告诉 Vim 在启动时执行 PluginInstall 命令，这通常用于安装插件。
+qall 是 Vim 的参数，它告诉 Vim 在执行完 PluginInstall 命令后退出 Vim。


#  $HOME/Scripts/dotfiles/install.sh内容：
```
#bash $HOME/Scripts/dotfiles/install.sh内容：

#!/usr/bin/env bash

# check gnu stow is installed
hash stow 2>/dev/null || {
    echo >&2 "GNU stow is required but it's not installed.";
    echo >&2 "Install with homebrew: brew install stow";
    exit 1;
}
#如果系统中已经有了stow，直接hash调取，出错写入/dev/null文件；不管成功与否，都进行下一步
# >&2：将进度信息写入stderr，这样脚本即可以方便地和其他应用协作（通过管道或者重定向到文件作为其他应用的输入），同时也可以在屏幕上看到进度。
#exit（1）：非正常运行导致退出程序



# colors in term
# http://stackoverflow.com/questions/5947742/how-to-change-the-output-color-of-echo-in-linux
GREEN=
RED=
NC=
if tty -s < /dev/fd/1 2> /dev/null; then
  GREEN='\033[0;32m'
  RED='\033[0;31m'
  NC='\033[0m' # No Color
fi
#2>/dev/null意思就是把错误输出到“黑洞”
#tty(teletypewriter)指令查询目前使用的终端机的文件名称，-s或--silent或--quiet 不显示任何信息，只回传状态代码。
#/dev/fd/1是指标准输出
#设置字体颜色


# echo -e 处理特殊字符
log_warn () {
  echo -e "==> ${RED}$@${NC} <=="
}
#出现warn，用红色显示

log_info () {
  echo -e "==> ${GREEN}$@${NC}"
}
#出现info提示，用绿色显示

log_debug () {
  echo -e "==> $@"
}
#出现bug



# enter BASE_DIR
BASE_DIR=$( cd "$( dirname "${BASH_SOURCE[0]}" )" && pwd )
cd "${BASE_DIR}" || exit
#将目录挂载到$HOME/Scripts/dotfiles/下，后退出


# stow configurations
mkdir -p ~/.config
#创建~/.config目录


log_warn "Restow dotfiles"
#出现警示提示“Restow dotfiles”
DIRS=( stow-git stow-latexmk stow-perltidy stow-screen stow-wget stow-vim stow-proxychains )


for d in ${DIRS[@]}; do
    log_info "${d}"
    for f in $(find ${d} -maxdepth 1 | cut -sd / -f 2- | grep .); do
        homef="${HOME}/${f}"
        if [ -h "${homef}" ] ; then
            log_debug "Symlink exists: [${homef}]"
        elif [ -f "${homef}" ] ; then
            log_debug "Delete file: [${homef}]"
            rm "${homef}"
        elif [ -d "${homef}" ] ; then
            log_debug "Delete dir: [${homef}]"
            rm -fr "${homef}"
        fi
    done
	stow -t "${HOME}" "${d}" -v 2
done
#d是DIRS=( stow-git stow-latexmk stow-perltidy stow-screen stow-wget stow-vim stow-proxychains )中的变量，执行下列命令
#出现信息提示“该变量名称”
#find ${d} -maxdepth 1指定遍历搜索的最大深度。以当前目录 . 作为起始深度1，即只列出当前目录下的所有普通文件
#cut -sd：-s不打印没有包含分界符的行;-d使用指定分界符代替制表符作为区域分界




# don't ruin Ubuntu
log_info "stwo-bash"
#出现信息提示“stwo-bash”
stow -t "${HOME}" stow-bash -v 2
```

# 补充内容:
1.   configure  
![tupian](./pictures/%E5%9B%BE%E7%89%8720.png)
2. tty命令  
![tu](./pictures/%E5%9B%BE%E7%89%8721.png)