# Multi-stage Build
- Image oluşturma işlemi sırasında birden fazla image oluşturulabilir ve bunlar arasında etkileşim sağlanabilir. Buna "Multi-stage Build" denir.
 Aşağıda verilen örnekte bir Dockerfile'dan iki image(stage) oluşturulmuştur. İlk stage'de Java source code'u build(compile) edilmiş, ikinci stage'de ise bu build çekilip yeni bir image oluşuturulmuştur.

```bash
# Java code'unun Build işlemi için jdk imajından base image oluşturuluyor
FROM mcr.microsoft.com/java/jdk:8-zulu-alpine AS derleyici
# Working directory seçiliyor.
WORKDIR /usr/src/uygulama
# W.D. içine java kaynak kodu atılıyor. 
COPY /source /usr/src/uygulama 
# Java kaynak code'u build ediliyor.
RUN javac uygulama.java

# jre base image seçiliyor.
FROM mcr.microsoft.com/java/jre:8-zulu-alpine
WORKDIR /uygulama
# derleyici ismi verilen build stage'inde oluşturulmuş olan build edilmiş code, yeni stage'e alınıyor.
COPY --from=derleyici /usr/src/uygulama .
CMD ["java", "uygulama"]
```