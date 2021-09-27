# logs

log memory usage of mme:
```bash
while true; do \
  MME_PROCESS_ID="$(ps aux | grep /usr/local/bin/mme | grep -v grep | awk '{print $2}')" \
  MME_MEMORY_USED="$(sudo pmap -d ${MME_PROCESS_ID} | tail -n 1)" \
  echo "$(date '+%m/%d/%Y %H:%M:%S') -- ${MME_MEMORY_USED}" | tee -a mme-pmap.logs; \
  sleep 2; \
  done
```

