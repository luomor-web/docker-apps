```shell
 sudo docker network create \
   --driver=bridge  \
   --subnet=192.168.254.0/29 RSBackend

 sudo docker network create \
   --driver=ipvlan --subnet=192.168.1.0/24 \
   --gateway=192.168.1.1 \
   -o ipvlan_mode=l2 \
   -o parent=eth0 DMZ

```