---
layout: post
title: "ubuntu上安装tomcat8"
category: 
- Java
- Tomcat
- Ubuntu 
tags: ["Ubuntu","Tomcat","Java"]
---
* content
{:toc}

Ubuntu 上通过APT INSTALL安装tomcat服务。

<!-- more -->
<!-- TOC -->
# 安装
```bash
sudo apt-get install tomcat8 tomcat8-admin
# service tomcat8 start
# service tomcat8 status
● tomcat8.service - LSB: Start Tomcat.
   Loaded: loaded (/etc/init.d/tomcat8; generated)
   Active: active (running) since Sat 2018-10-27 19:00:20 CST; 7min ago
     Docs: man:systemd-sysv-generator(8)
    Tasks: 35 (limit: 4915)
   CGroup: /system.slice/tomcat8.service
           └─5643 /usr/lib/jvm/default-java/bin/java -Djava.util.logging.config.

```

# 配置管理员
```bash
sudo vim /var/lib/tomcat8/conf/tomcat-users.xml
```
```xml
<role rolename="manager-gui"/>
<role rolename="admin-gui"/>
<user username="root" password="123456" roles="manager-gui,admin-gui"/>
```

# 重启

```bash
sudo service tomcat8 restart
```
# 配置服务自启动
```bash
sudo systemctl enable tomcat8
```
# 测试
```bash
http://127.0.0.1:8080/
```

# 卸载
```bash
sudo apt-get autoremove tomcat8
```

