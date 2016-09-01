# PXE
PXE Network Installations

### Preparation
You should prepare "pxelinux.0" file in the tftp-server's folder.

For Debian users:  
```sh
$ wget http://ftp.nl.debian.org/debian/dists/testing/main/installer-amd64/current/images/netboot/netboot.tar.gz

$ tar -zxvf netboot.tar.gz
```

### Installation
Default ethercard is eth0, you can choose another one.

1. DHCP
```sh
$ ethercard=enp10s0 ./pxe-install dhcp
Do you want to auto install (yes/no)? no
sudo apt-get update
sudo apt-get install isc-dhcp-server

Sample:
$ cat /etc/dhcp/dhcpd.conf
subnet 192.168.33.0 netmask 255.255.254.0 {
       	range 192.168.33.10 192.168.33.100;
       	option routers 192.168.33.1;
       	option domain-name-servers 8.8.8.8;
       	filename "pxelinux.0";
       	next-server 192.168.33.32  ;

}
```
2. TFTP
```sh
$ ./pxe-install tftp
Do you want to auto install (yes/no)? no
sudo apt-get update
sudo apt-get install tftpd-hpa

$ cat /etc/default/tftpd-hpa
# /etc/default/tftpd-hpa

TFTP_USERNAME="tftp"
TFTP_DIRECTORY="/root"
TFTP_ADDRESS="0.0.0.0:69"
TFTP_OPTIONS="--secure"
```

### Active service
```sh
$ sudo service isc-dhcp-server start
$ sudo service tftpd-hpa start
```
