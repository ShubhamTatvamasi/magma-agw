# magma-agw

### Prerequisites

[VirtualBox](https://www.virtualbox.org) [Vagrant](https://vagrantup.com)

---

### Setup AGW

download magma repo:
```bash
git clone https://github.com/magma/magma.git --depth 1
```

move to gateway folder: 
```bash
cd magma/lte/gateway
```

download vagrant box:
```bash
vagrant box add magmacore/magma_dev \
  --box-version=1.1.20210618 \
  --provider=virtualbox
```

install ansible:
```bash
sudo apt install ansible
```

start vagrant box:
```bash
vagrant up magma
```

ssh inside vagrant box:
```bash
vagrant ssh magma
```
---

### Build AGW

build AGW
```bash
cd magma/lte/gateway
make run
```

Install scp plugin for Vagrant and copy the rootCA.pem file to AGW
```bash
vagrant plugin install vagrant-scp
vagrant scp /tmp/rootCA.pem magma:~

vagrant ssh magma
```
---

### Configure AGW

First, copy the root CA for your Orchestrator deployment into your AGW:
```bash
sudo mkdir -p /var/opt/magma/tmp/certs/
sudo mv rootCA.pem /var/opt/magma/tmp/certs/rootCA.pem
```

Then, point your AGW to your Orchestrator:
```bash
sudo mkdir -p /var/opt/magma/configs
cd /var/opt/magma/configs
sudo vim control_proxy.yml
```

Put the following contents into the file:
```yaml
cloud_address: controller.magma.shubhamtatvamasi.com
cloud_port: 443
bootstrap_address: bootstrapper-controller.magma.shubhamtatvamasi.com
bootstrap_port: 443
fluentd_address: fluentd.magma.shubhamtatvamasi.com
fluentd_port: 24224

rootca_cert: /var/opt/magma/tmp/certs/rootCA.pem
```

Then restart your services to pick up the config changes:
```bash
sudo service magma@* stop
sudo service magma@magmad restart
sudo service magma@magmad status

# check status of magma services
sudo systemctl status magma@*
```

check logs:
```bash
sudo tail -f /var/log/syslog
sudo journalctl -u magma@magmad -f
```

grab the hardware secrets off your AGW:
```bash
show_gateway_info.py

# if above command doesn't work
sudo pip3 install snowflake
export AGW_SCRIPTS=/home/vagrant/magma/orc8r/gateway/python
ln -s ${AGW_SCRIPTS}/magma ${AGW_SCRIPTS}/scripts/
${AGW_SCRIPTS}/scripts/show_gateway_info.py
```

test network:
```bash
checkin_cli.py
```

---

### Extras

Generate new Challenge key:
```bash
cd /var/opt/magma/certs
sudo openssl ecparam -name secp384r1 -genkey -noout -out gw_challenge.key
sudo chmod 644 gw_challenge.key
```

Generate new Hardware ID:
```bash
sudo uuidgen > /etc/snowflake
sudo snowflake --force-new-key
```

remove gateway keys and network config:
```bash
sudo rm /var/opt/magma/certs/gateway.crt
sudo rm /var/opt/magma/certs/gateway.key
sudo rm /var/opt/magma/configs/gateway.mconfig
```
---

check certificate details:
```bash
openssl x509 -text -noout -in rootCA.pem

openssl x509 -text -noout -in /var/opt/magma/tmp/certs/rootCA.pem
```


