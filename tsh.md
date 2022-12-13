# tsh

https://goteleport.com/docs/installation/

Client cleanup:
```bash
rm -rf ~/.tsh
```

Login for 30 hours:
```bash
tsh login --ttl 1800
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

---

### mysql

List databases:
```bash
tsh db ls
```

login into database:
```bash
tsh db login --db-user=root --db-name=mysql mysql
```

Connecti to mysql server:
```bash
tsh db connect --db-user=root --db-name=mysql mysql
```
