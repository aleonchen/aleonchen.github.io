---
title: PyCharm调试LeanCloud设置
date: 2017-01-28 21:53:51
tags: [pycharm, leancloud, debug]
---

摘要：本文为LeanCloud开发者提供了在Pycharm下调试Python程序的一个解决办法
![leancloud_pychar](/media/leancloud_pycharm.jpg)

<!-- more -->

# 正文
## 设置Pycharm
之前被Asaka安利了PyCharm很多回，但是中间我自己想要用它的一个非常重要的原因就是他方便调试。在使用LeanCloud开发的过程中，经常碰到一些问题，我不是很清楚，打日志比较麻烦，而且有的时候比如特别想知道程序流程的时候，其实调试是个非常好的手段。但是在Sublime里面调试一直是个硬伤。而一般的IDE会做的比较好，比如PyCharm。

PyCharm的Debug设置可以自动识别virtualenv，简直就是福音。但是在LeanCloud做调试的时候有个麻烦的事情，就是普通的调试我们使用命令

```
lean up
```
来启动本地调试，但是在PyCharm里面不是特别的方便，后来发现只要通过 `lean env`取到Leancloud的环境变量，再设置的到PyCharm Debug Configuration的 "Environment Variables"里面即可

![leancloud_pychar](/media/leancloud_pycharm.jpg)




现在可以快乐的调试啦

