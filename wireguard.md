# wireguard

### Solution for libvirt

enable on auto start:
```bash
sudo crontab -e
```
```
@reboot wg-quick up Shubham_HP
@reboot ip route del default
@reboot ip route add default via 192.168.122.1 dev eth0
```

