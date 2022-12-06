# helm

https://goteleport.com/docs/management/guides/teleport-operator/

Add the helm repo:
```bash
helm repo add teleport https://charts.releases.teleport.dev
helm repo update
```

Install teleport operator:
```bash
helm install teleport-cluster teleport/teleport-cluster \
  --create-namespace \
  --namespace teleport-cluster \
  --set clusterName=k8s.shubhamtatvamasi.com \
  --set operator.enabled=true \
  --set acme=true \
  --set acmeEmail=shubhamtatvamasi@gmail.com \
  --version 11.1.1
```

Uninstall server:
```bash
helm un teleport-cluster -n teleport-cluster
kubectl delete ns teleport-cluster
```

Uninstall agent:
```bash
helm un teleport-agent -n teleport
kubectl delete ns teleport
```

---

Skip TLS for agent:
```bash
yq e '.insecureSkipProxyTLSVerify = true' -i prod-cluster-values.yaml
```
