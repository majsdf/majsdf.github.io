---
title: groupsession
layout: default
---

# Groupsession

## Temurin 11.0.13
~~~
# cd /usr/local/java
# tar xvpf OpenJDK11U-jdk_x64_alpine-linux_hotspot_11.0.26_4.tar.gz
# vi ~/.bash_profile
~~~
~~~
# User specific environment and startup programs
JAVA_HOME=/usr/local/java/jdk-11.0.26+4
PATH=$JAVA_HOME/bin:$PATH
export PATH
~~~
## tomcat
~~~
# yum install tomcat
~~~
## groupsession
  * /var/lib/tomcat/webapps に gsession.war を配置
~~~
# systemctl enable --now tomcat
~~~
~~~
cd /var/lib/tomcat/webapps/gsession
unzip dba5.5.0_0.zip
~~~

