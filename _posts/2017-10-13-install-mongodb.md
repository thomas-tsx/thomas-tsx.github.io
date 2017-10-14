---
title: CentOs 7安装 mongodb
date: 2017-10-13  14:21:33
categories:
- Linux
tags:
- Mongodb
---

注意：本文原创，转载请注明出处。

下面简单记录一下在CentOs 7上安装mongodb单机版，mongodb集群以后再介绍

<!-- more -->

## 1、安装过程
1、拷贝mongodb-linux-x86_64-rhel70-3.4.9.tgz到指定目录  
2、解压缩mongodb-linux-x86_64-rhel70-3.4.9.tgz  
3、修改文件夹名字 cp -r mongodb-linux-x86_64 ./mongodb  
4、删除旧目录 rm -rf mongodb-linux-x86_64  
5、进入mongodb目录，新建好几个目录 mkdir -p data/db 用于存放mongodb数据（-p表示递归创建文件夹）
mkdir conf 用来存放 mongodb 配置文件，mkdir logs 用于存放mongodb日志  
6、在conf目录下新建一个文件 mongodb.conf，写入以下信息并保存
```R
    # 数据存放目录
    dbpath=/usr/local/mongodb/data/db/
    # 日志存放目录
    logpath=/usr/local/mongodb/logs/mongodb.log
    # 以追加的方式记录日志
    logappend=true
    # 以后台方式运行进程
    fork=true
    # 端口号
    port=27017
```
7、启动mongodb，./bin/mongod -f conf/mongodb.conf
