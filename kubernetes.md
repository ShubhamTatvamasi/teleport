# kubernetes

https://teleport.shubhamtatvamasi.com

Create a user and group:
```bash
tctl create -f << EOF
kind: role
metadata:
  name: kube-access
version: v5
spec:
  allow:
    kubernetes_labels:
      '*': '*'
    kubernetes_groups:
    - admin
    kubernetes_users:
    - $(kubectl config view -o jsonpath="{.contexts[?(@.name==\"$(kubectl config current-context)\")].context.user}")
  deny: {}
EOF
```
