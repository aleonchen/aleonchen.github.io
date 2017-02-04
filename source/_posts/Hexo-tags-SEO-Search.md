---
title: 让博客被Google搜索 Hexo配置/全站搜索/Tags/SEO
date: 2017-02-04 11:30:04
tags: [hexo, local searche, tags, google, SEO]
---

# 摘要
本文介绍了如何在Hexo博客配置全站搜索，创建tags页面和搜索引擎Google SEO。

# 正文
创建好了Hexo装修简直是停不下来的节奏，一方面是既然做了Blog就像把他弄好，另一方，其实在做网站运营方面一直有很多方法没有机会尝试，这次有时间，有机会一定要按照自己的想法尝试一下。首先站内的文章希望有个比较好的结构，可以作为自己的知识储备，那么全站搜索必须做，其次作为运营要让博客能够被找到，SEO必须得做。接下来就是整个过程啦。

## 全站搜索
看了下NexT主题推荐的搜索方式，默认是**Swiftype 搜索**。我注册了之后，很不幸的发现，这个是收费的，只有14天免费期，看了博主的issue发现，Local Search反而是比较靠谱的，也简单。
1. 安装`hexo-generator-searchdb`插件，在站点的根目录下执行以下命令

```
$ npm install hexo-generator-searchdb --save
```

2. 编辑站点配置文件`_config.yml`，新增以下内容到任意位置：

```
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```

重新发布就OK了

## 添加标签tags
为了被搜索引擎爬取，站点的主题最好比较明确，所以添加关键字是比较好的做法，每篇文章添加tags。
1. 添加一个标签云页面，并在菜单中显示页面链接。

新建一个页面，命名为 tags 。命令如下：

```
hexo new page "tags"
```
2. 编辑刚新建的页面，将页面的类型设置为 tags ，主题将自动为这个页面显示标签云。

```
title: 所有标签
date: 2017-02-04 11:07:24
type: "tags"
---
```
注意：如果有启用多说 或者 Disqus 评论，默认页面也会带有评论。需要关闭的话，请添加字段 comments 并将值设置为 false，如：

```
title: 所有标签
date: 2017-02-04 11:07:24
type: "tags"
comments: false
---
```
3. 在菜单中添加链接。编辑主题的`themes/next/_config.yml` ，添加 tags 到 menu 中，如下:

```
menu:
  home: /
  archives: /archives
  tags: /tags
```
然后主站就多了一个标签的页面可以预览下了 http://aleonchen.com/tags/

4.每篇文章在撰写的时候添加标签，如果是多标签是需要符合yml语法的，形如: tags: [tag1,tag2,tag3]
比如我的[这篇文章](http://aleonchen.com/2017/02/03/MTA/)就是这么写的

```
---
title: Hexo添加腾讯移动分析(MTA)支持
date: 2017-02-03 20:26:37
tags: [hexo, mta]
---
```

## 搜索 Search
道理上还是Google做排名更加靠谱一些，百度做排名那是简直了。

### 首页title优化

更改index.swig文件(your-hexo-site\themes\next\layout);

将下面这段代码

```
{% block title %} {{ config.title }} {% endblock %}
```
改成

```
{% block title %} {{ theme.keywords }} - {{ config.title }}{{ theme.description }} {% endblock %}
```
打开网站源码看看'description'里面都是自动摘抄的网站内容

>注意：别堆砌关键字，整个标题一般不超过80个字符，可以通过chinaz的seo综合查询检查。

### 添加sitemap站点地图
1. 安装sitemap站点地图自动生成插件

```
npm install hexo-generator-sitemap --save
npm install hexo-generator-baidu-sitemap --save
```
在主题配置文件中添加一下配置 ，这里有的文章说的是在站点配置文章中添加，这个应该问题不大。

```
sitemap:
  path: sitemap.xml
  
baidusitemap:
  path: baidusitemap.xml
```

>注意：上面的格式一定要正确，一定要有缩进，不然会出错，我想信很多小伙伴因为没有缩进而不能编译的。

然后在主题配置文件中修改url为你的域名，例如我的

```
url: http://aleonchen.com
```
NexT主题默认的是http://yoursite.com
配置好后，hexo g 就能在your-hexo-site\public 中生成sitemap.xml 和 baidusitemap.xml了;
其中第一个是一会要提交给google的，后面那个看名字当然就是提交给Baidu的了；

在your-hexo-site\source中新建文件robots.txt,内容可以参照我的

```
User-agent: *
Allow: /
Allow: /archives/
Allow: /categories/
Allow: /tags/

Disallow: /vendors/
Disallow: /js/
Disallow: /css/
Disallow: /fonts/
Disallow: /vendors/
Disallow: /fancybox/
```
其中Allow后面的就是你的menu；

在robots.txt中添加下面的代码

```
Sitemap: http://aleonchen.com/sitemap.xml
Sitemap: http://aleonchen.com/baidusitemap.xml
```
请自行将`aleonchen.com`改成自己的域名,然后`hexo d -g`提交一下

### 配置Google站点管理工具（Google Webmaster tools）
设置 Google站点管理工具 的验证字符串，用于提交 sitemap
1. 获取 google site verification code
![google_site_verification](/media/google_site_verification.jpg)

登录 Google Webmaster Tools，导航到验证方法，并选择 HTML Tag。将会获取到一段代码：
<meta name="google-site-verification" content="XXXXXXXXXXXXXXXXXXXXXXX" />
将 content 里面的 XXXXXXXXXXXXXXXXXXXXXXX 复制出来。

2.编辑站点配置`themes/next/_config.yml`，修改字段 google_site_verification。
google_site_verification: XXXXXXXXXXXXXXXXXXXXXXX

3.让Google手动抓取，重建索引
- 测试robots.txt
- 提交站点地图
- 让Google抓取

>关键是配置Google抓取工具，在这里我们填上我们需要抓取的url,不填这表示抓取首页，抓取方式可以选择桌面，智能手机等等，自行根据需要选择。填好url之后，点击抓取。提交完成后，提交至索引，根据提示操作就可以了，见图
![google_search_console](/media/google_search_console.jpg)
这个时候再去Google搜索，不上首页都难吧
![google_result](/media/google_result.png)

# 参考
参考了这篇文章，感谢作者
[Hexo Seo优化让你的博客在google搜索排名第一](http://hunao.info/2016/06/01/Hexo-Seo%E4%BC%98%E5%8C%96%E8%AE%A9%E4%BD%A0%E7%9A%84%E5%8D%9A%E5%AE%A2%E5%9C%A8google%E6%90%9C%E7%B4%A2%E6%8E%92%E5%90%8D%E7%AC%AC%E4%B8%80/)







