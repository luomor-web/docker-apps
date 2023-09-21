```shell
# https://rustdesk.com/docs/en/self-host/rustdesk-server-oss/docker/
sudo docker image pull rustdesk/rustdesk-server
sudo docker run --name hbbs -v `pwd`:/root -td --net=host rustdesk/rustdesk-server hbbs -r <relay-server-ip[:port]>
sudo docker run --name hbbr -v `pwd`:/root -td --net=host rustdesk/rustdesk-server hbbr

# TCP (21115, 21116, 21117, 21118, 21119)
# UDP (21116)
docker logs hbbs

# rustdesk docker-compose
sudo docker pull rustdesk/rustdesk-server:1.1.8-2
sudo docker-compose up -d
sudo docker-compose down
sudo docker-compose ps
sudo docker-compose logs -f

sudo docker-compose stop hbbs
sudo docker-compose start hbbs

netstat -tlnp

# server pro
sudo docker network create \
   --driver=bridge  \
   --subnet=192.168.254.0/29 RSBackend

sudo docker network create \
   --driver=ipvlan --subnet=192.168.1.0/24 \
   --gateway=192.168.1.1 \
   -o ipvlan_mode=l2 \
   -o parent=eth0 DMZ
```

```shell
docker run --name hbbr -p 21117:21117 -p 21119:21119 -v pwd:/root -it --net=host thtom/rustdesk-server hbbr
docker run --name hbbs -p 21115:21115 -p 21116:21116 -p 21116:21116/udp -p 21118:21118 -v pwd:/root -it --net=host thtom/rustdesk-server hbbs
```