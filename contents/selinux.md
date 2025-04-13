---
title: selinux
layout: default
---
# SELinux: Security-Enhanced-Linux

|表示|ステータス|モード|内容|
|:--|--:|:--:|:--:|
|Enforcing|  有効  |Enforcinモード|SELinux有効（制御有 + ログ出力有）|
|Permissive|  有効  |Permissiveモード|SELinux有効（制御無 + ログ出力有）|
|Disabled|  無効  |  -  |SELinux無効（制御無 + ログ出力無）|

## SELinux status tool
~~~
  # sestatus
  # setenforce  enforce | permissive | 1 | 0 
~~~
## Kernel パラメータ
~~~
  # cat /proc/cmdline
~~~

# grubby: command line tool for configuring grub and zipl
## 情報
~~~
  # grubby --info=1
  # grubby --info=ALL
~~~

## SELinux無効化
~~~
  # grubby --update-kernel=ALL --args="selinux=0"
~~~
~~~
  # vi /etc/selinux/config [#p7b72765]
  
  SELINUX=enforcing
~~~
編集後は、必ず sestatus を実行して変更をチェックする

## chcon - change file SELinux security context
~~~
  $ chcon --help
  $ chcon -R -t httpd_sys_content_t ./public_html/
  $ ls -lZ
~~~


