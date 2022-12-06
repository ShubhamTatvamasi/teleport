# kubernetes

https://teleport.shubhamtatvamasi.com

Create a user and group:
```bash
tctl --insecure create -f << EOF
kind: role
version: v5
metadata:
  name: admin
spec:
  allow:
    logins: ['admin']
    kubernetes_groups: ['admin']
    node_labels:
      '*': '*'
    kubernetes_labels:
      '*': '*'
EOF
```
