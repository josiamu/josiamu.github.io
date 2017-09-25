---
layout: post
title: "Docker Workshop"
description: ""
categories: docker
tags: [unix,docker]
---

#### [Docker_Presentation_NODEJS](/book/Docker_Presentation_NODEJS.pdf)

---

### Workshop_1-1_Download_Install

<del>
[Link for download](https://www.docker.com/products/docker-toolbox)
</del>

- <del>See PDF document for detail to install</del>
- <del>After finished then run below command for check docker-machine (Command prompt)</del>
  - <del>`docker-machine --version`</del> 				
    - <del>check version of docker machine & readyness</del>
  - <del>`docker-machine create --driver virtualbox labdocker`</del>
    - <del>create new docker-machine for lab</del>
  - <del>`docker-machine ls`</del>
    - <del>check ip address of new docker-machine</del>
  - <del>`docker-machine start labdocker`</del>
    - <del>start service</del>
- <del>SSH to docker-machine (labdocker)</del>
  - <del>`docker-machine ssh labdocker`</del>
    - <del>default ssh via command prompt</del>
  - <del>access via putty(`windows`) to ip address</del>
  - <del>access via Shell(`mac`)</del>
    - <del>Shell - New Remote Connection (Service: ssh)</del>
- <del>Remark:default username/password for access docker-machine is docker/tcuser</del>

---

### Workshop_1-2_Access_PoolImage

<del>Access docker-machine via SSH</del>

1. <del>Command Line ==> `docker-machine ssh labdocker`</del>
2. <del>Putty (Windows) / Shell (MAC)</del>
  
docker-machine operate:

1. <del>Start 	==> `docker-machine start labdocker`/del>
2. <del>Stop 	==> `docker-machine stop labdocker`/del>
3. <del>Restart 	==> `docker-machine restart labdocker`/del>
4. <del>Remove	==> `docker-machine rm labdocker`/del>
5. <del>Create	==> `docker-machine create --driver virtualbox <name of docker-machine>`/del>
6. <del>Status	==> `docker-machine status labdocker`/del>
7. <del>View IP	==> `docker-machine ls`/del>


Pull image (Access to docker-machine via SSH first)

1. `docker pull josiamu/alpine:latest` 		==> pull docker image from repository (josiamu/alpine) with tag "latest"
2. `docker pull josiamu/alpineweb:latest`	==> pull docker image from repository (josiamu/alpineweb) with tag "latest"
3. `docker images` 				==> check sizing and detail of all image in docker-machine

---

Workshop_1-3_Create_PushImage

1. access url: http://hub.docker.com and register
2. create repository name alpineweb
3. Tag image to your account name: `docker tag labdocker/alpineweb:latest <account>/alpineweb:latest`
4. Login to hub.docker.com via step below
  1. `docker login -u <account> -p <password> -e <email address>`
  2. `docker push <account>/alpineweb:latest`
  3. `docker logout`

---

#### Workshop_1-4_Run_Container

Interactive NODEJS

- run docker on interactive mode with command

  ```
  docker run  -i -t --rm --name nodejs -p 3000:3000 \
  josiamu/alpineweb:latest node hello.js
  ```

- open browser with url: `http://<ip address of docker>:3000`
- open another session and press command: `docker ps`

Detach NODEJS

- run docker on detach mode with command

  ```
  docker run -d -t --name nodejs -p 3000:3000 \
  josiamu/alpineweb:latest node hello.js
  ```

- open browser with url: `http://<ip address of docker>:3000`
- access shell to container with command: `docker exec -i -t nodejs sh`
- With command: `docker ps`
- Try stop/start docker with command: `docker stop nodejs`,`docker ps -a`,`docker start nodejs`
- After finished to stop container. We will remove docker container with command: `docker rm nodejs`

---

#### Workshop_1-5_CPU_Memory_IO

- configure multiple CPU for "labdocker"
- Download and Run "cAdvisor"
- pull image with command: docker pull josiamu/cadvisor:latest
- docker run with command:

  ```
  docker run \
  --volume=/var/run:/var/run:rw \
  --volume=/sys:/sys:ro \
  --volume=/var/lib/docker/:/var/lib/docker:ro \
  --publish=8080:8080 \
  --detach=true \
  --name=cadvisor \
  josiamu/cadvisor:latest
  ```
- open browser with url: `http://<ip address of docker>:8080` and workthrough
- Download and Run "busybox"
- pull image with command: `docker pull josiamu/busybox:latest`

  ```
  docker run -d \
  --name='Share_30' \
  --cpuset-cpus=0 \
  --cpu-shares=30 \
  josiamu/busybox:latest md5sum /dev/urandom  
  ```

  ```
  docker run -d \
  --name='Share_70' \
  --cpuset-cpus=0 \
  --cpu-shares=70 \
  josiamu/busybox:latest md5sum /dev/urandom
  ```  

- open cAdvisor and Check
- stop all container with command: `docker stop Share_30 Share_70`
- remove all container with command: `docker rm Share_30 Share_70`
- memory and CPU `docker update --cpuset-cpus=3 Share_70`

---

#### Workshop_1-6_Network

- Pull image nginx with command: 		"docker pull josiamu/nginx:lab"
- Pull image nodejs (web1) with command:	"docker pull josiamu/alpineweb:web1"
- Pull image nodejs (web2) with command:	"docker pull josiamu/alpineweb:web2"
- Create Public Network with command:

  ```
  docker network create --driver bridge \
  --subnet=192.168.100.0/24 --ip-range=192.168.100.128/25 \
  --gateway=192.168.100.5 --opt="com.docker.network.mtu"="1500" webpublic

  docker network create --driver bridge \
  --subnet=192.168.101.0/24 --ip-range=192.168.101.128/25 \
  --gateway=192.168.101.5 --opt="com.docker.network.mtu"="9000" webinternal

  docker network ls
  ```

- Run container web1 & web2 with command:

  ```
  docker run -dt --name web1 --net webinternal \
  --ip="192.168.101.131" josiamu/alpineweb:web1 node hello.js

  docker run -dt --name web2 --net webinternal \
  --ip="192.168.101.132" josiamu/alpineweb:web2 node hello.js
  ```  

- Run container nginx and attach network

  ```
  docker run -dt --name nginx --net webinternal \
  --ip="192.168.101.130"  -p 80:8080 josiamu/nginx:lab

  docker network connect webpublic nginx --ip="192.168.100.130"  
  ```

- Open url: `http://<ip address of docker-machine>:80/nodejs`

- Shell to nginx and test curl to nodejs with command below:

  ```
  docker exec -it nginx sh
  curl http://192.168.101.131:3000
  curl http://192.168.101.132:3000
  ```

- Clean up container with command:

  ```
  docker stop web1 web2 nginx
  docker rm web1 web2 nginx  
  ```

---

#### Workshop_1-7_Volume

- Create volume container with command:

  ```
  docker run -dt --name datavol \
  -v /data josiamu/alpine sh
  ```

- Create web container (web1) by attach volume with command:

  ```
  docker run -dt --name web1 \
  --volumes-from datavol josiamu/alpine sh
  ```

- Shell to container web1 and touch file on /data

  ```
  docker exec -it web1 sh
  touch /data/test_web1
  ```

- Create web container (web2) by attach volume with command:

  ```
  docker run -dt --name web2 \
  --volumes-from datavol josiamu/alpine sh
  ```

- Shell to container web2 and touch file on /data

  ```
  docker exec -it web2 sh
  touch /data/test_web2
  ```

- Create backup for volume /data by run container with command:

  ```
  docker run --rm --volumes-from datavol \
  -v $(pwd):/backup josiamu/ubuntu tar cvf \
  /backup/vol001.tar /data
  ```

- We will see backup file (vol001.tar) on /home/docker

- Shell to any container to delete file

  ```
  docker exec -it web1 sh
  rm * /data
  ```

- Restore backup for volume /data by run container with command:

  ```
  docker run --rm --volumes-from datavol \
  -v $(pwd):/backup josiamu/ubuntu bash -c \
  "cd /data && tar xvf /backup/vol001.tar --strip 1"
  ```

- Check on any container for check file

  ```
  docker exec -it web1 sh
  ls -l /data
  ```

- Cleanup lab

  ```
  docker stop web1 web2 datavol
  docker rm -v web1 web2 datavol  
  ```

---

#### Workshop_1-8_Inspect_Logs

- Create container nginx with command:

  ```
  docker run -dt --name nginx -p 80:8080 josiamu/nginx:latest
  ```

- Check configuration of container with command:

  ```
  docker inspect nginx |more
  ```

- Check log of container with command:

  ```
  docker logs nginx |more
  ```

- Clean up lab:

  ```
	docker stop nginx
	docker rm nginx
  ```  

---  

#### Workshop_1-9_DockerFile

- On docker-machine. Create directory "nodejs" for keep dockerfile with command: `mkdir /home/docker/nodejs`

- On WINSCP (For Windows) for transfer file `Hello.js` and `dockerfile` to `/home/docker/nodejs`

- Build docker image from command: `docker build -t josiamu/node:1.0 /home/docker/nodejs`

- Test run docker image from command: `docker run -dt --name NODEJS -p 3000:3000 josiamu/node:1.0`

- open url: `http://x.x.x.x:3000`

- Check IP Address of docker-machine for configure in nginx.conf by command: `docker-machine ls`

- Open nginx.conf for configure IP Address on nginx.conf

- On docker-machine. Create directory "nginx" for keep dockerfile with command: `mkdir /home/docker/nginx`

- On WINSCP (For Windows) for transfer file `nginx.conf` and `dockerfile` to `/home/docker/nginx`

- Build docker image from command: `docker build -t josiamu/web:1.0 /home/docker/nginx`

- Test run docker image from command: `docker run -dt --name NGINX -p 8080:8080 josiamu/web:1.0`
- open url:"http://x.x.x.x:8080"
- open url:"http://x.x.x.x:8080/nodejs"
- Clean Up Lab with command below
  - `docker stop NGINX NODEJS`
  - `docker rm NGINX NODEJS`
  - `cd / & rm -R -f /home/docker/nodejs & rm -R -f /home/docker/nginx`

---

#### Workshop_1-10_Compose

Install docker-compose

- Get docker-compose from curl to /home/docker with command:

  ```
  curl -L https://github.com/docker/compose/releases/download/1.6.2/docker-compose-`uname -s`-`uname -m` > /home/docker/docker-compose
  ```

- Copy docker-compose to /usr/local/bin/docker-compose with command:

  ```
  sudo cp /home/docker/docker-compose /usr/local/bin/docker-compose
  ```

- Change mode for allow execute with command: `sudo chmod +x /usr/local/bin/docker-compose`
- Check docker-compose readyness by command: `docker-compose --version`


=================
COMPOSENODEJS
=================

- On docker-machine. Create directory `composenodejs` for keep compose-service with command:

  ```
  mkdir /home/docker/composenodejs
  mkdir /home/docker/composenodejs/web
  ```

- Transfer file `docker-compose.yml` to `/home/docker/composenodejs`
- Transfer file `dockerfile`,`Hello.js` from /web to `/home/docker/composenodejs/web`
- Start docker-compose on path: `/home/docker/composenodejs` by command: `docker-compose up -d`
- Open url: `http://x.x.x.x:3000` for check result
- Stop docker-compose by command: `docker-compose stop`
- Remove docker-compose by command: `docker-compose down`


================
MULTIPLENODEJS
================

- On docker-machine. Create directory "composemultinodejs" for keep compose-service with command:

  ```
  mkdir /home/docker/composemultinodejs
  mkdir /home/docker/composemultinodejs/web1
  mkdir /home/docker/composemultinodejs/web2
  mkdir /home/docker/composemultinodejs/nginx  
  ```

- Transfer file `docker-compose.yml` to `/home/docker/composenodejs`
- Transfer file `dockerfile`,`Hello.js` from composemultinodejs/web1 to `/home/docker/composemultinodejs/web1`
- Transfer file `dockerfile`,`Hello.js` from composemultinodejs/web2 to `/home/docker/composemultinodejs/web2`
- Transfer file `dockerfile`, `nginx.conf` from composemultinodejs/nginx to `/home/docker/composemultinodejs/nginx`
- Start docker-compose on path: `/home/docker/composemultinodejs` by command: `docker-compose up -d`
- Open url: `http://x.x.x.x/nodejs` for check result
- Stop docker-compose by command: `docker-compose stop`
- Remove docker-compose by command: `docker-compose down`

---

#### Workshop_1-11_Registry

===================================
Registry on single docker-machine
===================================

- Getting image of registry by command: `docker pull registry:2.3`
- Running registry by command:

  ```
  docker run -d -p 5000:5000 \
  --restart=always --name registry \
  -e REGISTRY_STORAGE_DELETE_ENABLED=true \
  -v /home/docker:/var/lib/registry registry:2.3   
  ```

- Tag image for upload to new registry with command:

  ```
  docker tag josiamu/alpine:latest \
  localhost:5000/alpine:latest  
  ```

- Push docker images to registry with command: `docker push localhost:5000/alpine:latest`

- Operate with registry with curl:

  ```
  curl -X GET http://localhost:5000/v2/_catalog ==> List all images in catalog
  curl -X GET http://localhost:5000/v2/alpine/tags/list ==> List all tag on alpine image
  ```

- Test Delete and redownload docker image with command:

  ```
  docker rmi localhost:5000/alpine:latest
  docker images
  docker pull localhost:5000/alpine:latest
  docker images  
  ```

- Delete docker images from registry

  ```
  curl -X DELETE http://localhost:5000/v2/alpine/manifests/sha256:6756df7c9e260c69087fbe2891740db105e41be00fc3ffc124575f54b85ddf8a
  ```

- Clean Up Lab by command:

  ```
  docker stop registry
  docker rm -v registry
  ```

===================================
Registry on multihost docker-machine
===================================

- Create second docker-machine "labdocker2" by command (on notebook): `docker-machine create labdocker2 --driver virtualbox`

- Check ip address of new docker-machine (labdocker2) by command (on notebook): `docker-machine ls`

- Create new directory for store key file on "labdocker" by command: `mkdir /home/docker/labdockercert` (labdocker, labdocker2)
- Transfer `labdocker.com.key`,`labdocker.com.crt` to `/home/docker/labdockercert` (labdocker)
- Transfer `labdocker.com.crt`, to `/home/docker/labdockercert` (labdocker2)
- Trust certificate via command (labdocker, labdocker2):

  ```
  sudo mkdir /etc/docker/certs.d
  sudo mkdir /etc/docker/certs.d/labdocker.com:5000
  sudo cp /home/docker/labdockercert/labdocker.com.crt /etc/docker/certs.d/labdocker.com:5000
  ```

- Add "192.168.99.100	labdocker.com" on (labdocker, labdocker2)

  ```
  sudo vi /etc/hosts

  192.168.99.100	labdocker.com
  ```

- Run container registry:

  ```
  docker run -d -p 5000:5000 \
  --restart=always --name registry \
  -v /home/docker:/var/lib/registry \
  -v /home/docker/labdockercert:/certs \
  -e REGISTRY_STORAGE_DELETE_ENABLED=true \
  -e REGISTRY_HTTP_TLS_CERTIFICATE=/certs/labdocker.com.crt \
  -e REGISTRY_HTTP_TLS_KEY=/certs/labdocker.com.key \
  registry:2.3
  ```

- Tag docker image and Test Push (via labdocker docker-machine) by command:

  ```
  docker tag josiamu/alpine:latest \
  labdocker.com:5000/alpine:1.0

  docker push labdocker.com:5000/alpine:1.0
  ```

- Test pull image from labdocker 2 (via labdocker2 docker-machine) by command:

  ```
  docker pull labdocker.com:5000/alpine:1.0
  ```

- Operate with docker registry via https

  ```
  curl --cacert /home/docker/labdockercert/labdocker.com.crt -X GET https://labdocker.com:5000/v2/_catalog ==> List all images in catalog
  curl --cacert /home/docker/labdockercert/labdocker.com.crt -X GET https://labdocker.com:5000/v2/alpine/tags/list ==> List all tag on alpine image
  curl --cacert /home/docker/labdockercert/labdocker.com.crt -X DELETE https://labdocker.com:5000/v2/alpine/manifests/sha256:6756df7c9e260c69087fbe2891740db105e41be00fc3ffc124575f54b85ddf8a  
  ```
  
---
