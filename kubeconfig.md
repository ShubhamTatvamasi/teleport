# Kubeconfig


```bash
export KUBECONFIG=~/.kube/teleport-kubeconfig.yaml
```

```
tsh kube login teleport.k9s.shubhamtatvamasi.com
```

```bash
mv ~/.kube/config ~/.kube/config.bak
```

```
export KUBECONFIG=~/.kube/config.bak:~/.kube/teleport-kubeconfig.yaml
```

```
kubectl config view --merge --flatten > ~/.kube/config
```

```yaml
kubectl apply -f - << EOF
apiVersion: resources.teleport.dev/v5
kind: TeleportRole
metadata:
  name: kube-admin
  namespace: teleport
spec:
  allow:
    kubernetes_labels:
      "*": "*"
    kubernetes_groups:
      - system:masters
    kubernetes_users:
      - admin
EOF
```


```bash
kubectl -n teleport \
  exec -it deploy/teleport-auth -- \
  tctl users update admin --set-roles=editor,access,auditor,kube-admin
```


```
tsh logout
```

```
tsh login --proxy=teleport.k9s.shubhamtatvamasi.com:443 --auth=local --user=admin teleport.k9s.shubhamtatvamasi.com
```

```
tsh kube login teleport.k9s.shubhamtatvamasi.com
```


