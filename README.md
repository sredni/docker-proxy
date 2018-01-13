# Docker proxy
Docker proxy project to keep out of local nginx proxy (made especially for macOS)

## Installation
```
git clone https://github.com/sredni/docker-proxy.git
cd docker-proxy
```
create your proxy configs in `conf.d/`
```
docker network create global
docker-compose up -d
```
## Tips
Attach new containers to network called `global`, 
this will simplify your configs by providing container name instead of hardtyped ips. 
For example:
- using docker-compose:
```
version: '3'

services:
  web:
    container_name: web
    ...
    
networks: 
  default:
    external:
      name: global
```
- using docker run:
```
docker run -itd --network=global --name web busybox
```
Then in nginx configs you can use:
```
proxy_pass http://web;
```
