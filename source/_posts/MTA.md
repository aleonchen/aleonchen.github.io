---
title: Hexo添加腾讯移动分析(MTA)支持
date: 2017-02-03 20:26:37
tags: [hexo, mta]
---
# 摘要
本文介绍了为Hexo中NexT主题模板添加“腾讯移动分析(MTA)”的详细过程，并开源在GitHub上，可以了解为hexo添加第三方hexo的过程

# 正文
## 缘起
搭建好了Hexo的博客之后，今天有空稍微整理下，目前选了[NexT的模板](http://notes.iissnan.com/)也是目前使用的主题，这个主题非常优雅，感谢作者iissnan。按照作者的[配置指南](http://theme-next.iissnan.com/)，完善了下博客的配置，打开了多说评论、安装了阅读技术等等。

## 腾讯统计
在弄数据统计的时候，发现除了Google、Baidu的统计，腾讯的统计模块还是非常旧的ta.qq.com的统计支持。这个应用腾讯官方已经基本不维护了，目前官方推荐的是使用[腾讯移动分析](mta.qq.com)，不仅可以支持应用统计、HTML5网页统计甚至还有小程序的统计。支持用户画像、区域和行为分析等。之前项目使用MTA比较熟悉，所以也想自己的Blog可以支持。
![mta_su](/media/mta_sum-1.png)
![mta_devices](/media/mta_devices-1.png)


## 修改代码
稍微研究了下NexT的代码，其实只要修改三个地方就可以了。

1.在NexT的`_config.yml`下面添加一个MTA的设置，MTA只要去创建一个HTML5的应用即可，填入你所申请的`App Id`

```
# Tencent MTA ID
tencent_mta: your app id
```

2.修改`analytics.swig`文件，添加一个新的js模板，路径为：

```
layout/_scripts/third-party/analytics.swig
```
添加一行代码

```
{% include 'analytics/tencent-mta.swig' %}
```

3.在`layout/_scripts/third-party/analytics`目录下面添加一个新文件`tencent-analytics.swig`，内容为：

```
{% if theme.tencent_mta %}
<script>
  	var _mtac = {};
  	(function() {
  		var mta = document.createElement("script");
  		mta.src = "http://pingjs.qq.com/h5/stats.js?v2.0.2";
  		mta.setAttribute("name", "MTAH5");
  		mta.setAttribute("sid", "{{theme.tencent_mta}}");

  		var s = document.getElementsByTagName("script")[0];
  		s.parentNode.insertBefore(mta, s);
  	})();
</script>
{% endif %}
```

最后，在本地`hexo server`跑起来看了下 mta的代码有没有添加到页面，如果有了，就OK了。

## 代码 & PR
如果有问题，可以去看代码 https://github.com/aleonchen/hexo-theme-next

也给作者提交了一个pull request，希望能够添加到官方 😊

