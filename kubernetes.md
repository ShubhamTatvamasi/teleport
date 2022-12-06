# kubernetes

https://teleport.shubhamtatvamasi.com

Update `access` role to allow the access to kubernetes cluster:
```
spec.allow.kubernetes_groups[1] = system:masters
```
