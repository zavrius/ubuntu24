1. Отключить управление сетью cloud-init

sudo nano /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg

network: {config: disabled}

2. Создать свой netplan конфиг

sudo nano /etc/netplan/01-static.yaml

network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: no
      addresses:
        - 192.168.3.11/24
      routes:
        - to: default
          via: 192.168.3.1
      nameservers:
        addresses:
          - 192.168.3.1
          - 8.8.8.8


2.1 Выставим права 600 
sudo chmod 600 /etc/netplan/01-static.yaml

3. Удалить старый DHCP конфиг
sudo rm /etc/netplan/50-cloud-init.yaml

4. Применить конфигурацию
sudo netplan generate
sudo netplan apply

5. Проверить

ip a | grep gl
inet 192.168.3.11/24 brd 192.168.3.255 scope global enp0s3

ip r | grep def
default via 192.168.3.1 dev enp0s3 proto static 

grep -v ^# /etc/resolv.conf 
nameserver 127.0.0.53
options edns0 trust-ad
search .


6. Проверка после перезагрузки
sudo reboot


Маленький совет администратора (чтобы не поймать себе приключений):
Перед применением можно использовать безопасный режим:
sudo netplan try

Он откатит настройки через 120 секунд, если сеть пропадёт.
