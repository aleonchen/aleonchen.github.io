---
title: 一个高逼格的代码高亮配色gruvbox
date: 2017-01-24 23:39:08
tags: [gruvbox, pycharm]
---

摘要：一个优秀的代码高亮的主题（gruvbox）在SubLime PyCharm Vim中的配置指南

<!-- more -->

# 正文
之前被Asaka安利PyCharm无数回，今天心血来潮折腾PyCharm的配色，先是找来了Materail Theme (话说Sublime下面这绝对是个好配色）
![Pycharm](http://oj8r5ullr.bkt.clouddn.com/20170125.png)
可是怎么弄都不太满意，于是找Asaka问了下PyCharm有没有好的代码高亮配色，他旋即扔了一个URL给我 https://github.com/morhetz/gruvbox
![官方截图](http://oj8r5ullr.bkt.clouddn.com/14852726955113.jpg)
)
看到这个配色,眼睛一亮，好看。本来只是想搞定Pycharm就算了，谁曾想居然这个是Vim的主题，顺便也搞定了，然后看了下Sublime也有Package顺便一起搞定了。

- PyCharm 包括JetBrains其他的用这个即可
https://github.com/caleb/gruvbox-idea
- Sublime 直接在Package Control里面搜gruvbox
- Vim 就比较多点步骤了 
`.vimrc` 文件里面设置 

```
Plugin 'morhetz/gruvbox
```
然后`:PluginInstall` 搞定，在设置

```
colorscheme gruvbox
set background=dark    " Setting dark mode
```

终于三个编辑器看起来是一样的了，然后他又扔了个字体Fira Code给我😂，https://github.com/tonsky/FiraCode 看了下Sublime不支持ligatures，真心搞不动了。

BTW，我看到gruvbox里面介绍24bit的显示效果
https://github.com/morhetz/gruvbox/wiki/Terminal-specific
可我试了下没看到有什么不同，是我的显示器太渣？ 为此我还特地装了newVim，一样效果，谁能告诉？


