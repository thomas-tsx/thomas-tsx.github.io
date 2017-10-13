---
title: CentOs安装Gitlab
date: 2017-10-12 17:12:51
categories:
- Linux
tags:
- Git
---

注意：本文原创。

**前言**
- 众所周知，Git是目前世界上最先进的分布式版本控制系统
- 而GitLab是利用 Ruby on Rails 一个开源的版本管理系统，实现一个自托管的Git项目仓库
- 可通过Web界面进行访问公开的或者私人项目。它拥有与Github类似的功能，能够浏览源代码，管理缺陷和注释
- 可以管理团队对仓库的访问，它非常易于浏览提交过的版本并提供一个文件历史库。
- 以下简单介绍CentOS 6 以及 CentOS 7 下安装 gitlab
- 安装方法大致参照官网，CentOS 6 与 CentOS 7 前置准备工作有些许不同

<!-- more -->

## CentOS 6 安装 Gitlab

①：依次使用以下命令在系统防火墙里开启HTTP和SSH端口
```she&#39;ll
    sudo yum install -y curl openssh-server openssh-clients cronie
    sudo lokkit -s http -s ssh
```

②：接下来安装Postfix发送电子邮件通知，如果要使用其他解决方案发送电子邮件，请跳过此步骤，并在安装Gitlab之后配置外部SMTP服务器（后面介绍配置其他邮件服务器）
```she&#39;ll
    sudo yum install postfix
    sudo service postfix start
```
启动postfix时可能报错：
```she&#39;ll
    Job for postfix.service failed because the control process exited with error code. See "systemctl status postfix.service" and "journalctl -xe" for details.
```
解决办法，修改 /etc/postfix/main.cf的设置
```she&#39;ll
    inet_protocols = ipv4  
    inet_interfaces = all
```
![plot of chunk main_postfix](/images/main_postfix.png)
```she&#39;ll
    sudo chkconfig postfix on
```


## CentOS 7 安装 Gitlab

①：依次使用以下命令在系统防火墙里开启HTTP和SSH端口
```she&#39;ll
    sudo yum install -y curl policycoreutils openssh-server openssh-clients
    sudo systemctl enable sshd
    sudo systemctl start sshd
    sudo firewall-cmd --permanent --add-service=http
```
执行以上firewall命令时可能会报错
```she&#39;ll
    FirewallD is not running
    通过systemctl status firewalld查看firewalld状态，发现当前是dead状态，即防火墙未开启
    通过systemctl start firewalld开启防火墙，没有任何提示即开启成功，再次通过systemctl status firewalld查看firewalld状态，显示running即已开启了
    如果要关闭防火墙设置，可能通过systemctl stop firewalld这条指令来关闭该功能
    sudo systemctl reload firewalld
```

②：接下来安装Postfix发送电子邮件通知，如果要使用其他解决方案发送电子邮件，请跳过此步骤，并在安装Gitlab之后配置外部SMTP服务器（后面介绍配置其他邮件服务器）
```she&#39;ll
    sudo yum install postfix
    sudo systemctl enable postfix
    sudo systemctl start postfix
```
启动postfix时可能报错，解决办法与上面一致


## 准备安装gitlab
通过 rpm 包的方式安装gitlab，我安装的是9.0.5-ce版本
拷贝gitlab-ce-9.0.5-ce.0.el6.x86_64.rpm到服务器某目录
执行安装命令等待即可
```she&#39;ll
    rpm -i gitlab-ce-9.0.5-ce.0.el6.x86_64.rpm
```

安装完成，修改端口（gitlab默认端口8080，可能与tomcat冲突）
```she&#39;ll
    vi /etc/gitlab/gitlab.rb
    修改 external_url 'http://*.*.*.*:8099' （修改成自己的IP地址）
    修改 nginx['listen_port'] = 8099
```
保存退出

修改防火墙设置，开放8099端口
```she&#39;ll
    vi /etc/sysconfig/iptables
    添加  -A INPUT -m state --state NEW -m tcp -p tcp --dport 8099 -j ACCEPT（注意此行添加在80端口后面）
```
![plot of chunk iptables](/images/iptables.png)

重启防火墙
```she&#39;ll
    service iptables restart
```

重新加载 gitlab 配置文件
```she&#39;ll
    sudo gitlab-ctl reconfigure
```
执行以上命令有可能报错：
```she&#39;ll
    Error executing action `run` on resource 'ruby_block[directory resource: /var/opt/gitlab/git-data/repositories]'
```
解决办法：
```she&#39;ll
    sudo chmod 2770 /var/opt/gitlab/git-data/repositories
    sudo gitlab-ctl restart 重启 gitlab
    sudo gitlab-ctl status 查看 gitlab 状态
```

配置外部邮件服务器
```she&#39;ll
    gitlab_rails['smtp_enable'] = true
    gitlab_rails['smtp_address'] = "smtp.ym.163.com"
    gitlab_rails['smtp_port'] = 25
    gitlab_rails['smtp_user_name'] = "tsx@zhiduntech.com"
    gitlab_rails['smtp_password'] = "tsxP@ssw0rd"
    gitlab_rails['smtp_domain'] = "163.com"
    gitlab_rails['smtp_authentication'] = "login"
    gitlab_rails['smtp_enable_starttls_auto'] = true
    gitlab_rails['smtp_tls'] = false

    gitlab_rails['gitlab_email_from'] = 'tsx@zhiduntech.com'

    user['git_user_name'] = "GitLab"
    user['git_user_email'] = "tsx@zhiduntech.com"
```
![plot of chunk iptables](/images/email_config1.png)
![plot of chunk iptables](/images/email_config2.png)
![plot of chunk iptables](/images/email_config3.png)
![plot of chunk iptables](/images/gitlab_page.png)
