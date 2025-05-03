---
title: PostgreSQL
layout: default
---

# PostgreSQL: DBMS

## redmineのケース
~~~
# su - postgres
$ initdb -E UTF-8 --locale=C -A scram-sha-256 -W
~~~
~~~
$ su
# systemctl enable --now postgresql
# exit
~~~
~~~
$ createuser -P redmine
$ createdb -E UTF-8 -l ja_JP.UTF-8 -O redmine -T template0 redmine
~~~

## 接続
/var/lib/pgsql/data/
- postgresql.conf
~~~
listen_addresses =    '*'
~~~
- pg_hba.conf
~~~
host    all             all             172.16.0.0/24         scram-sha-256
~~~



