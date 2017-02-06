---
title: Vim支持Nginx的语法高亮 - Ubuntu
date: 2017-02-06 16:57:01
tags: [vim, nginx, gruvbox]
---

摘要：vim越用越爽，nginx是经常要修改的文件，怎么能没有高亮呢？本文结合之前的gruvbox的主题，简单完成设置
![nginx_highlight](/media/nginx_highlight.png)

<!-- more -->

之前有博文[一个高逼格的代码高亮配色gruvbox](http://aleonchen.com/2017/01/24/gruvbox/)提到了一个非常赞的高亮主题，两步即可搞定

# 安装vundle
vundle是vim的一个插件管理工具，非常方便安装其他的plugin. [官网](https://github.com/VundleVim/Vundle.vim)

```
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

编辑`vim ~/.vimrc`

```
set nocompatible              " be iMproved, required
filetype off                  " required

syntax on

" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
" alternatively, pass a path where Vundle should install plugins
"call vundle#begin('~/some/path/here')

" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'

" The following are examples of different formats supported.
" Keep Plugin commands between vundle#begin/end.
" plugin on GitHub repo
Plugin 'tpope/vim-fugitive'
" plugin from http://vim-scripts.org/vim/scripts.html
" Plugin 'L9'
" Git plugin not hosted on GitHub
Plugin 'git://git.wincent.com/command-t.git'
" git repos on your local machine (i.e. when working on your own plugin)
" Plugin 'file:///home/gmarik/path/to/plugin'
" The sparkup vim script is in a subdirectory of this repo called vim.
" Pass the path to set the runtimepath properly.
Plugin 'rstacruz/sparkup', {'rtp': 'vim/'}
" Install L9 and avoid a Naming conflict if you've already installed a
" different version somewhere else.
Plugin 'ascenator/L9', {'name': 'newL9'}

Plugin 'morhetz/gruvbox'
Plugin 'vim-airline/vim-airline'
Plugin 'vim-airline/vim-airline-themes'

" All of your Plugins must be added before the following line
call vundle#end()            " required
filetype plugin indent on    " required
" To ignore plugin indent changes, instead use:
"filetype plugin on
"
" Brief help
" :PluginList       - lists configured plugins
" :PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
" :PluginSearch foo - searches for foo; append `!` to refresh local cache
" :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
"
" see :h vundle for more details or wiki for FAQ
" Put your non-Plugin stuff after this line

colorscheme gruvbox
set background=dark    " Setting dark mode
let g:gruvbox_contrast_dark='hard'
let g:airline_theme='simple'
```

保存之后，再次打开vim 输入 `:PluginInstall`，再打开看看。

# vim打开nginx高亮
vim并不支持nginx的高亮，但是可以通过nginx.vim来针对性的给出高亮，具体的代码如下

```
mkdir -p ~/.vim/syntax/

wget -O ~/.vim/syntax/nginx.vim http://www.vim.org/scripts/download_script.php?src_id=14376

# /usr/local/etc/nginx/vhosts/*为nginx配置文件存放目录
echo "au BufRead,BufNewFile /usr/local/etc/nginx/vhosts/* set ft=nginx" >> ~/.vim/filetype.vim
```
效果不错哟
![nginx_highlight](/media/nginx_highlight.png)




