# Установка через Docker Compose

```yaml
version: "2.1"

services:
  nextcloud:
    image: nextcloud:23.0.1-apache
    container_name: nextcloud-23
    environment:
      - TZ=Europe/Moscow
    volumes:
      - ./nextcloud/apps:/var/www/html/apps
      - ./nextcloud/custom_apps:/var/www/html/custom_apps
      - ./nextcloud/config:/var/www/html/config
      - ./nextcloud/data:/var/www/html/data
    ports:
      - 13360:80
    restart: unless-stopped
    depends_on:
      - postgres-nextcloud

  postgres-nextcloud:
    image: postgres:14.1-alpine
    container_name: postgres-nextcloud
    restart: unless-stopped
    environment:
      - POSTGRES_DB=nextcloud
      - POSTGRES_USER=nextcloud
      - POSTGRES_PASSWORD=12345
    volumes:
      - ./DB:/var/lib/postgresql/data
```