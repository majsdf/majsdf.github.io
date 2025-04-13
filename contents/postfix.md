---
title: postfix
layout: default
---

# postfix: SMTPサーバ
Postfix control program

## 設定ファイル
~~~
# diff --git a/main.cf b/main.cf
~~~
~~~
  index 5e70040..c4c4003 100644
  --- a/main.cf
  +++ b/main.cf
 @@ -99,7 +99,7 @@ mail_owner = postfix
  # $mydomain is used as a default value for many other configuration
  # parameters.
  #
 -#mydomain = domain.tld
 +mydomain = redhat94.maj
 
  # SENDING MAIL
  # 
 @@ -114,7 +114,7 @@ mail_owner = postfix
  # myorigin also specifies the default domain name that is appended
  # to recipient addresses that have no @domain part.
  #
 -#myorigin = $myhostname
 +myorigin = $myhostname
  #myorigin = $mydomain
 
  # RECEIVING MAIL
 @@ -129,10 +129,10 @@ mail_owner = postfix
  #
  # Note: you need to stop/start Postfix when this parameter changes.
  #
 -#inet_interfaces = all
 +inet_interfaces = all
  #inet_interfaces = $myhostname
  #inet_interfaces = $myhostname, localhost
 -inet_interfaces = localhost
 +#inet_interfaces = localhost
 
  # Enable IPv4, and IPv6 if supported
  inet_protocols = all
 @@ -180,8 +180,8 @@ inet_protocols = all
  #
  # See also below, section "REJECTING MAIL FOR UNKNOWN LOCAL USERS".
  #
 -mydestination = $myhostname, localhost.$mydomain, localhost
 -#mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
 +#mydestination = $myhostname, localhost.$mydomain, localhost
 +mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
  #mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain,
  #	mail.$mydomain, www.$mydomain, ftp.$mydomain
 
 @@ -280,7 +280,7 @@ unknown_local_recipient_reject_code = 550
  # of listing the patterns here. Specify type:table for table-based lookups
  # (the value on the table right-hand side is not used).
  #
 -#mynetworks = 168.100.189.0/28, 127.0.0.0/8
 +mynetworks = 172.16.0.0/16, 127.0.0.0/8
  #mynetworks = $config_directory/mynetworks
  #mynetworks = hash:/etc/postfix/network_table
 
 @@ -736,3 +736,10 @@ smtp_tls_CAfile = /etc/pki/tls/certs/ca-bundle.crt
  smtp_tls_security_level = may
  meta_directory = /etc/postfix
  shlib_directory = /usr/lib64/postfix
 +
 +#smtp_tls_protocols = !SSLv2, !SSLv3
 +#smtp_tls_mandatory_protocols = !SSLv2, !SSLv3
 +#smtpd_tls_protocols = !SSLv2, !SSLv3
 +#smtpd_tls_mandatory_protocols = !SSLv2, !SSLv3
 +
 +
~~~
~~~
# diff --git a/master.cf b/master.cf
~~~
~~~
  index 0af43e1..3ebe428 100644
  --- a/master.cf
  +++ b/master.cf
 @@ -16,7 +16,7 @@ smtp      inet  n       -       n       -       -       smtpd
  #tlsproxy  unix  -       -       n       -       0       tlsproxy
  #submission inet n       -       n       -       -       smtpd
  #  -o syslog_name=postfix/submission
 -#  -o smtpd_tls_security_level=encrypt
 +  -o smtpd_tls_security_level=may
  #  -o smtpd_sasl_auth_enable=yes
  #  -o smtpd_tls_auth_only=yes
  #  -o smtpd_reject_unlisted_recipient=no
~~~

## 起動
~~~
 # postfix check
~~~
~~~
 # systemctl enable --now postfix
~~~
~~~
 # firewall-cmd --permanent --add-service smtp
~~~
~~~
 # firewall-cmd --reload
~~~
~~~
 # firewall-cmd --list-all
~~~

## メール送信
~~~
 # telnet localhost 25
~~~
~~~
# helo localhost
 # mail from:root@redhat94.maj
 # rcpt to:majsdf@redhat94.maj
 # data
 # test mail body
 # .
 # quit
~~~
