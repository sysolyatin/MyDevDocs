# Nginx с Let’s Encrypt на Ubuntu

## Установка Certbot

```Bash
sudo apt update && sudo apt upgrade -y
sudo apt install certbot python3-certbot-nginx
```

## Конфигурация Nginx

Все сайты должны быть описаны в своем файле с названием домена, например

```Bash
/etc/nginx/sites-enabled/example.com
```

Пример конфига сайта для проксирования на внутреннее приложение

```Bash
server {
    client_max_body_size 4096M;
    listen 80;
    server_name example.com www.example.com;
    location / {
        proxy_pass http://127.0.0.1:1234/;
        proxy_set_header  Host $host;
        proxy_set_header  X-Real-IP $remote_addr;
        proxy_set_header  X-Forwarded-For $remote_addr;
        proxy_set_header  X-Forwarded-Host $remote_addr;
    }
}
```

Про SSL писать ничего не надо, Certbot допишет всё сам.

После настроек сайта, необходимо рассказать об этом nginx-у

```Bash
sudo nginx -t
sudo systemctl reload nginx
```

## Получение сертификата SSL

```Bash
sudo certbot --nginx -d example.com -d www.example.com
```

## Автообновление сертификатов

Статус службы по автообновлению:

```Bash
sudo systemctl status certbot.timer
```

Список таймеров сертбота

```Bash
sudo systemctl status snap.certbot.renew.timer
```

