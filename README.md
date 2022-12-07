# teleport

Create a teleport directory and place your `key.pem` and `cert.pem` in it:
```bash
mkdir -p teleport
```

Start teleport server:
```bash
docker-compose up -d --force-recreate
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
