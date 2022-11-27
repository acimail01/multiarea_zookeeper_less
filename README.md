```bash
sudo tee -a /etc/hosts > /dev/null <<EOT
192.168.94.131  kafka1 kafka1.lan broker1.lan
192.168.94.132  kafka2 kafka2.lan broker2.lan
192.168.94.133  kafka3 kafka3.lan broker3.lan
EOT
```

```bash

#docker exec -it kafka kafka-topics --bootstrap-server localhost:9092       --replication-factor 1 --partitions 1 --create --topic topic01
docker exec -it kafka kafka-topics --bootstrap-server localhost:9193       --replication-factor 1 --partitions 1 --create --topic topic01
docker exec -it kafka kafka-topics --bootstrap-server kafka:9092           --replication-factor 1 --partitions 1 --create --topic topic02
docker exec -it kafka kafka-topics --bootstrap-server kafka1.lan:9092      --replication-factor 1 --partitions 1 --create --topic topic03
docker exec -it kafka kafka-topics --bootstrap-server 192.168.94.131:9092  --replication-factor 1 --partitions 1 --create --topic topic04
docker exec -it kafka kafka-topics --bootstrap-server kafka3.lan:9092      --replication-factor 1 --partitions 1 --create --topic topic05

docker exec -it kafka kafka-topics --bootstrap-server 192.168.94.131:9092,192.168.94.132:9092,192.168.94.133:9092         --replication-factor 2 --partitions 5 --create --topic topic07
docker exec -it kafka kafka-topics --bootstrap-server localhost:9092,broker1.lan:9092,broker2.lan:9092,broker3.lan:9092   --replication-factor 2 --partitions 5 --create --topic topic08

```
