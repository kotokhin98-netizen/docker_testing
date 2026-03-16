## Тест скорости интернета в docker

1. Speedtest в Docker
```shell
docker run -d -p 158:80 --name speedtest-server adolfintel/speedtest
```

[Открыть в браузере http://localhost:158/](http://localhost:158/)

![Используем код](/photos/код%20для%20проверки%20интернета.png)
![проверяем скорость](/photos/проверка%20интернета%20.png)