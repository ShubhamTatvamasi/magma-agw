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
```
HOST$ vagrant up magma
```

ssh inside vagrant box and
```
HOST$ vagrant ssh magma

AGW$ cd magma/lte/gateway
AGW$ make run
```
---

### Configure AWG

First, copy the root CA for your Orchestrator deployment into your AGW:
```
HOST$ scp -P 2222 -i ~/.vagrant.d/insecure_private_key rootCA.pem vagrant@127.0.0.1:~
HOST$ vagrant ssh magma

AGW$ sudo mkdir -p /var/opt/magma/certs/
AGW$ sudo mv rootCA.pem /var/opt/magma/certs/rootCA.pem
```

Then, point your AGW to your Orchestrator:
```
AGW$ sudo mkdir -p /var/opt/magma/configs
AGW$ cd /var/opt/magma/configs
```

add control_proxy:
```
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
```
AGW$ sudo tail -f /var/log/syslog
```

grab the hardware secrets off your AGW:
```
AGW$ cd ~/magma/orc8r/gateway/python/

AGW$ ./scripts/show_gateway_info.py
```

