
# [nginx-multiple-docker-compose](https://github.com/felipebossolani/nginx-multiple-docker-compose)

Projeto de teste para Proxy Reverso utilizando NGINX com mais de 1 Docker-Compose.
É um teste com propósitos de estudos, portando, não recomendado para uso em produção.

## Pré-Requisitos

[Docker](https://www.docker.com/)

## Utilização

### Docker

Na raiz do projeto execute o comando de criação da network:
```docker
docker network create --driver bridge nginx-network
```

Entre na pasta php_apache e execute o docker compose:
```docker
cd php
docker-compose down -v && docker-compose up --build -d
```
Entre na pasta whoami e execute o docker compose:
```docker
cd ..
cd whoami
docker-compose down -v && docker-compose up --build -d
```
Entre na pasta nginx e execute o docker compose:
```docker
cd ..
cd nginx
docker-compose down -v && docker-compose up --build -d
```

Para verificar os container e as portas execute:

```docker
docker ps -a
```
Algo assim deverá aparecer:
```docker
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
47e32e2aaa27        nginx_proxy         "nginx -g 'daemon of…"   14 hours ago        Up 27 minutes       0.0.0.0:80->80/tcp     nginx_proxy_1
a81e4d5032ba        php_apache          "httpd-foreground"       14 hours ago        Up 33 minutes       0.0.0.0:4000->80/tcp   php_apache
ddbd6e424258        whoami_whoiami      "/whoami"                15 hours ago        Up 2 hours          0.0.0.0:3000->80/tcp   whoami
```

### Acesse

[http://localhost/whoami](http://localhost/whoami)
Para testar um container e:
[http://localhost/php_apache](http://localhost/php_apache)
Para testar o outro.

## Agradecimentos
Ao grupo de telegram [dockerbr](https://t.me/dockerbr). O pessoal sempre ajudando, dando dicas e com muita paciência.
