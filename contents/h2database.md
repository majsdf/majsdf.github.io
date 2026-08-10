---
title: h2database
layout: default
---
# h2database: h2

## ロック中の H2 Database に読み取り専用で接続する方法

H2 Database は通常、同時アクセスによる衝突を避けるために単一ユーザーでの書き込みロックをかけます。しかし、既にロックされた状態でも **読み取り専用モード** でデータベースに接続することが可能です。以下に手順を解説します。

## 接続方法

### JDBC URL の指定

読み取り専用で接続するには `ACCESS_MODE_DATA=r` パラメータを使用します。例：

```java
String url = "jdbc:h2:/path/to/db;ACCESS_MODE_DATA=r";
Connection conn = DriverManager.getConnection(url, "ユーザー名", "パスワード");
```

/path/to/db は H2 データベースファイルのパスに置き換えてください。

ACCESS_MODE_DATA=r により読み取り専用モードで接続します。

この接続では既存ロックがある場合でも読み取りは可能ですが、書き込みはできません。

### SQL ツールからの接続
H2 コンソールや GUI ツールからも同様に接続できます。接続 URL に ;ACCESS_MODE_DATA=r を追加してください。
