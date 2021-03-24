# magma-agw

### Prerequisites

[VirtualBox](https://www.virtualbox.org) [Vagrant](https://vagrantup.com)

---

### Build AGW

download magma 1.4.0:
```
HOST$ wget https://github.com/magma/magma/archive/refs/tags/v1.4.0.tar.gz
```

extract and move to gateway folder: 
```
HOST$ tar xvfz v1.4.0.tar.gz
HOST$ cd magma-1.4.0/lte/gateway
```

download vagrant box:
```
HOST$ vagrant box add magmacore/magma_dev \
  --box-version=1.1.20201221 \
  --provider=virtualbox
```

start vagrant box:
```bash
HOST$ vagrant up magma
```

ssh inside vagrant box and
```bash
HOST$ vagrant ssh magma

AGW$ cd magma/lte/gateway
AGW$ make run
```
---

### Configure AWG

First, copy the root CA for your Orchestrator deployment into your AGW:
```
HOST$ scp rootCA.pem magma@10.0.2.1:~
HOST$ ssh magma@10.0.2.1

AGW$ sudo mkdir -p /var/opt/magma/certs/
AGW$ sudo mv rootCA.pem /var/opt/magma/certs/rootCA.pem
```

Then, point your AGW to your Orchestrator:
```
AGW$ sudo mkdir -p /var/opt/magma/configs
AGW$ cd /var/opt/magma/configs
```

add control_proxy:
```bash
AGW$ cat << EOF > control_proxy.yml
cloud_address: controller.magma.shubhamtatvamasi.com
cloud_port: 443
bootstrap_address: bootstrapper-controller.magma.shubhamtatvamasi.com
bootstrap_port: 443

rootca_cert: /var/opt/magma/certs/rootCA.pem
EOF
```

Then restart your services to pick up the config changes:
```
AGW$ sudo service magma@* stop
AGW$ sudo service magma@magmad restart
```

check logs:
```bash
sudo tail -f /var/log/syslog
```

```
AGW$ show_gateway_info.py
```

