---
title: Oracle
layout: default
---

# Oracle: Oracle AI Database 26ai Free Release 23.26.3.0.0 - Develop, Learn, and Run for Free
リレーショナルデータベース

## インストール
~~~
# yum install oracle-ai-database-preinstall-26ai-1.0-1.el10.x86_64.rpm
# yum install oracle-ai-database-free-26ai-23.26.3-1.el10.x86_64.rpm
~~~

## サービス構成スクリプト
~~~
# /etc/init.d/oracle-free-26ai configure
~~~

## 環境変数の設定
~~~
$ export ORACLE_SID=FREE 
$ export ORAENV_ASK=NO 
$ . /opt/oracle/product/26ai/dbhomeFree/bin/oraenv
$ export NLS_LANG=Japanese_Japan.UTF8
~~~
~~~
SQL> select * from dict
  2  where table_name='NLS_DATABASE_PARAMETERS';

TABLE_NAME
----------------------------------------------------------------------------------------------------
COMMENTS
----------------------------------------------------------------------------------------------------
NLS_DATABASE_PARAMETERS
Permanent NLS parameters of the database
~~~
