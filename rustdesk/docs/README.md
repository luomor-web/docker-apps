```shell
# https://rustdesk.com/docs/en/self-host/rustdesk-server-oss/docker/
sudo docker image pull rustdesk/rustdesk-server
sudo docker run --name hbbs -v `pwd`:/root -td --net=host rustdesk/rustdesk-server hbbs -r <relay-server-ip[:port]>
sudo docker run --name hbbr -v `pwd`:/root -td --net=host rustdesk/rustdesk-server hbbr

# TCP (21115, 21116, 21117, 21118, 21119)
# UDP (21116)

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