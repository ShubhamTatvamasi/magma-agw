# apt

add latest magma AGW repo:
```bash
sudo echo "deb https://artifactory.magmacore.org/artifactory/debian-test focal-ci main" >> \
  /etc/apt/sources.list.d/magma.list
```

update pacakges:
```bash
sudo apt update
```

check if Installed and Candidate are different:
```bash
sudo apt policy magma | head
```

upgrade magma:
```bash
sudo apt upgrade magma
```
