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

# get pool a and b running, linking the ports to the host
docker run -d -e "POOL=a" -e "PORT=8080" --name=a -p 8080:80 registry.docker.codepen.io/tsabat/service:0.1
docker run -d -e "POOL=b" -e "PORT=8081" --name=b -p 8081:80 registry.docker.codepen.io/tsabat/service:0.1

HOST=$(ip route show | grep docker0 | awk '{print $9}')
docker run -d -p 9000:80 -e="HOST_ADDRESS=$HOST" registry.docker.codepen.io/tsabat/nginx_balance:0.1
