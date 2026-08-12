---
title: h2database
layout: default
---
# h2database: h2

## ロック中の H2 Database に接続する方法

H2 Database は通常、同時アクセスによる衝突を避けるために単一ユーザーでの書き込みロックをかけます。しかし、既にロックされた状態でも **ファイルロックなし** でデータベースに接続することが可能です。以下に手順を解説します。

## 接続方法

### JDBC URL の指定

ファイルロックなしで接続するには `FIEL_LOCK=NO` `ACCESS_MODE_DATA=rws` パラメータを使用します。
```java
String url = "jdbc:h2:/path/to/db;FILE_LOCK=NO;ACCESS_MODE_DATA=rws";
Connection conn = DriverManager.getConnection(url, "ユーザー名", "パスワード");
```

/path/to/db は H2 データベースファイルのパスに置き換えてください。

この接続では既存ロックがある場合でも接続は可能ですが、データの **破損** につながる可能性があります。

### SQL ツールからの接続
H2 コンソールや GUI ツールからも同様に接続できます。接続 URL に ;FILE_LOCK=NO;ACCESS_MODE_DATA=rws を追加してください。

