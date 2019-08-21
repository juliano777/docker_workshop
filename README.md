**Links Úteis**:

- [GitHub do Curso "Docker Unleashed"- by Gabriel Abdalla](https://github.com/gcavalcante8808/docker-unleashed)
- [Docker Unleashed - Versão Web](https://docker-unleashed.readthedocs.io)

* * *

```bash
docker pull nginx
```

```bash
docker pull debian:buster-slim
```

```bash
docker run -itd -p 80:80 --name teste_nginx --hostname web.dominio nginx
```

```bash
docker top teste_nginx
```

```bash
docker logs teste_nginx
```

```bash
docker stop teste_nginx
```

```bash
docker ps
```

```bash
docker start teste_nginx
```

```bash
docker exec -it teste_nginx bash
```

Ctrl + D para sair


```bash
docker rm -f teste_nginx
```

```bash
mkdir /tmp/nginx
```

```bash
vim /tmp/nginx/index.html
```

```bash
docker run -itd \
    -p 80:80 \
    --name teste_nginx \
    --hostname web.dominio \
    -v /tmp/nginx:/usr/share/nginx/html \
    nginx
```


```bash
docker run -itd \
    -p 0.0.0.0:8000:80 \
    --name teste_nginx \
    --hostname web.dominio \
    -v /tmp/nginx:/usr/share/nginx/html \
    nginx
```


```bash
sudo netstat -nltp | fgrep 8000
```


```bash
sudo iptables -nL | fgrep 80
```

```bash
ifconfig
```

```bash
ifconfig docker0
```

```bash
sudo iptables -t nat -L -n | fgrep 8000
```


```bash
docker search postgres
```


```bash
docker search -f=stars=100 --no-trunc postgres
```


```bash
docker search -f 'stars=100' --no-trunc postgres
```

```bash
docker search postgres_br
```

```bash
docker run -itd \
    -e POSTGRES_DB=db_teste \
    -e POSTGRES_USER=user_teste \
    --name pg \
    --hostname pg.dominio \
    postgres
```

```bash
docker exec -itu postgres \
    pg \
    psql -U user_teste db_teste
```

```bash
docker run -itd \
    --hostname pgbr.dominio \
    --name pgbr \
    juliano777/postgres_br
```

```bash
docker exec -it \
    pgbr \
    bash
```

```bash
whoami
```

```bash
docker run -itd \
    --hostname redis.dominio \
    --name srv_redis \
    redis
```


```bash
docker exec -it srv_redis redis-cli
```

[Try Redis! - https://try.redis.io/](https://try.redis.io/)



[Docker Compose](https://docs.docker.com/compose/)

```bash
sudo wget https://github.com/docker/compose/releases/download/1.24.1/\
docker-compose-Linux-x86_64 -O /usr/local/bin/docker-compose && \
sudo chmod +x /usr/local/bin/docker-compose
```


```bash
mkdir /tmp/odoo ; cd /tmp/odoo
```



```bash
vim docker-compose.yaml
```

```yaml
version: '2'

networks:
    net_odoo:
        driver: bridge

services:

    # Servidor de Aplicação    
    web:
        container_name: odoo_app
        hostname: odoo-app.dominio
        image: odoo:12.0
        depends_on:
            - odoo_db
        environment:
            - HOST=odoo_db
            - PASSWORD=123
            - USER=user_odoo           
        ports:
            - "8069:8069"
        networks:
            - net_odoo

    # Servidor de Banco de Dados
    odoo_db:
        container_name: odoo_db
        hostname: odoo-db.dominio
        image: postgres:12
        environment:
            - POSTGRES_DB=postgres
            - POSTGRES_PASSWORD=123
            - POSTGRES_USER=user_odoo
        networks:
            - net_odoo
```


```bash
docker-compose up -d
```

```bash
docker logs -f odoo_app
```

Control + C

```bash
docker exec -it odoo_db psql -U user_odoo db_odoo
```

```bash
\dt
```

```bash
docker pull opensuse/leap
```

```bash
docker run -itd --name opensuse opensuse/leap
```

```bash
docker ps | fgrep opensuse
```

```bash
docker images | fgrep opensuse
```

```bash
docker rmi opensuse/leap
```


```bash
docker rmi -f opensuse/leap
```


```bash
docker system prune
```

```bash
docker system prune -f
```

```bash
sudo systemctl restart docker
```


```bash
docker run -itd --restart always --name srvonboot centos
```

```bash
docker run -it --rm debian
```


```bash
cat /etc/os-release
```

```bash
docker run -it --rm --name tmpct debian
```

```bash
mkdir /curso-docker
```

```bash
docker commit tmpct imagem_teste:1.0
```

```bash
docker run -it --rm --name tmpct2 imagem_teste:1.0
```

```bash
mkdir /tmp/build ; cd /tmp/build
```

```bash
vim Dockerfile
```

```dockerfile
FROM debian

RUN apt update
RUN apt install -y vim
RUN apt clean
RUN useradd -md /home/foo -s /bin/bash foo

USER foo

CMD '/bin/bash'
```

```bash
docker build --no-cache -t debian_vim:1.0 .
```

```bash
docker tag debian_vim:1.0 debian_vim:latest
```

```bash
docker run -itd --name debian_com_vim --hostname debian-vim.local debian_vim
```

```bash
docker exec -it debian_com_vim bash
```

```bash
echo "Sou o usuário `whoami` e estou no diretório `pwd`"
```

Control + D

```bash
vim Dockerfile
```

```dockerfile
FROM debian

ENV HOME_FOO /home/foo

RUN apt update
RUN apt install -y vim
RUN apt clean
RUN useradd -md ${HOME_FOO} -s /bin/bash foo

USER foo

WORKDIR ${HOME_FOO}

CMD '/bin/bash'
```

```bash
docker build --no-cache -t debian_vim:2.0 .
```

```bash
docker tag debian_vim:2.0 debian_vim:latest
```

```bash
docker run -itd --name debian_com_vim2 --hostname debian-vim.local debian_vim
```

```bash
docker exec -it debian_com_vim2 bash
```

```bash
echo "Sou o usuário `whoami` e estou no diretório `pwd`"
```

```bash
vim Dockerfile
```

```dockerfile
FROM debian

ENV HOME_FOO /home/foo

RUN apt update && \
    apt install -y vim && \
    apt clean && \
    useradd -md ${HOME_FOO} -s /bin/bash foo

USER foo

WORKDIR ${HOME_FOO}

CMD '/bin/bash'
```

```bash
docker build --no-cache -t debian_vim:3.0 .
```

```bash
docker tag debian_vim:3.0 debian_vim:latest
```

```bash
docker images | fgrep vim
```
