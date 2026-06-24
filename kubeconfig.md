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
  name: kube-access
spec:
  allow:
    kubernetesLabels:
      "*": "*"
    kubernetesGroups:
      - system:masters
    kubernetesUsers:
      - admin
EOF
```



