## Install packages managed by Linuxbrew

Packages include:

* Programming languages: Perl, Python, R, Java, Lua and Node.js
* Some generalized tools

```shell script
bash $HOME/Scripts/dotfiles/brew.sh
source $HOME/.bashrc
```
 ##  brew.sh  内容
 ```shell script
 #!/bin/bash

export HOMEBREW_NO_AUTO_UPDATE=1
#export [-fnp][变量名称]=[变量设置值]export 可新增，修改或删除环境变量，供后续执行的程序使用。
#改变环境变量，禁用homebrew更新，直到使用brew install,brew upgrade, brew tap 命令

# export ALL_PROXY=socks5h://localhost:1080
#使用环境变量设置代理，设置代理，只在当前终端有效；写入配置文件(如: .bashrc)永久有效
#socks5h用于本地不能解析目标主机域名(比如google),由代理服务器解析目标主机域名
补充：
代理（英语：Proxy），也称网络代理，是一种特殊的网络服务，允许一个网络终端（一般为客户端）通过这个服务与另一个网络终端（一般为服务器）进行非直接的连接。一些网关、路由器等网络设备具备网络代理功能。一般认为代理服务有利于保障网络终端的隐私或安全，防止攻击。


# Clear caches
rm -f $(brew --cache)/*.incomplete

echo "==> gcc"
RELEASE=$( ( lsb_release -ds || cat /etc/*release || uname -om ) 2>/dev/null | head -n1 )
if [[ $(uname) == 'Darwin' ]]; then
    brew install pkg-config
else
    if echo ${RELEASE} | grep CentOS > /dev/null ; then
        brew install gcc
        brew install pkg-config
        brew unlink pkg-config
    else
        brew install gcc
        brew install pkg-config
        brew unlink pkg-config
    fi
fi

# perl
echo "==> Install Perl 5.34"
brew install perl

if grep -q -i PERL_534_PATH $HOME/.bashrc; then
    echo "==> .bashrc already contains PERL_534_PATH"
else
    echo "==> Updating .bashrc with PERL_534_PATH..."
    PERL_534_BREW=$(brew --prefix)/Cellar/$(brew list --versions perl | sed 's/ /\//' | head -n 1)
    PERL_534_PATH="export PATH=\"$PERL_534_BREW/bin:\$PATH\""
    echo '# PERL_534_PATH' >> $HOME/.bashrc
    echo $PERL_534_PATH    >> $HOME/.bashrc
    echo >> $HOME/.bashrc

    # make the above environment variables available for the rest of this script
    eval $PERL_534_PATH
fi

hash cpanm 2>/dev/null || {
    curl -L https://cpanmin.us |
        perl - -v --mirror-only --mirror http://mirrors.ustc.edu.cn/CPAN/ App::cpanminus
}

# Some building tools
echo "==> Building tools"
brew install autoconf libtool automake # autogen
brew install cmake
brew install bison flex

# libs
brew install gd gsl jemalloc boost # fftw
brew install libffi libgit2 libxml2 libgcrypt libxslt
brew install pcre libedit readline sqlite nasm yasm
brew install bzip2 gzip libarchive libzip xz
# brew link --force libffi

# python
brew install python@3.9

if grep -q -i PYTHON_39_PATH $HOME/.bashrc; then
    echo "==> .bashrc already contains PYTHON_39_PATH"
else
    echo "==> Updating .bashrc with PYTHON_39_PATH..."
    PYTHON_39_PATH="export PATH=\"$(brew --prefix)/opt/python@3.9/bin:$(brew --prefix)/opt/python@3.9/libexec/bin:\$PATH\""
    echo '# PYTHON_39_PATH' >> $HOME/.bashrc
    echo ${PYTHON_39_PATH} >> $HOME/.bashrc
    echo >> $HOME/.bashrc

    # make the above environment variables available for the rest of this script
    eval ${PYTHON_39_PATH}
fi

# https://github.com/Homebrew/homebrew-core/issues/43867
# Upgrading pip breaks pip
#pip3 install --upgrade pip setuptools wheel

# r
# brew install wang-q/tap/r@3.6.1
hash R 2>/dev/null || {
    echo "==> Install R"
    brew install r
}

cpanm --mirror-only --mirror http://mirrors.ustc.edu.cn/CPAN/ --notest Statistics::R
# 这里出了一些问题   Command 'cpanm' not found, but can be installed with:sudo apt install cpanminus
这条命令的目的是通过 cpanm 工具，使用指定的 CPAN 镜像源（中国科学技术大学的镜像站点）来下载并安装 Perl 模块 Statistics::R。设置镜像源可以加快模块的下载速度，并且由于指定了 --notest，在安装模块时不会运行测试，加快安装的速度。
问题已解决

# java
echo "==> Install Java"
if [[ "$OSTYPE" == "darwin"* ]]; then
    brew install openjdk
else
    brew install openjdk
    # brew link openjdk --force
fi
brew install ant maven

# pin these
# brew pin perl
# brew pin python@3.9
# brew pin r

# other programming languages
brew install lua node

# taps
brew tap wang-q/tap
# 出了一些问题，需要连接到代理7890 问题已解决



# downloading tools
brew install aria2 curl wget

# gnu
brew install gnu-sed gnu-tar

# other tools
brew install screen stow htop parallel pigz
brew install tree pv
brew install jq jid pup
brew install datamash miller tsv-utils
# 问题，第三个 tsv-utils 无法安装，需要安装gcc,运行：sudo apt install gcc
brew install librsvg udunits
brew install proxychains-ng

brew install bat exa tealdeer # tiv
brew install hyperfine ripgrep tokei
brew install bottom # zellij

# large packages
if [[ "$OSTYPE" == "darwin"* ]]; then
    brew install gpg2
fi

hash pandoc 2>/dev/null || {
    brew install pandoc
}

hash gnuplot 2>/dev/null || {
    brew install gnuplot
}

hash dot 2>/dev/null || {
    brew install graphviz
}

hash convert 2>/dev/null || {
    brew install imagemagick
}

# weird dependancies by Cairo.pm
# brew install linuxbrew/xorg/libpthread-stubs linuxbrew/xorg/renderproto linuxbrew/xorg/kbproto linuxbrew/xorg/xextproto

# gtk+3
# brew install gsettings-desktop-schemas gtk+3 adwaita-icon-theme gobject-introspection