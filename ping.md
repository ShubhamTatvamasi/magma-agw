# Enable Ping 

Install Yq:
```bash
add-apt-repository --yes ppa:rmescandon/yq
apt install yq
```

Check if the ping is blocked:
```bash
yq '.access_control.block_agw_local_ips' /etc/magma/pipelined.yml
```

Allow ping:
```bash
sudo yq e '.access_control.block_agw_local_ips = false' -i /etc/magma/pipelined.yml
```

