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
|Ctrl + X/Y|删除行|
|Ctrl + N|查找类|
|Ctrl + F|查找文本|
|Ctrl + E|最近打开的文件|
|Ctrl + G|跳到指定行|
|Ctrl + L|find next（选中文本时先按Ctrl + F3 find word caret）|
|Ctrl + Home|跳到文件开头|
|Ctrl + End|跳到文件结尾|
|Ctrl + [|跳到 { 开始处|
|Ctrl + ]|跳到 } 结尾处|
|Ctrl + F12|展示当前文件结构|
|Ctrl + H|展示当前类的继承关系|
|Ctrl + Shift + N|查找文件|
|Ctrl + Shift + J|整合多行代码为一行|
|Ctrl + Shift + U|大小写转换|
|Ctrl + Alt + H|open call hierarchy|
|Ctrl + Alt + L|格式化代码|
|Ctrl + Alt + O|优化导入的类和包|
|Ctrl + Alt + T|Surround with......|
|Alt + Enter|自动导包|
|Alt + Insert|生成构造方法或者 setter，getter方法|
|Alt + 1|快速打开/隐藏 左边工程面板|
|Alt + 4|打开tomcat控制台|
|Alt + F1|查找代码所在位置（Open Explorer）|
|sout + Tab 键|快速创建输出语句（System.out.println()）|
|psvm + Tab 键|快速创建主函数（public static void main）|
|fori + Tab 键|快速创建 for 循环|
|Ctrl + / 或 Ctrl + Shift + /|单行注释或多行注释|
|Double Shift（按两下Shift）|打开 search everywhere 框|
|Ctrl + Alt + Shift + S|打开当前项目/模块属性（Project Structure）|
|Ctrl + W|关闭当前文件 Close（自定义）|
|Ctrl + Shift + W|关闭所有活动窗口 Close All（自定义）|
|Ctrl + B|跟进接口实现方法 Implementations（自定义）|
|Ctrl + Alt + B|跟进接口文件 Declaration（自定义）|

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

3、IDEA 对于引用 dubbo 接口会一直有警告提示，Could not autowired，No bean of "ISystemType" type found，原因是 IDEA 只认在配置文件配置的<bean>，而 dubbo 的 reference 是不认的，可以做如下改动去掉警告即可
![plot of chunk idea_config4](/images/idea_config4.png)

4、Information:java: javacTask: 源发行版 1.7 需要目标发行版 1.7
   选择项目，maven，Reimport重新编译即可
![plot of chunk idea_config5](/images/idea_config5.png)

5、Information:java: javacTask: 源发行版 1.7 需要目标发行版 1.7
   选择项目，maven，Reimport重新编译即可
![plot of chunk idea_config5](/images/idea_config5.png)
