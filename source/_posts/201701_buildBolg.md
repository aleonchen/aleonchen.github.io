---
title: 小白从零搭建博客系统
date: 2017-01-18 14:28:54
tags: [hexo, markdown, github]
---

摘要：本文详细介绍了用Hexo从头免费搭建一个个人博客的教程，包含了macOS的工具准备，Markdown的撰写等等，博主会持续更新。
>Last Update: 2017-02-04

<!-- more -->

# 正文 
## 起步
搭建自己的博客系统，最终的目的是希望有一个称手的工具，可以便捷的表达自己的想法，成果和生活感悟。为了做到这一点需要很多的前提条件，需要写作、发布、更新、展示等等。在技术层面，需要一台电脑写作，需要写作软件，需要一台服务器，还需要一套管理和发布流程。Word哥，不要紧，本教程就是一步步整理我的整个搭建系统的流程，教小白从头搭建自己的博客系统。
> PS: 初稿给小白看了下，表示完全看不懂  (⊙ˍ⊙)，看来还有好长的路要走

## 准备工作
首先是要了解整个博客系统能够顺利发布需要那几个步骤，各位看官可以看下下面的流程图。（貌似hexo并不支持flowchat.js)

```flow
st=>start: 开始写博客
e=>end: 完成
cond1=>condition: Mac电脑

op1_1=>operation: 买台Mac,windows不在讨论之列

op1=>operation: 系统篇
op2=>operation: 域名篇
op3=>operation: 服务器篇
op4=>operation: 写作/发布篇

st->cond1
cond1(yes)->op1->op2->op3->op4->e
cond1(no)->op1_1(right)->e
```

先做个铺垫，基本上这是个程序员的建设历程，如果你觉得打开Terminal(命令行)，看着字符跑来跑去很有趣，那么你可以关闭本文了。本文有点高能，不太适合你，亦或者你是个颜值很高的人，你可以尝试联系我🍹。

## 设置篇
大家觉得搞个bolg不就是去开个账号，然后开写就结束了？咳咳，作为一个动手能力强的程序员，怎么可能选择这么容易的方案？当然是从装脚手架开始，各种系统都要装上尝试下（比如在Markdown里面画流程图），然后打造一个轮子。为了记录，将需要的工具挨个记录和点评，排名不分前后。
> 因为还没有整理的非常好，这部分会不断的更新。

