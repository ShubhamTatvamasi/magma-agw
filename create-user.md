# create user


```bash
sudo useradd -m magma -s /bin/bash -p $(echo magma | openssl passwd -1 -stdin)
```

