---
layout: post
title: "Docker-Toolbox에서 디렉토리 마운트 방법"
description: "윈도우즈 환경 Docker에서 디렉토리 마운트 방법"
categories: [tip]
tags: [docker, docker-toolbox, windows]
redirect_from:
  - /2019/08/01/
---

* table of contents
{:toc .toc}

## 디렉토리 지정해서 Docker-Volume 사용하기
- VirtualBox 설정의 공유폴더에서 공유할 디렉토리를 설정(이름을 확인한다.) VM을 정지한 상태에서 진행.


~~~sh
$ VBoxManager sharefolder add [VM Name] --name [SF name] --hostpath [디렉토리]
~~~

- virtualbox ssh 접속
~~~sh
$ docker-machine.exe ssh
~~~

- 공유 디렉토리 마운트
~~~sh
$ mkdir -p /shared
$ sudo mount -t vboxsf -o uid=1000,gid=50 [공유이름] /shared
~~~

- 리부팅
~~~sh
$ docker-machine.exe restart
~~~

## Docker-Compose에 적용

~~~yml
[docker-compose.yml example]

services:
    image: ....
    container_name : ...
    ...
    volumes:
        - /shared:/home/shared   #external dir:container dir
~~~
