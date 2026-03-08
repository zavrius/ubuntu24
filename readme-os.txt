lsb_release -a | grep -i desc ; uname -r

Description:	Ubuntu 24.04.4 LTS
6.17.0-14-generic

apt list --installed | grep linux-generic
linux-generic-hwe-24.04/noble-updates,noble-security,now 6.17.0-14.14~24.04.1 amd64 [установлен]

-------------------------------------------------------
Здесь ядро 6.17 - это значит, что я при установке выбрал ядро HWE (Hardware Enablement) - смысл поддержка нового железа
поэтому мой uname -r = 6.17

Но есть и обычный (по-дефолту) GA (General Availability) 6.8 - базовое стабильное ядро LTS

GA (6.8)
максимально стабильное
редко меняется
идеально для серверов

HWE (6.17)
новые драйверы
лучше поддержка нового CPU / NIC / GPU
быстрее поддержка нового железа

Canonical будет обновлять ядро каждые ~6 месяцев, подтягивая его из следующего релиза Ubuntu.
Например так: 6.8  → 6.11 → 6.14 → 6.17 → ...


Супер-короткая «админская сводка» через sudo
(Кто управляет сетью (netplan renderer)
 
 Netplan
  ↓
systemd-networkd
  ↓
systemd-resolved


bash script
echo "Kernel: $(uname -r)"
echo "Renderer:"; grep renderer /etc/netplan/*.yaml
echo "IP:"; ip -brief a
echo "Route:"; ip r | grep default
