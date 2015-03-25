# load_balanced_docker
example of how to load balance a docker container

based on this article.

https://www.codeschool.com/blog/2015/01/16/production-deployment-docker/

## Setup

```
cd nginx
docker build -t registry.docker.codepen.io/tsabat/nginx_balance:0.1 .
cd ../service
docker build -t registry.docker.codepen.io/tsabat/service:0.1 .

docker run -d -e "POOL=a" -e "PORT=8080" --name=a --expose=8080 registry.docker.codepen.io/tsabat/service:0.1
docker run -d -e "POOL=a" -e "PORT=8081" --name=b --expose=8081 registry.docker.codepen.io/tsabat/service:0.1

docker run -d --link=a:pool_a --link=b:pool_b registry.docker.codepen.io/tsabat/nginx_balance
```
