Клонируем node1 в node2 и после применяем на node2 

sudo hostnamectl set-hostname node2
sudo nano /etc/hosts
sudo nano /etc/netplan/01-static.yaml
sudo netplan apply
sudo rm /etc/machine-id
sudo systemd-machine-id-setup

1)
1. Поменять hostname
sudo hostnamectl set-hostname node2
hostnamectl

2. Обновить /etc/hosts
sudo nano /etc/hosts
127.0.1.1 node1 меняем на 127.0.1.1 node2

а также добавим туда и др машины

192.168.3.11 node1
192.168.3.12 node2
192.168.3.13 node3
192.168.3.14 node4
192.168.3.15 node5
192.168.3.16 node6
192.168.3.17 node7
192.168.3.18 node8
192.168.3.19 node9


3. Изменить IP в netplan
sudo nano /etc/netplan/01-static.yaml

меняем IP на 192.168.3.12/24

4. Применить сеть
sudo netplan apply
ip a 
ip r
hostname

(Очень желательно) изменить Machine ID --> sudo systemd-machine-id-setup
Если клонируется VM, machine-id будет одинаковый, что плохо для:
- systemd
- DHCP
- кластеров
- journald

2)
в VirtualBox при клонировании лучше выбирать “Reinitialize MAC address of network cards”, иначе две VM могут получить одинаковый MAC, и сеть начнёт вести себя странно (DHCP, ARP, кеши).
ip link show enp0s3

