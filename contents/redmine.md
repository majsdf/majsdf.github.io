---
title: redmine
layout: default
---

# redmine

## postgresql
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
## redmine
~~~
# cd /var/lib
# tar xvpf redmine-6.0.4.tar.gz
# chown -R apache redmine-6.0.4
~~~
~~~
# cd config
# cp -p database.yml.example database.yml
# cp -p configuration.yml.example configuration.yml
~~~
~~~
# cd /var/lib/redmine-6.0.4
# yum install g++ make
# bundle config set --local without 'development test'
# gem install bundler
# bundle install
# bin/rake generate_secret_token
# bin/rake db:migrate RAILS_ENV="production"
# bin/rake redmine:load_default_data RAILS_ENV="production"
# gem install passenger -N
# passenger-install-apache2-module --auto --languages ruby
# passenger-install-apache2-module --snippet
~~~

## # cat /etc/httpd/conf.d/redmine.conf
~~~
  LoadModule passenger_module /usr/local/share/gems/gems/passenger-6.0.26/buildout/apache2/mod_passenger.so
  <IfModule mod_passenger.c>
    PassengerRoot /usr/local/share/gems/gems/passenger-6.0.26
    PassengerDefaultRuby /usr/bin/ruby
  </IfModule>
  Alias /redmine /var/lib/redmine-5.1.7/public
  <Directory "/var/lib/redmine-5.1.7/public">
    Require all granted
  </Directory>
  <Location /redmine>
    PassengerBaseURI /redmine
    PassengerAppRoot /var/lib/redmine-5.1.7
  </Location>
~~~
## ファイル
~~~
# cd /var/lib/redmine/public
# cp -p htaccess.fcgi.example .htaccess
# cp -p dispatch.fcgi.example dispatch.fcgi
~~~
## フック
~~~
# cat /var/opt/git/repository.git/hooks/post-receive

   #!/bin/sh
   wget  http://172.16.0.100/redmine/sys/fetch_changesets?key=UhqEogp240dRTT3Eek62

# chmod 755 /var/opt/git/repository.git/hooks/post-receive
# chown apache:apache /var/opt/git/repository.git/hooks/post-receive
~~~
