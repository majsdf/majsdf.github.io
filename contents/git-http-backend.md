---
title: git-http-backend
layout: default
---

# git-http-backend

## /etc/httpd/conf.d
~~~
# cat git-http-backend.conf

SetENV GIT_PROJECT_ROOT /pub/git
SetENV GIT_HTTP_EXPORT_ALL
ScriptAlias /git-http-backend "/usr/libexec/git-core/git-http-backend"
<Location /git-http-backend>
    AuthType Digest
    AuthDigestProvider file
    AuthName "username"
    AuthUserFile /pub/git/git.htdigest
    Require valid-user
    Order allow,deny
    Allow from all
</Location>
~~~
~~~
# htdigest -c /repository/git.htdigest "Git" username

Adding password for username in realm Git.
New password:
Re-type new password:
~~~
## clone
~~~
git clone http://redhat94/git-http-backend/document.git
~~~
