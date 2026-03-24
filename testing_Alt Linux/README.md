## Alt Linux в Docker


#### Использовать контейнер с Alt

##### Загрузить готовый образ Alt
```shell
docker pull alt:sisyphus
```

##### Запустить и использовать
```shell
docker run -ti --rm --name alt alt:sisyphus /bin/bash
```
![Запуск](/photos/запуск%20Alt%20Linux%20.png)

#### Установить приложение Fastfetch в контейнере
```shell
apt-get update && apt-get install fastfetch
```

#### Запустить Fastfetch
```shell
fastfetch
```

![Запуск Fastfetch](/photos/Установить%20приложение%20Fastfetch%20в%20контейнере.png)
##### Выйти из контейнера с Alt
```shell
exit
```

### Полезные ссылки

[alt Docker Official Image](https://hub.docker.com/_/alt/)

[Dockerfile](https://github.com/alt-cloud/docker-brew-alt/blob/p10/x86_64/Dockerfile)

[Docker Alt Linux Image](https://github.com/sibsau/docker-alt/blob/master/README.md)

> Если вы обнаружили ошибку в этом тексте - сообщите пожалуйста автору!