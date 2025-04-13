---
title: dovecot
layout: default
---
# Dovecot: MDA
a secure and highly configurable IMAP and POP3 server

## 設定ファイル
~~~
# diff --git a/conf.d/10-auth.conf b/conf.d/10-auth.conf
~~~
~~~
 index 3e9c4e4..56b0857 100644
 --- a/conf.d/10-auth.conf
 +++ b/conf.d/10-auth.conf
 @@ -7,7 +7,7 @@
  # matches the local IP (ie. you're connecting from the same computer), the
  # connection is considered secure and plaintext authentication is allowed.
  # See also ssl=required setting.
 -#disable_plaintext_auth = yes
 +disable_plaintext_auth = no
  
  # Authentication cache size (e.g. 10M). 0 means it's disabled. Note that
  # bsdauth and PAM require cache_key to be set for caching to be used.
~~~
~~~
# diff --git a/conf.d/10-mail.conf b/conf.d/10-mail.conf
~~~
~~~
 index fee4802..33bc2c2 100644
 --- a/conf.d/10-mail.conf
 +++ b/conf.d/10-mail.conf
 @@ -27,7 +27,7 @@
  #
  # <doc/wiki/MailLocation.txt>
  #
 -#mail_location = 
 +mail_location = mbox:/var/empty:INBOX=/var/mail/%u:INDEX=MEMORY
  
  # If you need to set multiple mailbox locations or want to change default
  # namespace settings, you can do it by defining namespace sections.
~~~
~~~
# diff --git a/conf.d/10-master.conf b/conf.d/10-master.conf
~~~
~~~
 index d52ce80..5bd60ad 100644
 --- a/conf.d/10-master.conf
 +++ b/conf.d/10-master.conf
 @@ -104,9 +104,9 @@ service auth {
    }
  
    # Postfix smtp-auth
 -  #unix_listener /var/spool/postfix/private/auth {
 -  #  mode = 0666 
 -  #}
 +  unix_listener /var/spool/postfix/private/auth {
 +    mode = 0666
 +  }
  
    # Auth process is run as this user.
    #user = $default_internal_user
 @@ -116,7 +116,7 @@ service auth-worker {
    # Auth worker process is run as root by default, so that it can access
    # /etc/shadow. If this isn't necessary, the user should be changed to
    # $default_internal_user.
 -  #user = root
 +  user = root
  }
  
  service dict {
~~~
~~~
# diff --git a/conf.d/10-ssl.conf b/conf.d/10-ssl.conf
~~~
~~~
 index 0bee01e..99da1ff 100644
 --- a/conf.d/10-ssl.conf
 +++ b/conf.d/10-ssl.conf
 @@ -5,7 +5,7 @@
  # SSL/TLS support: yes, no, required. <doc/wiki/SSL.txt>
  # disable plain pop3 and imap, allowed are only pop3+TLS, pop3s, imap+TLS and imaps
  # plain imap and pop3 are still allowed for local connections
 -ssl = required
 +ssl = no
  
  # PEM encoded X.509 SSL/TLS certificate and private key. They're opened before
  # dropping root privileges, so keep the key file unreadable by anyone but
~~~
~~~
# diff --git a/dovecot.conf b/dovecot.conf
~~~
~~~
 index b67e9eb..bd36efb 100644
 --- a/dovecot.conf
 +++ b/dovecot.conf
 @@ -21,13 +21,13 @@
  # --sysconfdir=/etc --localstatedir=/var
  
  # Protocols we want to be serving.
 -#protocols = imap pop3 lmtp submission
 +protocols = pop3
  
  # A comma separated list of IPs or hosts where to listen in for connections. 
  # "*" listens in all IPv4 interfaces, "::" listens in all IPv6 interfaces.
  # If you want to specify non-default ports or anything more complex,
  # edit conf.d/master.conf.
 -#listen = *, ::
 +listen = *
  
  # Base directory where to store runtime data.
  #base_dir = /var/run/dovecot/
~~~

## 起動
~~~
 # postfix check
~~~
~~~
 # systemctl enable --now postfix
~~~
~~~
 # firewall-cmd --permanent --add-service=imaps --add-service=imap --add-service=pop3s --add-service=pop3
~~~
~~~
 # firewall-cmd --reload
~~~
~~~
 # firewall-cmd --list-all
~~~

