---
title: GPG
layout: default
---

# GPG: GNU Privacy Guard
暗号ソフトウェア

## 主鍵生成
~~~
# gpg --full-gen-key
~~~

## 副鍵生成[S]
~~~
# gpg --edit-key 594F21DF
~~~

~~~
[root@redhat94 ~]# gpg --list-keys --keyid-format long
[root@redhat94 ~]# gpg --list-keys --keyid-format short
~~~
~~~
  /root/.gnupg/pubring.kbx
  ------------------------
  pub   rsa3072/36FE119D 2025-04-08 [SC]
        CE86497A732C7252692F2850DBA5092E36FE119D
  uid         [  究極  ] majsdf <majsdf@localdomain.ma.jp>
  sub   rsa3072/D23FDEC2 2025-04-08 [E]
  sub   rsa3072/A582E0F0 2025-04-08 [S]
~~~

## 公開鍵出力
~~~
# gpg --armor --export 594F21DF
~~~

## gitに設定
~~~
# git config --global commit.gpgsign true
# git config --global user.signingkey 7862A5F7
# export GPG_TTY=$(tty)
~~~
