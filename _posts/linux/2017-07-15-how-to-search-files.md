---
layout: post
title: 파일 검색
category: Linux
tag: [Linux 명령어]
---

리눅스에서 파일을 찾는 방법은 `find` 명령어를 이용해서 찾을 수 있습니다.
그리고 `-name` 옵션을 이용해서 원하는 파일을 검색할 수 있습니다.

탐색 경로를 생략한 경우에는 현재 작업중인 폴더부터 검색을 시작합니다.
읽기 권한이 없는 폴더는 건너뜁니다.

~~~
find -name [파일명]

ex)
find -name snowdeer
~~~

권한이 없는 폴더까지 검색을 하고 싶으면 앞에 `sudo`로 루트 권한을 얻으면 가능합니다.

루트 폴더부터 모든 폴더의 파일을 다 검색하고 싶을 때는 `/`를 명시하면 됩니다.

~~~
sudo find / -name snowdeer
~~~