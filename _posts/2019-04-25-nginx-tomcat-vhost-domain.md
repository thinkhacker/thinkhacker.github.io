---
layout: post
title: "结合nginx+tomcat虚拟主机配置实现子域名访问不同的应用"
category: 
- Java
- Tomcat
- Ubuntu
- Nginx
tags: ["Ubuntu","Tomcat","Java","Nginx","虚拟主机配置"]
---
* content
{:toc}

通过子域名来访问服务器上的多个Tomcat应用，是很多项目会碰到的场景。
本文主要是介绍通过域名，nginx，tomcat等配置实现多个域名访问不同
的tomcat应用。


<!-- more -->
<!-- TOC -->

# 需求说明

目前需要配置2个子域名来访问java的应用。

- 一个是管理后台  admin.xxx.com

- 一个是web前端  www.xxx.com



# 域名配置

域名上，通过添加域名等泛指A记录到服务器等IP。
```
admin.xxx.com  ==A记录=>  服务器IP 

www.xxx.com  ==A记录=>  服务器IP 

@xxx.com     ==A记录=>  服务器IP 

```
# Nginx配置
每一个子域名配置一个Nginx的vhost配置。

## 新建配置文件
```sh
vi /etc/nginx/conf.d/www.xxx.com.conf

```
## 配置内容
```config

upstream web-domain{
    server localhost:8081;
}

 
server {
    listen       80;
    server_name  www.xxx.com xxx.com;
    access_log  logs/www.xxx.com.access.log  main;
 	error_log   logs/www.xxx.com.error.log  main;

    location / {
        proxy_pass http://web-domain;
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;           
    }

    #error_page  404              /404.html;
    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   html;
    }
}
```
管理后台
```sh
vi /etc/nginx/conf.d/admin.xxx.com.conf
```
配置内容
```
 
upstream admin-domain{
    server localhost:8083;
}
 
server {
    listen       80;
    server_name  admin.xxx.com;
    access_log  logs/admin.xxx.com.access.log  main;
    error_log  logs/admin.xxx.com.error.log  main;
    
 
    location / {
        proxy_pass  http://admin-domain;
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;           
    }
 
    #error_page  404              /404.html;
 
    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   html;
    }
 
}
```
# Tomcat配置

目前的应用存放位置如下：

网站前端
```
/data/wwwapps/www.xxx.com
```
管理后台
```
/data/wwwapps/admin.xxx.com
```
## 修改配置文件
```sh
vi /etc/tomcat/conf/server.xml
```
## 配置文件内容
```xml

<?xml version='1.0' encoding='utf-8'?>

<Server port="8046" shutdown="SHUTDOWN">
  <Listener className="org.apache.catalina.startup.VersionLoggerListener" />

  <Listener className="org.apache.catalina.core.AprLifecycleListener" SSLEngine="on" />

  <Listener className="org.apache.catalina.core.JasperListener" />

  <Listener className="org.apache.catalina.core.JreMemoryLeakPreventionListener" />
  <Listener className="org.apache.catalina.mbeans.GlobalResourcesLifecycleListener" />
  <Listener className="org.apache.catalina.core.ThreadLocalLeakPreventionListener" />


  <GlobalNamingResources>

    <Resource name="UserDatabase" auth="Container"
              type="org.apache.catalina.UserDatabase"
              description="User database that can be updated and saved"
              factory="org.apache.catalina.users.MemoryUserDatabaseFactory"
              pathname="conf/tomcat-users.xml" />
  </GlobalNamingResources>

  <!--web app-->
  <Service name="Catalina">

    <Connector port="8081" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" URIEncoding="UTF-8"/>

    <Connector port="8010" protocol="AJP/1.3" redirectPort="8443" />


    <Engine name="Catalina" defaultHost="www.xxx.com">


      <Realm className="org.apache.catalina.realm.LockOutRealm">

        <Realm className="org.apache.catalina.realm.UserDatabaseRealm"
               resourceName="UserDatabase"/>
      </Realm>

      <Host name="www.xxx.com"  appBase="/data/wwwapps/www.xxx.com"
            unpackWARs="true" autoDeploy="true">


        <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
               prefix="localhost_access_log." suffix=".txt"
               pattern="%h %l %u %t &quot;%r&quot; %s %b" />

      </Host>
    </Engine>
  </Service>
   <!--admin appp Service -->
  <Service name="Catalina">

    <Connector port="8082" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" URIEncoding="UTF-8"/>

    <Connector port="8011" protocol="AJP/1.3" redirectPort="8443" />


    <Engine name="Catalina" defaultHost="admin.xxx.com">


      <Realm className="org.apache.catalina.realm.LockOutRealm">

        <Realm className="org.apache.catalina.realm.UserDatabaseRealm"
               resourceName="UserDatabase"/>
      </Realm>

      <Host name="admin.xxx.com"  appBase="/data/wwwapps/admin.xxx.com"
            unpackWARs="true" autoDeploy="true">

        <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
               prefix="localhost_access_log." suffix=".txt"
               pattern="%h %l %u %t &quot;%r&quot; %s %b" />


      </Host>
    </Engine>
  </Service>
</Server>
```