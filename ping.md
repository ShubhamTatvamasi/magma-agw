# Enable Ping 

Install Yq:
```bash
sudo apt install jq -y

VERSION=$(curl -s "https://api.github.com/repos/mikefarah/yq/tags" | jq -r '.[2].name')
BINARY=yq_linux_amd64

sudo wget https://github.com/mikefarah/yq/releases/download/${VERSION}/${BINARY} -O /usr/local/bin/yq
sudo chmod +x /usr/local/bin/yq

```

