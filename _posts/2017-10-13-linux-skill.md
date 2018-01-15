---
title: Linux 相关技巧
date: 2017-10-19 16:55:23
categories:
- Linux
tags:
- Skill
---

注意：本文原创，转载请注明出处。

**目录**：

- Linux查找Java最耗新能线程
- 待续

<!-- more -->

## 1、Linux查找Java最耗新能线程
1、首先在终端执行top命令，然后按下`Shift+P`查找出最耗CPU的pid号，如下
![plot of chunk linux_pid1](/images/linux_pid1.png)
可以看到最耗CPU的pid号是8606  

2、使用前面找出来的pid，使用`top -H -p pid`命令，按下`Shift+P`，找出最耗CPU的pid号
```R
top -H -p pid
```

3、使用jstack打印出进程信息
```R
jstack 9058 > /tmp/log.dat
```
![plot of chunk linux_pid2](/images/linux_pid2.png)

4、将pid号转成16进制，比如9058转成16进制是2362，使用文本编辑器打开log.dat，查找2362可以发现相关信息
![plot of chunk linux_pid3](/images/linux_pid3.png)  

5、mysql只能通过localhost连接，而不能通过IP连接，只需打开mysql终端，使用root登陆之后执行以下命令即可：
```R
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'password' WITH GRANT OPTION;
```
