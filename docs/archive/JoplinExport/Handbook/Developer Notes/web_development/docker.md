---
title: docker
updated: 2020-09-10 22:07:13Z
created: 2020-09-10 22:07:13Z
---

# Notes for docker
* Not using everyday so need instructions on how I use it
* [Removing Docker containers and images](https://zaiste.net/posts/removing_docker_containers/)
* Reset containers when using docker-compose. `docker-compose up --force-recreate`
* Reset everything - `docker-compose down --remove-orphans -v --rmi all`
* **ElasticSearch**
    * ElasticSearch Docker Images - `https://www.docker.elastic.co`
    * Use oss images - [Pulling images](https://www.elastic.co/guide/en/kibana/current/_pulling_the_image.html)
    * [Kibana Docker](https://www.elastic.co/guide/en/kibana/current/_configuring_kibana_on_docker.html) - Configure Kibana for docker.
        * [Docker Kibana](https://docs.docker.com/samples/library/kibana/#-via-docker-stack-deploy-or-docker-compose)

## Starting and using
* Now using Docker for Mac
1. ~~`docker-machine start default`~~
1. ~~Set the environment~~
    * ~~Configure Shell (Docker Toolbox on Mac)~~
        * ~~`eval "$(docker-machine env default)"`~~
1. ~~`docker-machine config` - verify can connect and pull info from the machine~~

## Use a base alpine image for docker
* [Official Alpine Docker Image](https://hub.docker.com/_/alpine/)
* [Docker Networking](https://docs.docker.com/compose/networking/)
* [Docker Store](https://store.docker.com/images/alpine)
  * `docker pull alpine`
  * `apk --no-cache add {package}`
  * Dockerfile Example - avoids using *--update* and *rm -rf /var/cache/apk/\**
```yaml
  FROM alpine:latest
  RUN apk add --no-cache nginx
  EXPOSE 80
  CMD ["nginx", "-g", "daemon off;"]
```
## Nginx docker config
* `sudo docker cp docker-nginx:/etc/nginx/conf.d/default.conf default.conf` - *Copy config file from docker container*

## Setup nginx-unit with docker
* [yousan/nginx-unit](https://github.com/yousan/nginx-unit/blob/master/docker-compose.yml) - instructions on getting access to the socket.
* [Nginx Unit Integration](https://unit.nginx.org/integration/)
* []()
* **docker-compose.yml**
```yaml
version: '3'
services:
  web:
    image: "nginx:1.13-alpine"
    container_name: lookfindme-web
    ports:
      - "7000:80"
    volumes:
      - ./containers/nginx/html:/usr/share/nginx/html:ro
      - ./containers/nginx/conf/nginx.conf:/etc/nginx/nginx.conf
      - ./containers/nginx/conf/default.conf:/etc/nginx/conf.d/default.conf
  nginx-unit:
    image: "nginx/unit:1.1-full"
    container_name: lookfindme-nginx-unit
    ports:
      - 8081:8081
      - 8200:8200
      - 8300:8300
    volumes:
      - ./containers/nginx/json:/root/json
      - ./containers/nginx/www/root:/www/root
  database:
    image: "mdillon/postgis:10-alpine"
    container_name: lookfindme-database
    ports:
      - "15432:5432"
    volumes:
      - ./containers/dbData:/var/lib/postgresql/data
  search:
    image: "docker.elastic.co/elasticsearch/elasticsearch-oss:6.2.3"
    container_name: lookfindme-search
    ports:
      - "9200:9200"
      - "9300:9300"
  queue:
    image: "rabbitmq:3-management-alpine"
    container_name: lookfindme-queue
    ports:
      - "15672:15672"
    volumes:
      - ./containers/queue:/var/lib/rabbitmq
```
* container folder. - *containers/nginx/conf/*
    * *default.conf*

```conf
server {
    listen       80;
    server_name  localhost;

    #charset koi8-r;
    #access_log  /var/log/nginx/host.access.log  main;

    location /static {
        root /usr/share/nginx;
    }

   location / {
        proxy_pass http://unit_backend;
        proxy_set_header Host $host;
    }

    location /home {
        # uswgi_pass lookfindme;
        # include uwsgi_params;
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

    # proxy the PHP scripts to Apache listening on 127.0.0.1:80
    #
    #location ~ \.php$ {
    #    proxy_pass   http://127.0.0.1;
    #}

    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    #
    #location ~ \.php$ {
    #    root           html;
    #    fastcgi_pass   127.0.0.1:9000;
    #    fastcgi_index  index.php;
    #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
    #    include        fastcgi_params;
    #}

    # deny access to .htaccess files, if Apache's document root
    # concurs with nginx's one
    #
    #location ~ /\.ht {
    #    deny  all;
    #}
}
```
* nginx.conf
```conf
user  nginx;
worker_processes  1;

error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}



http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    upstream unit_backend {
        server nginx-unit:8300;
    }

    include /etc/nginx/conf.d/*.conf;
}
```

* nginx-unit json file
```json
{
	"listeners": {
			"*:8300": {
					"application": "blogs"
			}
	},

	"applications": {
			"blogs": {
					"type": "php",
					"processes": 20,
					"root": "/www/root",
					"index": "index.php"
			}
	}
}
```
* `docker-compose exec nginx-unit curl -X PUT -d @/root/json/local.json --unix-socket /var/run/control.unit.sock http://localhost/ && docket-compose exec nginx-unit /bin/bash`


## Setup nginx-unit with docker
* Using *Docker for Mac*
    * [Docker Nginx Unit](https://hub.docker.com/r/nginx/unit/)
* Using *docker-compose.yml*
```yml
  nginx-unit:
    image: "nginx/unit:1.1-full"
    container_name: nginx-unit
    ports:
      - 8081:8081
      - 8200:8200
      - 8300:8300
    volumes:
      - ../containers/nginx/json:/root/json
      - ../containers/nginx/www/root:/www/root
```
* Create *index.php* in ./containers/nginx/html
* *json.local* in ./containers/nginx/json
```json
{
	"listeners": {
			"*:8300": {
					"application": "blogs"
			}
	},

	"applications": {
			"blogs": {
					"type": "php",
					"processes": 20,
					"root": "/www/root",
					"index": "index.php"
			}
	}
}
```

## Creating the setup
* Create configuration in *docker-compose.yml* file
* Copy *json.local* to *containers/nginx/json*
* Copy *index.php* to *containers/nginx/www/root*
* `docker-compose up -d` - start the containers
* `docker-compose exec nginx-unit curl -X PUT -d @/root/json/local.json --unix-socket /var/run/control.unit.sock http://localhost/` - set the configuration for nginx unit
* Access the file at *http://localhost:8300*

## Errors
* **ERROR: network lookfindmeapi_default id ae6c919c63c2f8a9ed5a5aea2ba716f4b19efe4fd7599fc0262a991d6e34b494 has active endpoints**
    * `docker-compose ps`
    * `docker stop {container}`
    * `docker container prune`
