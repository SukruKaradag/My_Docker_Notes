## Docker Kurulum

- Docker Ubuntu kurulum

```bash
sudo apt-get update 
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get install -y docker-ce \
                        docker-ce-cli \
                        containerd.io \
                        docker.io
sudo usermod -aG docker ubuntu
newgrp docker
sudo systemctl start docker
sudo systemctl enable docker
```

- Docker AWS Linux kurulum:

```bash
sudo yum update -y
sudo yum install -y docker
sudo usermod -aG docker ec2-user
newgrp docker
sudo systemctl start docker
sudo systemctl enable docker
```
- Docker Compose kurulum

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" \
-o /usr/local/bin/docker-compose
```
- Docker Compose'a executable iznini ver:

```bash
sudo chmod +x /usr/local/bin/docker-compose
```

## Docker Komutları

```bash
docker version

docker info

docker "OPTIONS" inspect "OPTIONS_parametre"

docker run --name "verilen_isim" "image_adı" 

docker container logs "container_id"

docker container run -d -p 80:80 ozgurozturknet/adanzyedocker

docker container rm "id1" "id2" "id3"

docker container exec -it "websunucu" sh

docker container prune

docker image pull -q "image_adı" # "q" stands for quiet. Suppresses the verbose output

docker ps -l  # The "docker ps -l" command displays only the last container to exit.

docker sytem prune  # Makinadaki tüm çalışmayan container, kullanılmayan network, image ve build cache'leri siler.

docker image prune  # Dangling image'ları siler(dangling image means that you've created the new build of the image, but it wasn't given a new name. So the old images you have becomes the "dangling image".)

docker image prune -a # unused ve dangling'leri siler. "image" yerine "container", "network" ve "volume" yazılabilir.

``` 

## Docker notes

- ```docker image pull "image_name"``` komutunu kullandığımızda image orjinal değilse 2 katman iner. İlk katman orjinal image, ikinci katman da ilk imajın üstüne yapılan değişikliğin katmanıdır.

- ```ctrl+p+q``` ile container kapatılmadan çıkılır.

- Default'da açılan portların hepsi TCP olarak açılır, aksi ``` -p 80:80/udp ``` yazılarak belirtilmeli. "-p" parametresi ile sadece bir port belirtilirse externalport otomatik belirlenir.

- ``` -d ve -it beraber -dit olarak da kullanılabilir. Açılan termimal arkaplanda açılır.```
- ````docker cp container:/usr/src/app destination```` Container içinden dosya almak için kullanılır.