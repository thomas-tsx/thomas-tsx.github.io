---
title: CentOs 7安装Jekyll 
date: 2017-10-12
categories:
- Linux
tags:
- Jekyll
---

注意：本文原创，转载请注明出处。

本博客即采用Jekyll+github搭建，在安装Jekyll过程中遇到一些问题，所以写篇文章记录一下

<!-- more -->

## 安装rvm（ruby version manager）
Jekyll依赖Ruby，直接下载Ruby tar包编译安装太麻烦，所以先安装rvm
```she&#39;ll
    gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
    curl -sSL https://get.rvm.io | bash -s stable
    source /etc/profile.d/rvm.sh
```

## 安装 ruby 2.2.1
执行以下命令安装
```she&#39;ll
    sudo yum install libyaml  
    rvm install 2.2.1  /** 安装ruby 2.2.1 此过程需要一点时间 **/
    rvm use 2.2.1 --default /** 设为默认版本 **/
```

## 安装Nodejs
Jekyll 还依赖 JavaScript 运行库，需要安装Nodejs
下载 epel-release-6-8.noarch.rpm，执行以下命令安装
```she&#39;ll
    rpm -ivh epel-release-6-8.noarch.rpm
    sudo yum update /** 中间有些许 Error，不理会 **/
    sudo yum install nodejs
```

## 安装Jekyll
安装 Jekyll，为了加快下载速度，首先修改 gem 源
```she&#39;ll
    gem sources --remove https://rubygems.org/
    gem sources -a http://mirrors.ustc.edu.cn/rubygems/
    gem install jekyll
```

## 测试Jekyll
```she&#39;ll
    mkdir jekyll
    cd jekyll
    jekyll new blog
    cd blog
    jekyll serve --host 0.0.0.0
```
打开浏览器，访问 http://*.*.*.*:4000/ 即可看到 Jekyll 默认页面
![plot of chunk jekyll](/images/jekyll.png)


## 进阶使用
```she&#39;ll
    jekyll serve --host 0.0.0.0 --detach /** 使用后台模式运行 Jekyll **/
```
更多请参考 [Jekyll官方文档](http://jekyll.com.cn/docs/usage/ "Jekyll官方文档")


## QA（问题）

![plot of chunk bundler](/images/bundler.png)

```she&#39;ll
    gem install bundler
```
千万不要使用 sudo gem install bundler 安装，否则会报以上错误

安装bundler之后使用 bundle -v 查看版本发现报如下错误
![plot of chunk bundler_error](/images/bundler_error.png)
执行以下命令耐心等待即可
```she&#39;ll
    bundle install
```

在启动 jekyll server 的时候可能会看到以下类似的错误，基本上缺少什么就安装什么，有时候一次安装不成功就多试几次
![plot of chunk jekyll-paginate](/images/jekyll-paginate.png)
```she&#39;ll
    gem install jekyll-paginate
```