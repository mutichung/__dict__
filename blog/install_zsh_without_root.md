---
title: Install ZSH Without Root
date: 2025-01-01
tags:
  - Linux
  - Dev
draft: false
---
## Introduction

Last week I accidentally overwrote my `.bashrc` file and could not rescue it back (really should have used a dotfiles manager like [Chezmoi](chezmoi)). I then said to myself that this might be the best time to try out some other shells. I've always wanted to try out newer, more modern ones like `zsh` and `fish`, but failed quite a few times given the difficulty to install them without package managers and root access. Therefore, I decided to give it another try during the holiday season.

The below steps and configurations are borrowed from [this CSDN article](https://blog.csdn.net/weixin_43301333/article/details/126801922), since it was the only one I found out to be working.

## Install `ncurses`

The first difficulty I ran into is that the server did not have `ncurses` library. Thus, I had to compile it myself.

```shell
export CXXFLAGS="-fPIC"
export CFLAGS="-fPIC"
export NCURSES_HOME=/path/to/ncurses
export PATH=$NCURSES_HOME/bin:$PATH
export LD_LIBRARY_PATH="$NCURSES_HOME/lib${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}"
export CPPFLAGS="-I$NCURSES_HOME/include" LDFLAGS="-L$NCURSES_HOME/lib"

mkdir -p $NCURSES_HOME && cd $NCURSES_HOME
wget https://ftp.gnu.org/gnu/ncurses/ncurses-6.5.tar.gz
tar -xzvf ncurses-6.5.tar.gz
cd ncurses-6.1
./configure --prefix=$NCURSES_HOME --with-shared --without-debug --enable-widec
make && make install
```

## Install `zsh`

```shell
export ZSH_HOME=/path/to/zsh
mkdir -p $ZSH_HOME && cd $ZSH_HOME
wget https://www.zsh.org/pub/zsh-5.9.tar.xz
tar -xvf zsh-5.9.tar.xz

cd zsh-5.9
./configure --prefix=$ZSH_HOME
make && make install
```

After that, ZSH should be executable as a binary under `$ZSH_HOME/bin`. Remember to add it to your `$PATH` environment variable to run it.

```shell
export PATH=$ZSH_HOME/bin:$PATH
```

## Setting `zsh` as the Default Shell

Since I don't have root permission, `chsh` wouldn't work for me. I ended up adding the following settings to my `.bashrc`:

```shell
export PATH=$ZSH_HOME/bin:$PATH
export SHELL=$ZSH_HOME/bin/zsh
exec zsh
```