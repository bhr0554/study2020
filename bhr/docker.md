---
title: "Docker"
date: 2020-07-27T22:43:49+09:00
categories: [docker, docker_install]
tags: [docker]
cover: ""
draft: false
---
도커 용어 정리 : <https://docs.microsoft.com/ko-kr/dotnet/architecture/microservices/container-docker-introduction/docker-terminology>  
도커 개념 정리 : <https://cultivo-hy.github.io/docker/image/usage/2019/03/14/Docker%EC%A0%95%EB%A6%AC/>  

* * *
# docker install to CentOS8  
$ dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo (docker를 설치할 때 바라볼 repository 설정)  
  
docker를 설치하는 3가지 방법.  
#### 1.  
$ dnf install --nobest docker-ce  
--nobest option은 docker 설치에 가장 적합한 종속 package들을 설치해준다.  
--nobest option없이 특정 버전을 설치할 때에는 아래와 같이 진행한다.  
  
#### 2.  
$ dnf list docker-ce --showduplicates | sort -r (repository에 있는 docker버전 목록)  
$ dnf install docker-ce-버전  
ex) $ dnf install docker-ce-3 : 18.09.1-3.el7  
단, 특정 버전을 설치하려 하면 방화벽문제로 docker container 내부에 DNS가 실행되지 않아 에러가 발생할 수 있다.  
위와 같은 문제를 해결하기 위해서는 방화벽을 비활성화시켜주어야 한다.  
$ systemctl disable firewalld  
  
#### 3.  
최신 버전을 설치하려 할 때에는 아래와 같이 진행한다.  
$ dnf install https://download.docker.com/linux/centos/7/x86_64/stable/Packages/containerd.io-1.2.6-3.3.el7.x86_64.rpm  
$ dnf install docker-ce  
  
(실행해 보진 않았음. 필자는 --nobest옵션을 사용하여 설치함.)  
  
$ systemctl start docker (docker 실행)  
  
* * *
### Docker를 사용하는 이유
Docker를 쓰는 가장 큰 이유는 환경설정이 매우 간단하기 때문이다.  
기본적으로 docker에서 제공해주는 이미지들이 있어 명령어 몇 줄 입력하는 것으로 server세팅을 할 수가 있다.  
  
예로, 아래 링크는 docker를 이용한 mariadb와 mysql 세팅 방법이다.  
Link: <https://bhr0554.github.io/study/docker/docker_mysql>  
  
  
Docker는 VM과 비슷하게 보일 수 있으나 큰 차이점을 가지고 있다.  
VM은 Host OS위에 Guest OS를 설치해야 하고, Docker는 Host OS를 함께 사용한다는 것이다.  
즉, VM의 경우 App하나를 구동시키기 위해 그에 맞는 Guest OS 등 환경설정을 달리 해야 하며, 가상의 공간을 나눔으로써 제한적인 자원(HDD, CPU 등) 공간을 갖게 되어 속도가 느려지게 되는 반면, Docker의 경우에는 Host OS위에서 동작하여 Application을 동작시키기 위해 Host에 없는 것만을 추가적으로 설치하여 실행되기 때문에 VM에 비해 속도가 빠를 수밖에 없다.  
이것은 곧, Docker는 어느 환경에서나 동일하게 작용된다는 것과 같은 뜻이다.  
애플리케이션을 환경에 구애 받지 않고 실행하는 것이 Docker의 기술이다.  
  
  
docker에 대한 공부는 진행중에 있음으로 추가적으로 적어나아갈 것입니다.  
