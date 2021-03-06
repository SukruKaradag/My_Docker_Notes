# Dockerfile ile image oluşturma

FROM | Oluşturulacak imajın hangi imajdan oluşturulacağını belirten talimat. Dockerfile içerisinde geçmesi mecburi tek talimat budur. Mutlaka olmalıdır. 
Ör: FROM ubuntu:18.04

LABEL | İmaj metadata’sına key=value şeklinde değer çiftleri eklemek için kullanılır. Örneğin team=development şeklinde bir etiket eklenerek bu imajın development ekibinin kullanması için yaratıldığı belirtilebilir.
Ör: LABEL version:1.0.8

RUN | İmaj oluşturulurken shell’de bir komut çalıştırmak istersek bu talimat kullanılır. Örneğin apt-get install xxx ile xxx isimli uygulamanın bu imaja yüklenmesi sağlanabilir. 
Ör: RUN apt-get update

WORKDIR | cd xxx komutuyla ile istediğimiz klasöre geçmek yerine bu talimat kullanılarak istediğimiz klasöre geçer ve oradan çalışmaya devam ederiz. 
Ör: WORKDIR /usr/src/app

USER | gireceğimiz komutları hangi kullanıcı ile çalıştırmasını istiyorsak bu talimat ile onu seçebiliriz. 
Ör: USER poweruser

COPY | İmaj içine dosya veya klasör kopyalamak için kullanırız
Ör: COPY /source /user/src/app

ADD | COPY ile aynı işi yapar yani dosya ya da klasör kopyalarsınız. Fakat ADD bunun yanında dosya kaynağının bir url olmasına da izin verir. Ayrıca ADD ile kaynak olarak bir .tar dosyası belirtilirse bu dosya imaja .tar olarak sıkıştırılmış haliyle değil de açılarak kopyalanır. 
Ör: ADD https://wordpress.org/latest.tar.gz /temp

ENV | Imaj içinde environment variable tanımlamak için kullanılır
Ör: ENV TEMP_FOLDER="/temp"

ARG | ARG ile de variable tanımlarsınız. Fakat bu variable sadece imaj oluşturulurken yani build aşamasında kullanılır. Imajın oluşturulmuş halinde bu variable bulunmaz. ENV ile imaj oluşturulduktan sonra da imaj içinde olmasını istediğiniz variable tanımlarsınız, ARG ile sadece oluştururken kullanmanız gereken variable tanımlarsınız.
Ör: ARG VERSION:1.0

VOLUME | Imaj içerisinde volume tanımlanamızı sağlayan talimat. Eğer bu volume host sistemde varsa container bunu kullanır. Yoksa yeni volume oluşturur. 
Ör: VOLUME /myvol

EXPOSE | Bu imajdan oluşturulacak containerların hangi portlar üstünden erişilebileceğini yani hangi portların yayınlanacağını bu talimatla belirtirsiniz. 
Ör: EXPOSE 80/tcp

ENTRYPOINT | Bu talimat ile bir containerın çalıştırılabilir bir uygulama gibi ayarlanabilmesini sağlarsınız.
Ör: ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

CMD | Bu imajdan container yaratıldığı zaman varsayılan olarak çalıştırmasını istediğiniz komutu bu talimat ile belirlersiniz. 
Ör: CMD java merhaba

HEALTHCHECK | Bu talimat ile Docker'a bir konteynerin hala çalışıp çalışmadığını kontrol etmesini söylebiliriz. Docker varsayılan olarak container içerisinde çalışan ilk processi izler ve o çalıştığı sürece container çalışmaya devam eder. Fakat process çalışsa bile onun düzgün işlem yapıp yapmadığına bakmaz. HEALTHCHECK ile buna bakabilme imkanına kavuşuruz.
Ör: HEALTHCHECK --interval=5m --timeout=3s CMD curl -f http://localhost/ || exit 1

SHELL | Dockerfile'ın komutları işleyeceği shell'in hangisi olduğunu belirtiriz. Linux için varsayılan shell ["/bin/sh", "-c"],Windows için ["cmd", "/S", "/C"]. Bunları SHELL talimatı ile değiştirebiliriz. 
Ör: SHELL ["powershell", "-command"]
## Dockerfile Notes
- ```FROM``` Dockerfile içinde zorunlu olan tek komuttur. Image'ın hangi Imaj'dan oluşturulucağı belirtilir.
- ```RUN``` Oluşturulucak olan Image'ın Komut satırında çalıştırılmak istenen komut yazılır. Örn.:```RUN apt-get install -y curl```
- ```WORKDIR``` Default olarak çalışılmak istenen istenen path belirtilir. Belirtilen yol yoksa oluşturulur.
- ```COPY``` Image içine kopyalanmas istenen dosya belirtilir. Örn.:```COPY ./deneme.py /home/container/```
- ```EXPOSE``` Image'dan oluşturulacak container'ların hangi portlardan yayın yapacağı belirtilir.
- ```CMD```  Container oluşturulduktan sonra default olarak çalıştırılması istenen komut girilir. ```RUN```'dan farkı ise ```RUN``` Image'ın oluşturulması için gereken bir veya birden fazla komutu kapsarken, ```CMD``` o image'dan yaratılmış olan container'ın içinde default olarak çalışacak komut içindir.
- ```HEALTHCHECK``` Belirtilen parametrelere gör container'ın sağlık durumunu sorgular. Örn.:```HEALTHCHECK --interval=5m --timeout=3s ``` 
- Dockerfile'da yapılan tüm değişiklikler, yapılan değişiklikten sonraki katmanları da etkiler. Öncesi için cache'den işlem yapar.
- ``ADD`` ``COPY``'ile aynı işlemi yapar. Farklı olarak web sunucudan kopyalama yapar. Dosya sıkıştırılmışsa hedefe açarak atar.
- ``ARG`` Dockerfile içinde değişken tanımlamaya yarar. "ARG" build aşamasında kullanılır. "ENV" ``container run`` aşamasında.
  Örn.: 
  ```bash
    # Dockerfile yazılır.
    FROM ubuntu:latest
    WORKDIR /gecici
    ARG VERSION
    ADD https://www.python.org/ftp/python/${VERSION}/Python-${VERSION}.tgz .
    CMD ls -al
    # Built aşamasında "ARG" değeri verilir.
    docker image build -t app:ARG --build-arg VERSION=3.7.1 .
   ```

## Commands
```bash
docker image build -t deneme/merhaba . # Komut Dockerfile'ın olduğu directory'de çalıştırılır.
docker image build -t deneme/merhaba -f "dosya_adı" . # Dockerfile'ın adı farklı ise veya komut Dockerfile'ın oldu directory'de değilse "-f" 
verilerek dosya ve yolu belirtilir.
docker image tag "source_image" "new_image_tag" # Image'a tag vermek için.
```

- docker image history "image name" image'nin katmanları/geçmişini gösterir. 
- ```-t``` ile image'a bir tag verilir.

# Docker commit ile image oluşturma
``docker commit "container_name" "image_name":latest``
``docker commit`` komutunu verirken de Dockerfile komutları girilebilir:
``docker commit -c 'WORKDIR /app/' "container_name" "image_name"`` 
