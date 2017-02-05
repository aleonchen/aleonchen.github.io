---
title: 更改 macOS(osx) Docker image下载路径
date: 2017-02-05 18:14:51
tags: [docker, macOS]
---

摘要：Docker的镜像比较占用空间，在Linux系统下面是可以修改下载目录的。但是macOS一直没有给出修改办法，本文介绍了一种方法。

<!-- more -->

Docker是一个比较有趣的应用，可以用来代替虚拟机VM，诸多好处。
- 比虚拟机性能好
- 占用空间少
- 可以统一开发环境和生产环境，便于维护
![docker_v](/media/docker_vm.png)

但是默认的macOS的Docker安装目录是在系统盘下面的文件里面

```
~/Library/Containers/com.docker.docker/Data/com.docker.driver.amd64-linux/Docker.qcow2
```

MBP那点可怜的空间很快就塞满了，Linux可以设置其他的目录，macOS暂时没有看到官方有提供办法更改，但是macOS有个很好的功能就是做软连接，咱们可以将数据复制到其他目录`otherPath`，然后做link即可

```
mv ~/Library/Containers/com.docker.docker/Data/com.docker.driver.amd64-linux/ /otherPath/com.docker.driver.amd64-linux

ln -s /otherPath/com.docker.driver.amd64-linux /Users/<username>/Library/Containers/com.docker.docker/Data
```

哈哈，看看大功告成


