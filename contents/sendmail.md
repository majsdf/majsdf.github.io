---
title: sendmail
layout: default
---
# Sendmail: SMTPサーバ

## solaris11

## 設定ファイル
~~~
 root@solaris11:/etc/mail# cat local-host-names
 
 solaris11.localdomain.ma.jp
~~~
~~~
 root@solaris11:/etc/mail# cat relay-domains
 
 172.
~~~
~~~
 root@solaris11:/etc/mail# cat mailertable

 localdomain.ma.jp    mailer:[172.16.0.100]
~~~


