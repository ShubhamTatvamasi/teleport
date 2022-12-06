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

Create an admin user:
```bash
kubectl -n teleport-cluster exec -it -c teleport \
  $(kubectl -n teleport-cluster get po -l app=teleport-cluster --no-headers | awk '{print $1}') \
  -- tctl users add admin --roles=editor,access --logins=root,ubuntu,ec2-user
```

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
    - k8s-group
    kubernetes_users:
    - admin
  deny: {}
EOF
```

Create Teleport Role:
```bash
kubectl apply -f - << EOF
apiVersion: resources.teleport.dev/v5
kind: TeleportRole
metadata:
  name: admin-role
  namespace: teleport-cluster
spec:
  allow:
    rules:
      - resources: ['user', 'role']
        verbs: ['list','create','read','update','delete']
EOF
```

Create Teleport User:
```bash
kubectl apply -f - << EOF
apiVersion: resources.teleport.dev/v2
kind: TeleportUser
metadata:
  name: admin
  namespace: teleport-cluster
spec:
  roles: ['admin-role']
EOF
```

Uninstall:
```bash
helm un teleport-cluster -n teleport-cluster
kubectl delete ns teleport-cluster
```
