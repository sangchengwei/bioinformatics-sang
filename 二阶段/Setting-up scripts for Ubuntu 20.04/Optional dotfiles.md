# bash $HOME/Scripts/dotfiles/install.sh
source $HOME/.bashrc
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
vim +PluginInstall +qall


vim 是启动 Vim 文本编辑器的命令。
+PluginInstall 是 Vim 的参数，它告诉 Vim 在启动时执行 PluginInstall 命令，这通常用于安装插件。
+qall 是 Vim 的参数，它告诉 Vim 在执行完 PluginInstall 命令后退出 Vim。