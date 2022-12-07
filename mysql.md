# mysql

Start mysql server:
```bash
docker run --name mysql -e MYSQL_ROOT_PASSWORD=password -d mysql
```

Download teleport client:
```bash
wget https://get.gravitational.com/teleport-v11.1.2-linux-amd64-bin.tar.gz
```

Extract files:
```bash
tar -zxvf teleport-v11.1.2-linux-amd64-bin.tar.gz
```

Install teleport:
```bash
cd teleport
sudo ./install
```

Write config file:
```bash
sudo teleport db configure create \
  --token=39ec2af67c45d8629618dead04459204 \
  --proxy=teleport.shubhamtatvamasi.com:443 \
  --name=mysql \
  --protocol=mysql \
  --uri=172.17.0.2:3306 \
  -o file
```

Start teleport:
```bash
sudo teleport start
```

