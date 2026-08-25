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

## 接続
~~~
sqlplus / as sysdba

SQL> show con_name

CON_NAME
------------------------------
CDB$ROOT
SQL> show pdbs

    CON_ID CON_NAME                       OPEN MODE  RESTRICTED
---------- ------------------------------ ---------- ----------
         2 PDB$SEED                       READ ONLY  NO
         3 FREEPDB1                       READ WRITE NO
SQL> alter session set container=freepdb1

セッションが変更されました。

SQL> show con_name

CON_NAME
------------------------------
FREEPDB1
~~~
`sqlplus USER/PASSWORD@HOTSNAME:1521/FREEPDB1`

## ユーザ作成
~~~SQL
CREATE USER ユーザー名 IDENTIFIED BY パスワード
DEFAULT TABLESPACE USERS
TEMPORARY TABLESPACE TEMP;
ALTER USER ユーザー名 QUOTA UNLIMITED ON USERS;
GRANT CONNECT, RESOURCE TO ユーザー名;
~~~
