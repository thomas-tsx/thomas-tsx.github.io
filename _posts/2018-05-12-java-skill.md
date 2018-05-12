---
title: 开发日常小技巧
date: 2018-05-12  10:18:43
categories:
- Java
tags:
- Skill
---

注意：本文原创，转载请注明出处。

## 1、还原文件默认打开方式
通过修改注册表来还原文件默认打开方式为白板，这简直是强迫症的福音，比如想还原war包的默认打开方式  
修改 HKEY_CLASSES_ROOT\war_auto_file\shell\open\command，将默认值清空即可。

<!-- more -->

## 2、git还原到某次提交代码之前
假如某文件现在history有10次提交记录，假设最近的这次提交有问题，本不想提交到服务器，这时候可以通过以下命令来还原代码，注意次方式为不可逆操作  
想要将第10次提交还原，这时候可以拷贝一下第9次的commitId，也就是Revision Number，执行以下命令即可
```R
  git reset --hard commitId
  git push -f origin master
```

## 3、待更新.......