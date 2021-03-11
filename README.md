# Get Started with NGINX on Docker

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/I3I63W4OK)

How to deploy a single-page app with NGINX in a docker container?

## [Medium Article](https://codeburst.io/get-started-with-nginx-on-docker-907e5c0c9f3a)

In this introductory article, we will use NGINX to server a Single-Page Application (SPA). We will set up and play with NGINX on docker, including (1) serving a website by mounting a volume to a docker container, and (2) building and running a docker image with a web app and NGINX.

---

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

docker run -it --rm -p 80:80 \
    -v /$PWD/dist/angular-nginx-docker://usr/share/nginx/html:ro \
    nginx:alpine

docker run -it --rm -p 4200:80 \
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

## License

Feel free to use the code in this repository as it is under MIT license.

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/I3I63W4OK)
