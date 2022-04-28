## Commads
```bash
docker network inspect "network_name"
docker container run -it --name deneme1 --net host ozgurozturknet/adanzyedocker sh # "--net" ile bağlanılacak network'ü seçtik.
docker network create --driver=host "network_name" # Network türü belirtilmezse network default'da bridge oluşur.
docker network create --driver=bridge --subnet=10.10.0.0/16 --ip-range=10.10.10.0/24 --gateway=10.10.10.10 "network_name"
docker network connect "network_name" "container_name_or_id"    # Container'ı network'e bağlamak için.
docker network disconnect "network_name" "container_name_or_id" # Container'ı network'den disconnect etmek için.
```
## Notes
- Aynı network'e bağlı tüm container'lar birbirlerinin ismini çözebilirler. Kullanıcı tanımlı bridge'lerde DNS hizmeti bulunur.
- Varsayılan dışında ip aralıkları tanımlanabilir.
- Containerlar çalışır durumdayken de kullanıcı tanımlı bridge networklere bağlanıp, bağlantıyı kesebilirler.
- Containerlar arası network izolasyonu sağlamak istersek ayrı bridge networkler yaratarak bunu sağlayabiliriz.
- Oluşturulan Network'ün subnet, ip range ve gateway'i belirtilebilir:
```docker network create --driver=bridge --subnet=10.10.0.0/16 --ip-range=10.10.10.0/24 --gateway=10.10.10.10 "network_name"```
- Kullanıcı tanımlı bridge network'lere bağlı olan bir container başka bir network'e bağlabilir. Container default bridge'e bağlıysa bu işlem gerçekleşmez.
- Container'a bağlı olan bir network silinemez.("-f" dahil) Containerların silinmesi veya durdurulması gerekir. Network silme işlemi bağlı olan container'ların durdurulması yolu ile gerçekleştiyse, o container'lar tekrar start edilemez ve başka bir network'e bağlatılamaz. Network ID kullanılarak aynı network yaratılırsa container tekrar çalışabilir.
