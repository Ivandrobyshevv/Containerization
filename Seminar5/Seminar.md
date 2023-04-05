**Задание:** Создать Docker Compose файл, который бы запускал 2 контейнера. Повтор примера лекции для лучшего понимания процесса

[docker-compose.yml](./docker-compose.yml)

```
docker-compose up -d  
docker ps -a

CONTAINER ID   IMAGE              COMMAND                  CREATED         STATUS         PORTS                  NAMES
e7a837126fe9   phpmyadmin:5.2.1   "/docker-entrypoint.…"   7 seconds ago   Up 6 seconds   0.0.0.0:8081->80/tcp   seminar5-adminer-1
53dc89a4d37c   mariadb:10.11.2    "docker-entrypoint.s…"   8 minutes ago   Up 8 minutes   3306/tcp               seminar5-mariadb-1
```

**Задание:**
Создать свой кластер из нод докера. Сделать так, чтобы каждая нода могла управлять кластером (была лидером). Также необходимо добавить каждой ноде по метке: prod, stage, lab. Проверить и убедиться, что метки действительно добавились.

```
root@docker-server1:~# docker swarm init
root@docker-server2:~# docker swarm join --token SWMTKN-1-1d2370jlss4cxk21ik6ex4rcuxr8kg41p2b47nsd5dm69skzp9-0khj0mw21733z3pta0uout8m7 192.168.0.108:2377
root@docker-server1:~# docker node ls
ID                            HOSTNAME         STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
524w3cmj3z24szk98hch0odxo *   docker-server1   Ready     Active         Leader           23.0.2
uhq531uixaxp9roxh3m8wqub2     docker-server2   Ready     Active                          23.0.2

docker node update --label-add env=prod docker-1
root@docker-server1:~# docker node inspect docker-server2
"Spec": {
            "Labels": {
                "env": "prod"
            },
            "Role": "worker",
            "Availability": "active"
        }
```
