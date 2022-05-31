## Commands

```bash
# Swarm'ı aktive etmek için:
docker swarm init --advertise-addr 172.31.21.200 

# Manager token'ını almak için:
docker swarm join-token manager 

# Worker token'ını almak için:
docker swarm join-token worker

# Örnek bir container oluşturma komutu:
docker service create --name test --replicas=5 -p 8080:80 nginx

docker service rm "service_name"

```
### Scaling

``docker service scale test=3``

### Update and Rollback

```bash
docker service update --detach -- update-delay 5s --update-parallelism 2 --image ozgurozturknet/web:v2 websrv # update edilir.

docker service rollback --detach websrv ## update geri alınır.
```

## Secret
docker create secret "name" "./file_name"
or
echo "password" | docker secret create "secret_name" -

- secret'lar container içindeki "/run/secrets" directory'sindedir.

docker service update --secret-rm "old_secret" --secret-add "new_secret" "secret_name" "service_name"

## Swarm notes
- Ports:
    2377/TCP        Cluster yönetimi için
    7946/TCP-UDP    Node'lar arası iletişim
    4789/UDP        Overlay Network

- İletişim etcd ile şifrelenmiştir.
- Manager sayısı her zaman 1, 3, 5 ,7 ... şeklinde tek sayı olarak ilerler.
- ideal Manager sayısı 3 olmakla birlikte, 7 Manager'den sonrası sağlıksızdır.
- Kubernetes'in aksine defaul'da Manager'ler da worker görevi görür
- Overlay Network'ler ile aynı ağda olmayan makineler aynı service'e alınabilir. 
- Default'da ingress Overlay network kullanılır.