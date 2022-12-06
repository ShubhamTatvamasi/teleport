# kubernetes

https://teleport.shubhamtatvamasi.com

Create a user and group:
```bash
tctl --insecure create -f << EOF
kind: role
version: v5
metadata:
  name: devs
spec:
  allow:
    logins: ['{{internal.logins}}']
    kubernetes_groups: ['{{internal.kubernetes_groups}}']
    node_labels:
      '*': '*'
    kubernetes_labels:
      '*': '*'
EOF
```

Create a user:
```bash
tctl --insecure create -f << EOF
kind: user
version: v2
metadata:
  name: admin
spec:
  roles: ['devs']
  traits:
    logins: ['admin']
    kubernetes_groups: ['edit']
EOF
```
