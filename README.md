# Parity POA
Parity PoA integration test

## Initialization
- build `parity` docker image (`docker.parity` is expected)
```
docker build -t docker.parity -f .travis.dockerfile .
```

- build `contract` docker image (`docker.contract` is expected)
```
cd contract
docker build -t docker.contract .
```

- or modify [docker-compose.yml](https://github.com/illya13/parity-poa/blob/master/docker-compose.yml)

## Run test

```
docker-compose up -d mach1 mach2 mach3 mach4 gateway
docker-compose logs --tail 100
docker-compose run contract node deploy.js
docker-compose run contract node main.js
docker-compose stop mach1 mach2 mach3 mach4 gateway
docker-compose logs --tail 100 mach1
docker-compose logs --tail 100 mach2
docker-compose logs --tail 100 mach3
docker-compose logs --tail 100 mach4
docker-compose logs --tail 100 gateway
docker-compose rm -f
```
