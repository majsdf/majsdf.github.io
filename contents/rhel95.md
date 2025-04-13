---
title: rhel95
layout: default
---

# RHEL95: Red Hat Enterprise Linux release 9.5 (Plow)
## hostname
~~~
# hostnamectl set-hostname redhat94.localdomain.ma.jp
~~~
## /etc/NetworkManager/system-connections/ens160.nmconnection
~~~
[connection]
id=ens160
uuid=56cd9bc3-75dc-3cb2-af35-2dba5cd306e3
type=ethernet
autoconnect-priority=-999
interface-name=ens160
timestamp=1739481364
[ipv4]
address1=172.16.0.100/16,172.16.0.2
dns=172.16.0.2
method=manual
~~~
~~~
# nmcli connection up ens160
~~~

## firewalld
~~~
# systemctl status firewalld
# systemctl stop firewalld
# systemctl disable firewalld
# yum remove firewalld
~~~
## yum
~~~
# subscription-manager register
# yum upgrade
~~~
## /etc/fstab
~~~
/dev/mapper/rhel-root   /                       xfs     defaults        0 0
UUID=efb94154-1678-4028-b0ed-95dcb90c701f /boot                   xfs     defaults        0 0
UUID=3F04-C625          /boot/efi               vfat    umask=0077,shortname=winnt 0 2
/dev/mapper/rhel-swap   none                    swap    defaults        0 0
/dev/sr0                /mnt/iso                iso9660 ro 0 0
~~~
## /etc/yum.repos.d/media.repo
~~~
[media-BaseOS]
name=RHEL9.4 - BaseOS
metadata_expire=-1
gpgcheck=1
enabled=1
baseurl=file:///mnt/iso/BaseOS/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
 
[media-AppStream]
name=RHEL9.4 - AppStream
metadata_expire=-1
gpgcheck=1
enabled=1
baseurl=file:///mnt/iso/AppStream/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
~~~

