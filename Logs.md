## Log Commands
``` bash
docker logs "container_name"
docker logs --details "container_name" # Daha çok detay için.
docker logs -t "container_name"  # Zaman detayı için.
docker logs --help
docker logs --until "log_time" "container_name" # Belirtilen zamana kadar oluşan loglar listelenir.
docker logs --since "log_time" "container_name" # Belirtilen zamandan itibaren oluşan loglar listelenir.
docker logs --tail "tail_number" "container_name" # Belirtilen sayıya göre son loglar listelenir.
docker logs -f "container_name"  # Gerçek zamanlı takip(-f) edilir.
docker container run --log-driver "logging_driver" "image" # Container belirtilen logging driver ile çalışır.
```

## Log Notes

- loglar ```/dev/fd/``` altındaki stdin, stdout ve stderr'den alınır.
- ```-f``` stands for follow.
- Default logging driver "json-file" dır. Docker awslogs, fluentd, gcplogs, gelf, journald, json-file, local, logentries, splunk ve syslog driver'larını da destekler. İstenilen driver default olarak seçilebilir.