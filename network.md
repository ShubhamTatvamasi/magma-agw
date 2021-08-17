# network


https://askubuntu.com/a/1317043

check network hardware:
```bash
lshw -C network
```

add network config on following file:
```bash
vim /etc/netplan/50-cloud-init.yaml
```

update your mac address:
```yaml
network:
    version: 2
    ethernets:
        eth0:
            dhcp4: true
            match:
                macaddress: <YOUR MAC ID HERE>
            set-name: enp2s0
```

test and apply:
```bash
netplan try
netplan apply
```

### Debain

Rename network interface in `/etc/network/interfaces`
```
rename ens18=enp1s0
rename ens19=enp2s0
```

restart network
```bash
sudo systemctl restart networking
```

update MME IP
```bash
vim /etc/network/interfaces.d/eth1
```

