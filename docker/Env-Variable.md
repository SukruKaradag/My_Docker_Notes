## Comands

```bash
docker container run -it --env Var1=deneme1 ubuntu sh #her variable için --env ya da -e paremetresi ayrı ayrı verilmeli
docker container run -it --env TEMP ubuntu sh # Host'dan variable aktarmak için.

```

## Nots
- Environment variable'lar case sensitive'dir.
- Host'un Environment'ları da container'a aktarılabilir. ``` --env "buraya host'daki variable'nın adı." ```
- Çoklu variable tanımla için ```--env-file "file_name_path"``` kullanılabilir.