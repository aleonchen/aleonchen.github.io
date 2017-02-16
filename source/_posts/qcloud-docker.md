---
title: 腾讯云安装docker服务及镜像加速配置 - Ubuntu
date: 2017-02-07 10:00:35
tags: [腾讯云, docker]
---

摘要: docker为应用部署、应用持续集成提供非常巨大的遍历性，提升了效率，同时为架构的横向扩张提供了非常好的基础。本文介绍了如何在腾讯云的服务器上自行搭建一个docker服务

<!-- more -->

## 系统选择
因为docker对于系统还是有要求的，推荐使用最新的系统，我用的是**Ubuntu 16.4 64bit**

## 一键安装docker
Congratulations! 腾讯云也出了官方的加速服务 [链接](https://www.qcloud.com/document/product/457/7207)。可惜一键安装脚本还没有，我们暂时用阿里的好了

```
curl -sSL http://acs-public-mirror.oss-cn-hangzhou.aliyuncs.com/docker-engine/internet | sh -
```

把默认用户加入docker组，免得每次都敲sudo（懒是优秀程序员必备的品质 :p)

```
sudo usermod -aG docker ubuntu
```

## 设置镜像加速
因为我安装的时候docker版本是1.13.0，腾讯官方给的方式还是比较旧的，建议采取修改json配置的方式更方便。可以通过修改daemon配置文件`/etc/docker/daemon.json`来使用加速器：

```
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://mirror.ccs.tencentyun.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

>其他方法：
>编辑 /etc/systemd/system/multi-user.target.wants/docker.service 文件，找到 ExecStart= 这一行，在这行最后添加加速器地址 --registry-mirror=<加速器地址>，如：`ExecStart=/usr/bin/dockerd --registry-mirror=<加速器地址>`

## 测试安装结果
修改好了之后确认一下，用`docker info`看看是不是和我一样设置正确了

```
Registry Mirrors:
 https://mirror.ccs.tencentyun.com
```

测试是好习惯

```
docker run --rm --name webserver -d -p 80:80 nginx
```
访问下`http://<you-server-ip>`，docker就起来啦
![nginx_welcome](/media/nginx_welcome.png)

碰到问题或者需要咨询欢迎在这里或者去公众号留言










