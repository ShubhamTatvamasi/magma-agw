# debug

Fix AGW crash:
```bash
wget https://ftp.debian.org/debian/pool/main/g/gcc-10/liblsan0_10.2.1-6_amd64.deb
wget https://ftp.debian.org/debian/pool/main/g/gcc-10/gcc-10-base_10.2.1-6_amd64.deb
sudo dpkg -i gcc-10-base_10.2.1-6_amd64.deb liblsan0_10.2.1-6_amd64.deb
```
