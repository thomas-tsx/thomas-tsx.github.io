---
title: CentOs 7安装 redis
date: 2017-10-13 15:35:45
categories:
- Linux
tags:
- Redis
---

注意：本文原创，转载请注明出处。

下面简单记录一下在CentOs 7上安装redis单机版，redis集群以后再介绍

## 1、安装过程
1、先安装tcl8.6.1  
> 拷贝tcl8.6.1-src.tar.gz到指定目录  
  解压缩tcl8.6.1-src.tar.gz  
  进入tcl8.6.1/unix目录  
  依次执行以下命令  
  <!-- more -->
  ```R
  ./configure
  make
  make install
  ```

2、安装redis
> 拷贝redis-4.0.0.tar.gz到指定目录  
  解压缩redis-4.0.0.tar.gz  
  进入redis-4.0.0/src目录执行以下命令  
  ```R
  make
  make install
  make test /** 一切正常则表示成功 **/
  ```
  在 usr/local目录下建立以下文件夹
  ```R
  mkdir -p redis/bin
  mkdir -p redis/conf
  ```  
  在之前 src 目录下执行以下命令（将那几个绿色的，可执行文件拷贝到 redis/bin目录下）  
  ```R
  mv mkreleasehdr.sh redis-benchmark redis-check-aof redis-check-rdb redis-cli redis-sentinel redis-server redis-trib.rb /usr/local/redis/bin/
  ```  
  拷贝 redis.conf 文件到redis/conf目录（原来的redis.conf位于src目录上一层）  
  修改redis.conf内容  
   ```R
   daemonize yes（以后台进程方式运行，默认no）
   bind 127.0.0.1注释（否则只能通过redis-cli -h localhost -p 6379 或者 redis-cli -h 127.0.0.1 -p 6379访问）
   protected-mode no（关闭保护模式，默认yes，如果开启保护模式则需要将# requirepass foobared 放开，并将foobared改为你的密码）
   ```

3、安装问题
>  阿里云安装redis之后默认只能通过redis-cli -h localhost -p 6379 或者 redis-cli -h 127.0.0.1 -p 6379来访问，此时修改redis.conf文件，将 bind 127.0.0.1注释掉，并且把 protect-mode 设为no（关闭保护模式，不需要密码），如果开启保护模式则需要将# requirepass foobared 放开，并将foobared改为你的密码
