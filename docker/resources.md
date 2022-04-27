## Commands
```bash
docker tap "container_name" # Belirtilen container içindeki process'leri listeler

docker stats "container_name" # Belirtilen container'ın kaynak kullanımını gerçek zamanlı olarak listeler. Komutta container belirtilmez ise çalışan tüm container'ler listelenir.

docker container run -d --memory=100m "container_name" # Ram sınırlandırmak için. (megabayt=m, gigabayt=g, kilobayt=k)

docker container run -d --memory=100m --memory-swap=100m "container_name" # Ram Swap miktarı için.

docker container run -d --cpus="1.5" "container_name" # CPU sınırlandırmak için.

docker container run -d --cpus="2" --cpuset-cpus="0,3" "container_name" # Kullanılması istenilen CPU core'ları belirtmek için.
```

