# bare-metal

check that we should have 2 network interface:
```bash
ip a
```

become root and download agw installer:
```bash
sudo su
wget https://raw.githubusercontent.com/magma/magma/v1.6/lte/gateway/deploy/agw_install_ubuntu.sh
```

install agw with static IP and it's gateway:
```bash
bash agw_install_ubuntu.sh 192.168.5.56/24 192.168.5.1
```

check installation process:
```bash
journalctl -fu agw_installation
```

open eth1 interface file:
```bash
sudo vim /etc/network/interfaces.d/eth1
```
```
auto eth0
  iface eth0 inet static
  address 192.168.4.15
  netmask 255.255.255.0
  gateway 192.168.4.1
```



