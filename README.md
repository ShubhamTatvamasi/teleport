# teleport

Start teleport server:
```bash
docker-compose up -d
```

Create an admin user:
```bash
docker exec teleport tctl users add admin --roles=editor,access --logins=root,ubuntu,ec2-user
```

Uninstall:
```bash
docker-compose down -v
```

---

Download tsh client

https://goteleport.com/docs/installation/#macos
