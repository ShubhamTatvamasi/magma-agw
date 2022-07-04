# Ubuntu Desktop Libvirt

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
      - 192.168.150.2/24
```
