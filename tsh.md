# tsh

Client cleanup:
```bash
rm -rf ~/.tsh
```

Client cli login:
```bash
tsh login --proxy=teleport.shubhamtatvamasi.com --user=admin --insecure
```

SSH into the Teleport Server.
```bash
tsh ssh root@teleport.shubhamtatvamasi.com
```
> This will use port `3022` to SSH into the container.

---

### kubernetes

List clusters:
```bash
tsh kube ls
```

login into a cluster:
```bash
tsh kube login cks
```

Test your connection:
```bash
kubectl get pods
```
