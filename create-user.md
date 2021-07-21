# create user

create `magma` user with `magma` password:
```bash
NEW_USER=magma
sudo useradd -m $NEW_USER -s /bin/bash -p $(echo $NEW_USER | openssl passwd -1 -stdin)
```

