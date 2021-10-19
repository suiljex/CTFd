# Краткая инструкция как поднять CTFd с HTTPS

## Поправьте `./conf/nginx/https.conf`

- Укажите в `server_name` нужные домены

## Поправьте `docker-compose.yml`

- Укажите нужный email в
``` yaml 
nginx:
    environment:
      - CERTBOT_EMAIL=your@email.org
```

## Проверьте работу certbot'а

``` shell
docker run -it -p 80:80 -p 443:443 --env CERTBOT_EMAIL=your@email.org --env STAGING=1 --env DEBUG=1 -v /<absolute_path_to_CTFd_folder>/conf/nginx/https.conf:/etc/nginx/user_conf.d/https.conf jonasal/nginx-certbot:latest
```

## Создайте `.ctfd_secret_key`

```
head -c 64 /dev/urandom > .ctfd_secret_key
```

## Запустите

```
docker-compose up -d --build
```