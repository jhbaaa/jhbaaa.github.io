---
layout: post
title: 파이프라인(Pipeline) 사용법
category: Linux
tag: [리눅스 명령어]
---
# 파이프라인

파이프라인은 어떤 명령의 실행 결과 출력을 그대로 다른 명령어에 전달하는 것을 의미합니다. 예를 들어 엄청난 양의 Log가 있다고 할 때, 여기서 원하는 단어가 들어간 라인만 필터링하고, 그 결과에서 또 다른 검색어로 필터링해서 그 결과를 조회하는 것도 파이프라인을 사용하는 것이라고 생각할 수 있습니다.

안드로이드의 `logcat`의 예를 들어보겠습니다.

`adb shell`로 안드로이드 쉘(Shell)에 접속한 다음

~~~
logcat
~~~

을 입력하면 엄청난 양의 Log가 화면에 출력이 됩니다. 눈으로 쫓아가기도 힘들 정도인데, 여기에 `grep`을 이용해서 필터링을 해보도록 하겠습니다.

~~~
logcat | grep "snowdeer"
~~~

여기서 '|'는 파이프라인을 의미합니다. 양쪽의 명령어를 연결해주는 역할을 합니다. 즉, `logcat`으로 나온 결과를 `grep "snowdeer"`로 다시 필터링을 하도록 만들어줍니다.

파이프라인은 다음과 같이 여러 개 연결할 수 있습니다.

~~~
logcat | grep "snowdeer" | grep -v "ignore"
~~~

`grep`의 `-v` 옵션은 해당 검색어를 제외하라는 옵션입니다. 

그리고 만약, 마지막 결과를 `less`와 같은 텍스트뷰어에서 조회하는 것도 가능합니다. (안드로이드 Shell에는 `less`가 없습니다.)

~~~
명령어 | grep "snowdeer" | grep -v "ignore" | less
~~~

<br>

## tail

실시간으로 바뀌는 파일의 끝 부분만 출력하는 명령어로 `tail`이 있습니다. (마찬가지로 안드로이드 Shell에는 없습니다.)

~~~
tail -F access.log
~~~

라고 하면, 'access.log' 파일이 갱신될 때마다 추가된 내용을 실시간으로 갱신해서 보여주는 기능을 합니다. `-F` 옵션은 해당 파일의 변경을 감시하라는 옵션입니다.

여기에도 마찬가지로 파이프라인으로 추가 필터링을 걸어줄 수 있습니다.