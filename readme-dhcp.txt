sudo cat /etc/netplan/50-cloud-init.yaml 
network:
  version: 2
  ethernets:
    enp0s3:
      dhcp4: true

ip a | grep gl 
inet 192.168.3.162/24 metric 100 brd 192.168.3.255 scope global dynamic enp0s3

ip r | grep def
default via 192.168.3.1 dev enp0s3 proto dhcp src 192.168.3.162 metric 100 

grep -v ^# /etc/resolv.conf
nameserver 127.0.0.53
options edns0 trust-ad
search .