### 基础工具 - Oh My Zsh [官网](http://ohmyz.sh/)
![zsh](http://macshuo.com/wp-content/uploads/2013/07/zsh1.png)
大部分工程师从windows迁移过来的一个非常核心的原因就是windows下面没有非常好用的shell。因为web编程的服务端大多都是Linux，极度依赖shell，下面你也将看到，基本上整个系统的搭建也是极度依赖于shell的脚本和各种包管理体系。

Mac自带了Bash等shell环境，但是太弱了，比如高亮这个必备的功能就没有，所以定制不可避免。ZSH有什么好处我就不安利了，大家可以去看池大的文章（[原文链接](http://macshuo.com/?p=676)），包括后期的定制都可以找到很多线索。

自行安装脚本 `wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh`

我比较喜欢简洁的配色，所以用的主题是avit

> 需要一些基础的配置，后续在补充

### 安装系统 - Home brew [官网](http://brew.sh/index_zh-cn.html)
就像windows安装完系统，我的第一件事情就是安装360软件管家（别吐槽，这个货的确方便）就像苹果的App Store一样，有一个信任的软件安装入口和渠道是省了不少事情的。好在Mac下面有很多靠谱的软件安装工具。brew就是方便的软件之一，本身他是用ruby写就的，ruby也是包管理的鼻祖。

`/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

装完之后，几乎所有的软件都可以用brew来安装，比如`brew cask sublime` 装sublime text软件

### 代码管理 - Git
整个系统的文档管理都是基于Git的版本管理系统，可以用brew安装
`brew install git`

### 博客构建系统 - Hexo [官网](https://hexo.io/)
在很早以前blog还是wordpress的天下，很多设计师和程序员靠定制wordpress的模板就可以横行天下。那是世界上最好的语言PHP写就的，不过太复杂，太古老，不是和我们新世纪的程序员。自从最大的男性交友社区Github推出pages服务以来，大家都在上面纷纷搭建系统，显得很酷(其实，主要是托管不要钱)。然后就出现了很多静态博客生成模板，最早期是Jekyll的，包括现在coding在内的很多git服务都有支持这个。但是但是，因为不可告人的原因，我选择了Hexo，而且的确比较好用

Hexo 官网介绍
> A fast, simple & powerful blog framework

先去安装下:
`npm install hexo-cli -g`

又冒出一个npm, 这个暂且不表可以先用`brew install npm`完成

```
npm install hexo-cli -g
hexo init blog
cd blog
npm install
hexo server
```

弄完这几个命令，不出意外地话会看到

```
INFO  Start processing
INFO  Hexo is running at http://localhost:4000/. Press Ctrl+C to stop.
```

浏览器里面访问下`http://localhost:4000/`基本上，你就有了第一个blog，然后就可以开始愉快的写blog了？

> Too Young, Too Naive

### 发布
如果是你土豪，或者说你想自己尝试一下从零搭建一台博客服务器，那么你可以选择自己买台服务器。否则还是推荐用Github的Pages服务。一来，你有地方可以安防自己的博客文章，顺带有版本管理。二来，你也有了免费的博客空间，再搭配Hexo就可以把博客从本地搬到网上了，不过这两年GibHub经常被墙，还是要小心哈。
注册号Github创建好工程，创建项目仓库，记得在`Setting`里面修改GitHub Pages的相关设置，我这里选择`master branch`
![github_pages](media/github_pages.png)


另外千万记得要设置`repository`名字为`username.github.io`，否则js和css静态文件是不会解析的，详情查看`GitHub Pages`的链接介绍
![create_github_pages](media/create_github_pages.png)


完事了修改`_config.yml` 中的deploy设置

```
deploy:
  type: git
  repo: https://github.com/aleonchen/aleonchen.github.io.git
  branch: master
```

刚才咱们已经用`hexo server`看过本地的博客没问题了。终于开始要发布到网上了

```
hexo g
hexo d
```

纳尼，报错
`ERROR Deployer not found: git`
有人说hexo不支持https的git，其实不是的在V3里面可以的是的你少了个插件
`npm install hexo-deployer-git --save`

第一次运行因为没有登录过github可能会出现

```
*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"
```
配置好即可

应该可以看到效果了，访问下你的blog地址看看

### 更换主题
Hexo的好处之一就是容易更换主题，比如
- [magnetic](https://github.com/klugjo/hexo-theme-magnetic) 
- [Next](https://github.com/iissnan/hexo-theme-next)

下面以magnetic为例：
首先在目录下安装

```
git clone https://github.com/klugjo/hexo-theme-magnetic themes/magnetic
```
然后更新一下`_config.yml`文件将主题更换为 magnetic

```
# Extensions
## Plugins: http://hexo.io/plugins/
## Themes: http://hexo.io/themes/
theme: magnetic
```

### 域名
首先得有一个自己的域名，各位可以去各大网站申请自己的域名，国内就是阿里云腾讯云，国外推荐Godaddy。在CName中设置域名指向自己的github page 主页，我这里是aleonchen.github.io
然后在Github Pages -> Custom domain 设置自己的域名`aleonchen.com`
> 这里有个坑爹的问题，之前在CName里面设置了'blog.aleonchen.com'，后来忘记了，在setting里面怎么修改都不对。发现只要在source/CName文件里面标记正确"aleonchen.com"就可以了，mark下，以免忘记

## 写作篇

### Markdown编辑器 - MWeb [官网](http://zh.mweb.im/index.html)
Markdown是互联网之子的伟大发明，可以用纯文本的方式管理自己的文档，但是效果比word和pages这些二进制的更加优秀。
MWeb是国人的独立开发者的作品，赞誉不胜枚举，现在你们看到的这篇文章也是MWeb这个工具写成的，后面关于发布流程的自动化也是基于这个工具。相关的介绍比较多了，少数派上有不少比如：[这里](http://sspai.com/33855)

### 图片问题
在写博客的时候会碰到一个问题，就是当你使用MWeb在本地撰写文章的时候，图片显示都是好的，但是发布到Github就无法显示图片了。仔细看了下其实是图片路径的问题。按照下面两个步骤操作既可以。
1. 在MWeb引入的时候，只引入`source`目录
2. 引入的时候设置拖入图片的保存位置为**绝对路径**,见下图(如果已经设置过，可以双击`source`)
![source](/media/source-1.png)


### 常规维护
每次写完文章之后输入这个即可
```
hexo -g d
```

### Hexo 配置技巧
1. 如何在首页设置「阅读全文」？
在首页显示一篇文章的部分内容，并提供一个链接跳转到全文页面是一个常见的需求。 NexT官方提供三种方式来控制文章在首页的显示方式。 也就是说，在首页显示文章的摘录并显示 阅读全文 按钮，可以通过以下方法：

1. 在文章中使用 `<!-- more --> `手动进行截断，Hexo 提供的方式 **推荐，本站用了这种方法**
2. 在文章的 front-matter 中添加 description，并提供文章摘录
3. 自动形成摘要，在 主题配置文件 中添加：

```
auto_excerpt:
  enable: true
  length: 150
```
默认截取的长度为 150 字符，可以根据需要自行设定，本站也设置了防止没有做人工摘要。

> 建议使用`<!-- more -->`（即第一种方式），除了可以精确控制需要显示的摘录内容以外， 这种方式也可以让 Hexo 中的插件更好的识别。

# 参考
## 翻墙
翻墙是基础，如果你连翻墙是什么都不知道，请自己去Google（哥只能帮你到这里了 ┑(￣Д ￣)┍）。

我试过非常多的翻墙工具和软件，一般来说分两种，自建和第三方，那么选哪种呢？理论上来说这两个都需要，因为你不知道谁会挂掉，但是如果第三方使用付费的，相对还是靠谱的，毕竟是商业公司。

`自建VPN`，买台国外的服务器，顺便做代理。比较好搭建的是PPTP，但是macOS从v12之后就不再支持这种不安全的VPN方案，目前比较适合的是使用SS，目前还没有搭建过，过两天尝试下。BTW，国外的服务器靠谱的还是不少比如DigitalOcean, Linode等等，这又是一篇话题。

`第三方VPN` 免费的用过goAgent，收费的试过Greenvpn开始，曲径等等。目前一直使用的是云梯。
> 八卦一下,听过一期云梯创始人的讲座，他说**"制作云梯的初衷就是，翻墙是每个人的诉求，但是翻墙比较复杂，让大家都和GFW斗智斗勇，太浪费时间，恰好我们有经验,交给我们好了"**。这个和我的价值观非常符合，节省大家的时间就是生产力，而实际上他们也没有让我失望，一直是我主力的翻墙手段之一。
> BTW: 云梯出了App可以方便的在macOS和iOS切换状态，并且是有自动选择路由的功能，国内不代理，国外才代理（是不是好贴心）

### 参考文章
 
[使用Github Pages搭建个人博客](https://dslztx.github.io/blog/2016/06/25/%E4%BD%BF%E7%94%A8Github-Pages%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/)


