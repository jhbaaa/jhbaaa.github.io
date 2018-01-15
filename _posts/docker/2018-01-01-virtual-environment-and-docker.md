---
layout: post
title: 가상 머신과 Docker
category: Docker
permalink: /blog/:year/:month/:day/:title/

tag: [Docker]
---
# 가상 머신과 Docker

Docker는 현재까지 많이 사용되어왔던 VMware, Microsoft Hyper-V, VirtualBox, Xen, 리눅스 KVM 등이 가상 머신과 비슷합니다.

가상 머신에 리눅스를 설치하고 다양한 서버 프로그램 및 DB를 설치합니다. 그리고 그 위에 App 또는 웹서비스 등을 실행했습니다. 이렇게 만들어진 가상 머신 이미지를 여러 서버에 복사해서, 이미지 한 장으로 서버를 계속해서 만들어낼 수 있습니다.

<br>

## 가상 머신

가상 머신은 간편하긴 했지만 성능면에서 부족한 부분이 많았습니다. 가상화 기술은 1960년대에 나왔지만 초기의 가상 머신들은 게스트의 하드웨어와 명령어(Instruction)를 전부 에뮬레이팅해야 했기 때문에 속도가 아주 느렸습니다.

이후 인텔과 AMD에서 CPU 차원의 가상화를 지원하기 시작했습니다. Intel VT-x나 AMD-V라는 기술로 HVM(Hardware Virtual Machine)이 가능해졌습니다. CPU의 하이퍼바이저(Hypervisor)가 하드웨어와 명령어를 빠른 속도로 처리해줄 수 있어서 성능이 많이 올라갔고 이러한 방식을 전가상화(Full Virtualization)이라고 했습니다.

![Image](/assets/docker/001.png)

그러다가 Xen(젠)이라는 소프트웨어기반 하이버파이저가 나오면서 가상화에 획기적인 성능 향상이 이루어졌습니다. 이 방식은 게스트 OS를 수정하여 호스트와 동일한 성능을 내도록 하는 방법이었고, 성능 덕에 아주 큰 인기를 끌게 되었습니다. 이를 반가상화(Paravirtualization)이라고 합니다. 커널 수정이 필요한 단점이 있었지만, 서버의 OS를 Linux를 많이 쓰게 되고 Linux가 오픈 소스였기 때문에 큰 문제가 되지 않았습니다.

<br>

## Docker

Docker는 반가상화보다 더 경량화된 방식입니다. 

![Image](/assets/docker/002.jpg)

위 그림과 같이 게스트 OS를 아예 설치하지 않습니다. 그 대신 서버 운영에 필요한 프로그램들과 라이브러리들만 설치할 수 있고, 시스템콜(Systemcall)과 같은 OS 자원은 호스트 OS와 공유합니다. 덕분에 이미지의 용량이 크게 줄어들었습니다.

Docker는 하드웨어 가상화가 없기 때문에 메모리 접근, 파일 시스템, 네트워크 속도가 기존의 가상 머신들에 비해 월등히 빠릅니다.

또한 Docker는 가상 머신과 달리 이미지의 용량이 작기 때문에 이미지의 생성/배포에 특화된 기능을 제공합니다. 하나의 파일로 이미지가 관리되기 때문에 버전 관리가 용이하고 Push/Pull 등의 명령어를 통해 이미지 업로드/다운로드가 자유롭습니다.

Docker는 베이스 이미지(Base image)로부터 새로운 이미지를 쉽게 만들 수 있습니다. 이 때 바뀐 부분만 이미지로 생성하고, 나중에 실행할 때는 베이스 이미지와 바뀐 부분을 합쳐서 실행합니다. 이런식으로 바뀐 부분들을 Layer라고 합니다.

![Image](/assets/docker/003.png)

<br>

## Docker 컨테이너

Docker 컨테이너는 이미지를 실행한 상태를 말합니다. 하나의 이미지로 여러 개의 컨테이너를 만들 수 있습니다.