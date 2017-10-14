---
title: 使用Jekyll+Github搭建博客
date: 2017-10-14 22:09:45
categories:
- Linux
tags:
- Jekyll
- Github
---

注意：本文原创，转载请注明出处。

下面主要介绍怎么使用Jekyll+Github搭建类似于我这样的博客
在这里很感谢[王诗翔](https://github.com/ShixiangWang "王诗翔的Github"){:target="_blank"}的帮助
<!-- more -->
## 1、注册Github账号
1、打开[https://github.com](https://github.com "Github"){:target="_blank"}  
2、注册Github账号，注意注册的用户名（假如是username），如果你没有额外购买其他域名，那么博客搭建好之后的域名就是https://username.github.io  
3、建立一个仓库，仓库名称username.github.io(把username替换成你自己的)，这里有两种做法  
第一：以github用户名命名仓库，以后代码提交到master分支上  
第二：仓库命名随意，但是代码必须提交到gh-pages分支上

## 2、安装Jekyll
1、关于怎么安装Jekyll前面已经有文章介绍了----------[CentOs 7安装Jekyll](https://thomas-tsx.github.io/linux/2017/10/12/install-jekyll/ "CentOs 7安装Jekyll"){:target="_blank"}
2、到 [Jekyll Theme](http://jekyllthemes.org/ "Jekyll Theme"){:target="_blank"}下载一个自己喜欢的主题，本人最喜欢 [Next](http://jekyllthemes.org/themes/jekyll-theme-next/ "Next Theme"){:target="_blank"}这个主题，简约风格  
(最简单粗暴的方式是直接fork别人的博客，然后自己修修改改就变成自己的了[坏笑]，因为原生的主题里面貌似没有评论系统之类的插件扩展)

## 3、使用Giuthub.io博客
1、将之前下载好的Jekyll Theme解压缩应该可以看到以下目录结构
![plot of chunk jekyll_theme_next_struct](/images/jekyll_theme_next_struct.png)  
2、按照第一种方式建立仓库，将代码提交到master分支上
```R
  git init
  git add .
  git commit -m "first commit"
  git remote add origin https://github.com/username/jekyll_demo.git
  git push -u origin master /** 将本地仓库push远程仓库，并将origin设为默认远程仓库 **/
```
3、打开Github网站，进入之前的仓库，点击 branch 查看是否编译通过
![plot of chunk github_site1](/images/github_site1.png)
![plot of chunk github_site2](/images/github_site2.png)
如果编译有问题，基本上都是仓库根目录下的_config.yml文件的问题，根据错误仔细排查  
如果编译没问题，过一会儿打开网站https://username.github.io即可看到如下页面
![plot of chunk jekyll_theme_next](/images/jekyll_theme_next.png)   
4 、发布新博客  
在根目录下有一个_posts目录，这就是存放博客文章的目录，一般都是写的markdown文件，后缀名为.md，copy一个，随便修改一下里面的内容再重新推送到github，如果编译没问题，再刷新博客页面，就可以看到你刚刚发布的博客了  
注意：md文件的最前面的几行是声明格式，可以修改内容，但是基本格式不要修改
