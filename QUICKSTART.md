# Быстрый старт

- Установить Docker
- `git clone https://github.com/suiljex/CTFd`
- Создайте `.ctfd_secret_key` в корне CTFd

  ``` bash
  head -c 64 /dev/urandom > .ctfd_secret_key
  ```

- Отредактируйте `./conf/nginx/https.conf`

  Укажите нужные доменные имена в параметре `server_name`

- Отредактируйте `docker-compose.yml`

  Укажите нужный email в

  ``` yaml
  nginx:
      environment:
        - CERTBOT_EMAIL=your@email.org
  ```

- `docker-compose up --build --detach`
- `docker-compose down`

## Может пригодиться

- Проверка работы certbot'а

  ``` shell
  docker run -it -p 80:80 -p 443:443 --env CERTBOT_EMAIL=your@email.org --env STAGING=1 --env DEBUG=1 -v /<absolute_path_to_CTFd_folder>/conf/nginx/https.conf:/etc/nginx/user_conf.d/https.conf jonasal/nginx-certbot:latest
  ```

- Все данные хранятся в `./.data`
