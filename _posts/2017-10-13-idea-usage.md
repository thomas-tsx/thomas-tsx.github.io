---
title: JetBrains IDEA 使用过程问题记录
date: 2017-10-13
categories:
- JetBrains
tags:
- IDEA
---

注意：本文原创，转载请注明出处。

本文主要记录IDEA在使用过程当中的一些问题，以及一些常用快捷键

<!-- more -->

## 1、一些常用快捷键
|快捷键|说明|
|----|-----|
|Ctrl + D|复制行|


## 2、IDEA 代码合并冲突解决
假设：项目Rcp-test中的 Test.java 类，各有v1.0.1，v1.0.2分支，两人在修改了同一行代码，比如，v1.0.1第10行新增System.out.println("v1.0.1 conflict test");
v1.0.2第10行新增System.out.println("v1.0.2 conflict test");
此时v1.0.2开发者先将此行合并到了master分支，之后v1.0.1开发者再合并到master时就会冲突，会有如下提示
![plot of chunk idea_merge1](/images/idea_merge1.png)

点击 Merge 弹出如下窗口
会看到有三个板块，左侧第一个版本为本地代码（master最新代码），最右侧为将要合并的分支代码（v1.0.1），中间则为合并之后的结果Result，此时自己手动将最左以及最右两个窗口代码合并复制到中间窗口，点击 Apply 即可解决冲突
![plot of chunk idea_merge2](/images/idea_merge2.png)

## 3、QA（问题）
1、IDEA导入Spring项目报如下错误
![plot of chunk idea_error1](/images/idea_error1.png)
打开 Project Structure，点击右边 + 号，弹出界面勾选 Spring 配置即可
![plot of chunk idea_config1](/images/idea_config1.png)
![plot of chunk idea_config2](/images/idea_config2.png)

2、IDEA 导入本地 maven 项目，需要区别于 Eclipse 的是，Eclipse 中的 workspace 在 IDEA 里相当于 Project，而在 Eclipse 中的一个个项目，在 IDEA 里面相当于 Module.
![plot of chunk idea_config3](/images/idea_config3.png)

3、IDEA 对于引用 dubbo 接口会一直有警告提示
```she&#39;ll
    Could not autowired，No bean of "ISystemType" type found
```
原因是 IDEA 只认在配置文件配置的`<bean>`，而 dubbo 的 reference 是不认的，可以做如下改动去掉警告即可
![plot of chunk idea_config4](/images/idea_config4.png)

4、Information:java: javacTask: 源发行版 1.7 需要目标发行版 1.7，选择项目，maven，Reimport重新编译即可
![plot of chunk idea_config5](/images/idea_config5.png)
