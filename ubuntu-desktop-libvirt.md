# Ubuntu Desktop Libvirt

Update network config:
```bash
sudo vim /etc/netplan/01-network-manager-all.yaml
```

Setup bridge network:
```yaml
# Let NetworkManager manage all devices on this system
network:
  version: 2
  renderer: NetworkManager
  ethernets:
    enp4s0:
      dhcp4: false

  bridges:
    br0:
      interfaces:
      - enp4s0
      addresses:
      - 10.0.2.3/24
```

Apply chnages:
```bash
sudo netplan apply
```
