# Docker

## cheat
```
$ docker exec -it CONTAINER bash
```

## 이미 실행중인 컨테이너 port 수정
```
# image 를 중간중간 저장해둬야 특정 시점으로 빠른 복구 가능
$ docker commit CONTAINER IMAGE_NAME
$ docker images
```

### redis
```shell script
$ docker pull redis

$ docker run --name some-redis -d -p 6379:6379 redis

# redis-cli 필요 시 
$ docker network create redis-net
$ docker run --name some-redis -p 6379:6379 --network redis-net -d redis redis-server --appendonly yes

// cli
$ docker run -it --network redis-net --rm redis redis-cli -h some-redis
```
