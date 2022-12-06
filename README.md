# teleport

Create teleport config directories:
```bash
mkdir -p ~/teleport/config ~/teleport/data
```

Generate teleport config file:
```bash
docker run --hostname localhost --rm \
  --entrypoint=/bin/sh \
  -v ~/teleport/config:/etc/teleport \
  public.ecr.aws/gravitational/teleport:11 -c "teleport configure > /etc/teleport/teleport.yaml"
```

Start teleport server:
```bash
docker-compose up -d
```

Create an admin user:
```bash
docker exec teleport tctl users add admin --roles=editor,access --logins=root,ubuntu,ec2-user
```

---

Skip TLS for agent:
```bash
yq e '.insecureSkipProxyTLSVerify = true' -i prod-cluster-values.yaml
```

---

Download tsh client

https://goteleport.com/docs/installation/#macos
