---
  title: cifs-utils
  layout: default
---
# cifs-utils

## コマンド
~~~
 # yum install cifs-utils.x86_64
 # mount -t cifs -o username=<share user>,password=<sharepassword>,dir_mode=0755,file_mode=0755 //WIN_PC_IP/<share name> /mnt
~~~

~~~
 # vi /etc/fstab
 
 //WIN_PC_IP/<share name>    /<mntpoint>   cifs  _netdev,username=<share user>,password=<share password>,dir_mode=0755,file_mode=0755,uid=500,gid=500 0 0
~~~
