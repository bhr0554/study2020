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
  
docker를 설치하는 2가지 방법.  
#### 1.  
$ dnf install --nobest docker-ce  
--nobest option은 docker 설치에 가장 적합한 종속 package들을 설치해준다.  
--nobest option없이 특정 버전을 설치할 때에는 아래와 같이 진행한다.  
  
#### 2.  
$ dnf list docker-ce --showduplicates | sort -r (repository에 있는 docker버전 목록)  
$ dnf install docker-ce-버전  
ex) $ dnf install docker-ce-3 : 18.09.1-3.el7  
단, 특정 버전을 설치하려 하면 의존성문제로 인해 설치되지 않을 수 있습니다.
  
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

* * *
아래 내용은 Docker 공식 사이트에서 찾아본 장점입니다.  
  
### 1.개발, 배송 및 배포를 위해 소프트웨어를 표준화 된 단위로 패키지합니다.  
  
컨테이너는 코드와 모든 종속성을 패키지화하는 표준 소프트웨어 단위이므로 응용 프로그램이 한 컴퓨팅 환경에서 다른 컴퓨팅 환경으로 빠르고 안정적으로 실행됩니다.  
Docker container 이미지는 가볍고, 독립적이며, application을 실행시키기 위한 모든 것(code,runtime,system tools, system libraries, 설정)을 포함한 경량의 소프트웨어 패키지입니다.  
  
Container 이미지는 Docker Engine위에서 실행되어 container가 된다.  
Linux와 Windows 둘 다에서 사용가능하다. 컨테이너 소프트웨어는 환경에 구애받지 않고 항상 똑같이 실행될 것이다.  
Container는 환경으로부터 소프트웨어를 격리하고, development(서버 개발 환경)과 stageing사이에서 보이는 여러 환경 차이에도 불구하고 작동되는 것을 보장한다.  
>staging = 운영 환경과 거의 동일한 환경을 만들어 놓고, 운영환경으로 이전하기 전에, 여러 가지 비 기능적인 부분 (Security, 성능, 장애등)을 검증하는 환경이다.  
개발환경 참고 : <https://bcho.tistory.com/759>  
  
##### Docker Engine에서 실행되는 Docker containers는  
 - 1. Standard(표준): Docker는 container를 위한 표준규격을 생성함으로써 어디서든 간편히(portable) 사용할 수 있다.  
 - 2. Lightweight(경량): Container는 Host OS 커널을 공유하여 app마다의 os가 필요하지 않으므로 서버 효율성을 높이고 라이센스 비용을 절감시킨다.  
 - 3. Secure(보안): Docker는 app에 격리된 공간을 제공하고, App은 container안에서 안전할 수 있다.  
  
  
### 2. Docker Container는 모든 곳에서 동작한다:Linux, Windows, Cloud etc.  
개발자의 필수 항목에 집중하였고, OS를 공유하였기 때문에 Docker의 기술은 유일무이하다.  
  
컨테이너가 거의 os 가상화나 다름없다.(하드웨어대신)  
컨테이너는 휴대성이 좋고 효율적이다.  
  
##### CONTAINERS  
컨테이너는 코드와 종속성을 함께 패키지하는 앱 계층의 추상화입니다.  
여러 컨테이너는 같은 machine에서 실행될 수 있고, OS 커널을 공유한다.  
컨테이너는 VM보다 적은 공간을 차지합니다. 또, 더 많은 app을 핸들링할 수 있고, 적은 수의 OS가 필요합니다.  
  
##### VIRTUAL MACHINES  
VM은 하나의 서버를 여러 서버로 나누는 물리적 하드웨어의 추상화입니다.  
각 VM에는 운영 체제, 응용 프로그램의 전체 필수요소가 필요합니다. 바이너리 및 라이브러리까지 수십 GB를 차지합니다. 이로 인해 VM booting은 느릴 수 있습니다.  
  
##### Containers and Virtual Machines Together  
컨테이너와 VM을 함께 사용하면 app을 배포하고 관리하기 편해집니다.(직접 환경 구성을 해봐야 와닿지 않을까 싶다.)  


