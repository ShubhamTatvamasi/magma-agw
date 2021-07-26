# S1AP tests

start AGW and S1AP VMs:
```bash
vagrant up magma magma_test
```
---

ssh to AGW VM:
```bash
vagrant ssh magma
```

start AGW services:
```bash
sudo systemctl start magma@magmad
```
---


ssh to S1AP VM:
```bash
vagrant ssh magma_test
```

move to integ_tests directory:
```bash
cd /home/vagrant/magma/lte/gateway/python/integ_tests
```

run attach_detach test:
```bash
make integ_test TESTS=s1aptests/test_attach_detach.py
```


