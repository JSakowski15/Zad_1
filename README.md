<h1>Technologie chmurowe - Zadanie 1</h1>

Jakub Sakowski

# Część 1 (Obowiązkowa)
## 1.1


## 1.2

``` Dockerfile
# syntax=docker/dockerfile:1.4

FROM  node:alpine3.16 as build-stage 

ARG VERSION

WORKDIR /app 

ENV REACT_APP_VERSION=${VERSION}

COPY package*.json /app/ 

RUN npm install axios && npm install && rm -rf $npm_config_cache && npm cache clean --force

COPY . . 

RUN npm run build


FROM nginx:1.23.4-alpine

ARG VERSION

LABEL org.opencontainers.image.version="$VERSION"
LABEL org.opencontainers.image.authors="Jakub Sakowski"

COPY nginx.conf /etc/nginx/conf.d/default.conf 

COPY --from=build-stage /app/build /usr/share/nginx/html 

EXPOSE 8080

HEALTHCHECK --interval=10s --timeout=1s \
    CMD curl -f http://localhost:8080/ || exit 1

CMD ["nginx", "-g", "daemon off;"]

```

## 1.3

```shell
docker build --build-arg VERSION=1.1 -t tchzad1:v1 .
```


```shell
docker run -d -p 8080:80 --name zad1cz1 tchzad1:v1
```


```shell
docker history tchzad1:v1
```


```shell
docker logs zad1cz1
```


<i>Komendy do  zastopowania i usunięcia kontenera</i>
```shell
docker stop zad1cz1
```
```shell
docker rm zad1cz1
```
 # Część 2 (Dodatkowa)
"# Zadanie1" 
"# Zadanie1" 
