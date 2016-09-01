# PXE
PXE Network Installations

### Preparation
You should prepare "pxelinux.0" file in the tftp-server's folder.

For Debian users:  
```sh
$ wget http://ftp.nl.debian.org/debian/dists/testing/main/installer-amd64/current/images/netboot/netboot.tar.gz

$ tar -zxvf netboot.tar.gz
```

### Active service
```sh
$ sudo service isc-dhcp-server start
$ sudo service tftpd-hpa start
```
