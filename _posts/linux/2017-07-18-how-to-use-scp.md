---
layout: post
title: SCP 사용법
category: Linux
tag: [Linux 명령어]
---

## SCP (Secure Copy)
SCP(Secure Copy) 명령어는 원격의 파일이나 폴더를 복사하는 Linux 명령어입니다.
SCP 명령어는 다음과 같은 형태로 사용할 수 있습니다.

~~~
SCP [옵션] [원본 경로] [타켓 경로]
~~~

예를 들어서, 다른 곳에 있는 파일을 현재 위치로 다운로드하고 싶을 경우는 다음과 같은
형태로 사용할 수 있습니다.

~~~
SCP -R pi@192.168.0.100:/home/pi/temp ./
~~~

여기서 -R 옵션은 하위 폴더까지 모두 포함시키는 옵션입니다.

반대로 로컬에 있는 파일을 서버로 업로드할 경우는 다음과 같이 할 수 있습니다.

~~~
SCP -P 22 ./index.html pi@192.168.0.100:/home/pi
~~~

-P 옵션은 포트를 지정할 때 사용하며, 기본적으로 22번 포트를 사용하는 경우는 생략을 해도 됩니다.