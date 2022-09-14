# multipass

Create instance:
```bash
multipass launch focal \
  --name magma \
  --disk 40G \
  --mem 4G \
  --cpus 2 \
  --network en0
```

SSH into vm:
```bash
multipass shell magma
```

Check if VM is running:
```bash
multipass list
```

delete vm:
```bash
multipass delete magma
multipass purge
```
