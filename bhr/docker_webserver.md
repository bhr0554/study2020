---
title: "How to install web server by Docker"
date: 2020-07-29T22:03:39+09:00
categories: [docker]
tags: [docker, docker_webserver, docker_nginx, docker_httpd, nginx, httpd]
cover: ""
draft: false
---
기본 설명  
$ docker pull 이미지명
$ docker run -dit --name 컨테이너명 -p 외부포트:컨테이너내부포트 Host경로:Container경로 이미지명  
* \-d ( 백그라운드 실행> webserver 등)  
* \-it ( 입출력 해야 하는 container일 경우> db서버 등)  
* 외부에서 들어오는 tcp포트에 대응하는 container 내부 tcp포트
* Host의 실 경로:Container내부 경로 
  
$ docker ps -a (도커프로세스 목록으로써 컨테이너id확인 가능)  
$ docker exec -it 컨테이너id /bin/bash (container 진입)  
root@컨테이너id: $ exit (container 나와서 Host로 돌아감)  
  
 
* * *
### Nginx
참고 사이트  
docker 공식 : <https://hub.docker.com/_/nginx>  
참고 : <https://minimilab.tistory.com/8>  
  
$ docker pull nginx:latest (최신버전의 nginx)  
$ docker run --name some-nginx -v /home/nginx:/usr/share/nginx/html:ro -d -p 80:80 nginx  
$ vi /home/nginx/index.html (nginx url 접속 시 index 페이지)  
$ docker exec -it 6b3e4f73dd81 /bin/bash (Docker Container 경로 진입)  
$ root@6b3e4f73dd81:/# exit (컨테이너 나가기)  
  
    

### Httpd
$ docker pull httpd:latest
$ docker run -dit --name httpd -p 81:80 -v "$PWD":/usr/local/apache2/htdocs/ httpd:latest
  $"PWD" 는 현재 경로  
$ vi /home/httpd/index.html (/home/httpd는 docker run할 때 지정한 "$PWD"경로임.)  
  

