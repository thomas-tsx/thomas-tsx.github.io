---
title: Atom 震撼烟花效果插件
date: 2017-11-02 15:35:45
categories:
- Linux
tags:
- Atom
---

注意：本文原创，转载请注明出处。

Atom作为一款非常好用的markdown语法编辑器，功能还是非常强大的，在网上某次发现在编辑时有特效，所以在此记录一下  
先看一下示例，以下图片摘自网上
![plot of chunk atom_plugin1](/images/atom_plugin1.jpg)
<!-- more -->

## 1、安装Atom
1、先到官网下载Atom安装，[Atom官网地址](https://atom.io/ "Atom官网"){:target="_blank"}  
2、安装成功后将Atom添加到系统环境变量 `C:\Users\tsx-t171\AppData\Local\atom\bin`

## 2、安装震撼烟花效果插件
1、该插件名称叫做activate-power-mode，github地址：<https://github.com/JoelBesada/activate-power-mode>  
2、下载zip包并解压拷贝到 `C:\Users\tsx-t171\.atom\packages`目录下，注意是 `.atom`  
3、进入activate-power-mode目录，也就是插件的目录，执行`apm install`，等待结果` installing modules done`即可，该过程可能需要开VPN  
4、重启Atom编辑器，使用`ctrl + alt + o`开控制开关的开启和关闭  
5、打开Atom的设置，File--->Settings，点击Packages，找到activate-power-mode，点击Settings，这里可以对该插件做一些个性化设置，比如现在新版的插件，默认使用了Combo Mode，可以在插件设置里面将Combo-Mode-Enable勾选去掉即可
![plot of chunk atom_plugin2](/images/atom_plugin2.png)

## 3、安装声音插件
1、插件github地址：<https://github.com/surdu/typewriter-sounds/releases>  
2、安装方法同上
