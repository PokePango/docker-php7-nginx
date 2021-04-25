# Docker PHP7 Nginx

docker-compose.yml example :
```
website:
    build: ./php7-nginx
    restart: unless-stopped
    volumes:
        - ./website/src:/var/www/html
    environment:
        - VIRTUAL_HOST=www.website.com, website.com
        - VIRTUAL_PORT=8080
        - LETSENCRYPT_HOST=www.website.com, website.com
        - LETSENCRYPT_EMAIL=contact@website.com
    ports:
        - 8080:8080
        - 9000:9000
    links:
        - website-db
```

Environment variables are set to use jwilder/nginx-proxy along with Let's Encrypt.

It can be easily linked to a mariadb image:

```
website-db:
    image: mariadb
    restart: unless-stopped
    environment:
        - MYSQL_ROOT_PASSWORD=PASSWORD
        - MYSQL_PASSWORD=PASSWORD
        - MYSQL_DATABASE=DATABASE
        - MYSQL_USER=USER
    volumes:
      - ./website/database:/var/lib/mysql
```