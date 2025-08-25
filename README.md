# Как запускать
После написания nginx.conf для запуска выполните команду
```
docker compose up --build --remove-orphans
```

# Как тестировать

## Login
Получить токен
```
curl -X POST -H "Content-Type: application/json" -d '{"login":"bob","password":"qwe123"}' http://localhost/v1/token
```
Пример
```
$ curl -X POST -H "Content-Type: application/json" -d '{"login":"bob","password":"qwe123"}' http://localhost/v1/token
{"token":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJib2IifQ.-51G5JQmpJleARHp8rIljBczPFanWT93d_N_7LQGUXU"}
```

## Test
Использовать полученный токен для загрузки картинки
```
curl -X POST -H 'Authorization: Bearer <TODO: INSERT TOKEN>' -H 'Content-Type: octet/stream' --data-binary @1.jpg http://localhost/upload
```
Пример
```
$ curl -X POST -H 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJib2IifQ.hiMVLmssoTsy1MqbmIoviDeFPvo-nCd92d4UFiN2O2I' -H 'Content-Type: octet/stream' --data-binary @1.jpg http://localhost/upload
{"filename":"c31e9789-3fab-4689-aa67-e7ac2684fb0e.jpg"}
```

 ## Проверить
Загрузить картинку и проверить что она открывается
```
curl localhost/image/<filnename> > <filnename>
```
Example
```
$ curl localhost/images/c31e9789-3fab-4689-aa67-e7ac2684fb0e.jpg > c31e9789-3fab-4689-aa67-e7ac2684fb0e.jpg
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 13027  100 13027    0     0   706k      0 --:--:-- --:--:-- --:--:--  748k

$ ls
c31e9789-3fab-4689-aa67-e7ac2684fb0e.jpg
```

server.py скрипт реализует:
1. Flask‑веб‑сервер с REST API.  
2. Метрики для Prometheus.  
3. Авторизацию по логину/паролю с хранением паролей в хэшированном виде (pbkdf2_sha256).  
4. Выдачу и валидацию JWT токенов.  
5. Простейший healthcheck.

server.js

Этот Node.js скрипт запускает веб-сервер на Express, который служит для приёма загрузки изображений и сохранения их в хранилище совместимое с S3 (MinIO), а также собирает метрики Prometheus.

Этот скрипт — **сервис для загрузки изображений** с проверкой MIME-типов, сохранением файлов в S3-совместимом хранилище (MinIO) и встроенной поддержкой метрик Prometheus, который можно использовать для мониторинга производительности и состояния.  

Он полезен, если нужно принимать и хранить изображения с валидацией, а также отслеживать метрики запросов и нагрузки.  

Если нужно, могу помочь с расширением или детальной настройкой его частей!