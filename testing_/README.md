## Pcb2gcode web application wrapper


### Создаём папку для данных (если её нет)

#### Для Git-Bash/Linux/macOS:

```shell
mkdir -p ~/insolante_data
```

#### Для Windows (PowerShell):

Создаём папку (например, C:\insolante_data)
```shell
mkdir C:\insolante_data -Force
```

Загружаем образ, создаём и запускаем контейнер:

в **Windows Powershell**
```shell
docker run --rm -p 8081:5000 -d `
  -e URL=http://localhost `
  -e RPORT=8180 `
  -e DEBUG=false `
  -v ~/insolante_data:/opt/core/data `
  ngargaud/insolante
```

в **Git-Bash/Linux/WSL 2.0/Mac**
```shell
docker run --rm -p 8081:5000 -d \
  -e URL=http://localhost \
  -e RPORT=8180 \
  -e DEBUG=false \
  -v ~/insolante_data:/opt/core/data \
  ngargaud/insolante
```
![Запуск](/photos/запуск%20Pcb2gcode%20.png)

[Открыть проект в браузере http://localhost:8081](http://localhost:8081)

Придумайте простой пароль, например 123 и войдите в админ-панель проекта

[Docker-версия Pcb2gcode](https://hub.docker.com/r/ngargaud/insolante)`

![Запуск сайта](/photos/Сайт%20Pcb2gcode.png)