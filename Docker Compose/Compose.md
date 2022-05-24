## Installation
- curl ile compose dosyasını indir:
``DOCKER_CONFIG=${DOCKER_CONFIG:-$HOME/.docker}``
``mkdir -p $DOCKER_CONFIG/cli-plugins``
```curl -SL https://github.com/docker/compose/releases/download/v2.5.0/docker-compose-linux-x86_64 -o $DOCKER_CONFIG/cli-plugins/docker-compose```

- Dosyayı executable yap:
```chmod +x $DOCKER_CONFIG/cli-plugins/docker-compose```

- Version check:
``docker compose version``

## Notes
- version-2'de hyphen(-) yerine 'space' verilebilir. Örn.: "``docker-compose`` ``docker compose``"
- Oluşturulan servisler "bulunduğu-klasörün-adı_Verilen-ad" şeklinde adlanır. 


## Commands
```bash
docker compose up -d 
docker compose down # oluşan tüm servisler silinir.
docker compose build # compose aşamasında Dockerfile ile image oluşturulduysa "docker compose up" tekrarlandığında hali hazırda yarılmış olan image kullanılır. Dolayısıyla yapılan değişiklikler image'da olmaz. Bunun için bu komut girilerek image yeniden oluşturulur. 
```