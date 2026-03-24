## Adminer (альтернатива phpMyAdmin)

Запуск Adminer для управления БД


Запустите **Adminer** в **Windows Powershell**
```shell
docker run -d `
  --name adminer `
  -p 8084:8080 `
  adminer:latest
```

Запустите **Adminer** в **Git-Bash/Linux/WSL 2.0/Mac**
```shell
docker run -d \
  --name adminer \
  -p 8084:8080 \
  adminer:latest
```

![Работа с Adminer](/photos/Работа%20с%20Adminer%20задание%201%20.png)

[Откройте: http://localhost:8084](http://localhost:8084)

> Без отдельно запущенного контейнера с БД PostgreSQL и связи с ним админ-панель работаеть не будет!

> Заполнять данные админ-панели не нужно!

Система:
- PostgreSQL
- сервер: host.docker.internal
- логин: postgres
- пароль: mysecretpassword

![вход в систему](/photos/Работа%20с%20Adminer%20задание%202%20.png)