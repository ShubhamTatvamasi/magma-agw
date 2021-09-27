# logs

log memory usage of mme:
```bash
while true; do \
  sudo pmap -d \
  $(ps aux | grep mme | grep -v grep | awk '{print $2}') | \
  tail -n 1 >> mme-pmap.logs; \
  sleep 2; \
  done
```

