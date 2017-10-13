---
title: 关于Sublime Text
date: 2017-10-13 22:02:23
categories:
- Windows
tags:
- Sublime Text 3
---

注意：本文摘录，原文地址 <http://blog.csdn.net/lxyhenpiaoliang/article/details/51939033>

## 1、安装包管理器
使用Ctrl+~快捷键或者通过View->Show Console菜单打开命令行，粘贴如下代码  
测试超链接[example](http://yinping4256.github.io){:target="_blank"}
<!-- more -->
> import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ',' ')).read())

顺利的话，此时就可以在Preferences菜单下看到Package Settings和Package Control两个菜单了

## 2、安装乱码处理插件
打开ctrl+shift+p,输入：install package，回车，在稍后弹出的安装包框中搜索：ConvertToUTF8或者GBK Encoding Support，选择点击安装即可
