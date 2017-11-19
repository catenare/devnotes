# Notes for docker
* Not using everyday so need instructions on how I use it
*[Removing Docker containers and images](https://zaiste.net/posts/removing_docker_containers/)
## Starting and using
1. ~~`docker-machine start default`~~
1. ~~Set the environment~~
    * ~~Configure Shell (Docker Toolbox on Mac)~~
        * ~~`eval "$(docker-machine env default)"`~~
1. ~~`docker-machine config` - verify can connect and pull info from the machine~~

## Use a base alpine image for docker
* [Official Alpine Docker Image](https://hub.docker.com/_/alpine/)
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
