# create user

create `magma` user with `magma` password:
```bash
sudo useradd -m magma -s /bin/bash -p $(echo magma | openssl passwd -1 -stdin)
```

