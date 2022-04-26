## Volume Commands
```bash
docker volume create "volume_name"
docker volume inspect "volume_name"
docker container run -it -v volume_name:/uygulama alpine sh
docker container run -it -v volume_name:/uygulama:ro alpine sh #"ro" stands for read only. you can't chance anything in this volume.
docker container run --rm -it ozgurozturknet/adanzyedocker sh  #"rm" command will delete container when you stop it.
```
## Volume Notes

- Eğer bir volume mount edildiği klasör mevcut değilse bu klasörü yaratır.
Ve o anda volume içerisinde hangi dosyalar varsa bu klasörde de o
dosyaları görürsünüz. Boşsa boş görürsünüz.
- Eğer bir volume imaj içerisinde bulunan mevcut bir klasöre mount edilirse:
A: Klasör boşsa o anda volume içerisinde hangi dosyalar varsa bu klasörde de
o doşyaları görürsünüz.
B: Klasörde dosya varsa ve volume boşsa bu sefer o klasördeki dosyalar
volume'e kopyalanır.
C: Klasörde dosya var ya da yok fakat volume'de dosyalar varsa yani volume
boş değilse, bu sefer siz o klasörün içerisinde volume'de ne dosya varsa onu
görürsünüz.

### Bind Mount
 bind mount local'deki bir directory'yi container'a mount etmeyi sağlar. Devolopment yaparken kullanılır.

 örn.:
 ```bash 
 docker container run -d -p 80:80 -v "local_directory:container_mount_point" nginx # while creating a bind mount use the "-v" parameter just like volumes.
 ```