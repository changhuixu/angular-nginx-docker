# AngularNginxDocker

```bash
ng new angular-nginx-docker --minimal

# build a docker image
docker build -t angular-nginx-docker .

docker run -d -p 80:80 angular-nginx-docker
docker run -it -p 80:80  angular-nginx-docker
docker exec -it angular-nginx-docker /bin/sh
```

```bash
# run the default nginx website in a container
docker run --name docker-nginx -p 80:80 nginx

# navigate the nginx files in the docker alpine image
docker run -it nginx:alpine sh
# navigate the nginx files in the docker image
docker run -it --name nginx-container -P nginx bash
root@805435da60f9:/# cd etc/nginx/

```

```bash
ng build --prod

docker run -it -p 80:80 \
    -v /$PWD/dist/angular-nginx-docker://usr/share/nginx/html:ro \
    nginx:alpine

docker run -it -p 4200:80 \
    -v /$PWD/dist/angular-nginx-docker://usr/share/nginx/html:ro \
    -v /$PWD/.nginx/nginx.conf://etc/nginx/nginx.conf:ro \
    nginx:alpine

```

```bash
# compare gzip effect using the following two commands

$ curl http://localhost:80/ \
    --silent \
    --write-out "%{size_download}\n" \
    --output /dev/null
# console output: 814

$ curl http://localhost:80/ \
    --silent \
    -H "Accept-Encoding: gzip,deflate" \
    --write-out "%{size_download}\n" \
    --output /dev/null
# console output: 391
```
