---
# 도커 자주 사용하는 명령어(command)
* [이미지](#이미지)
* [컨테이너](#컨테이너)
* [컴포즈](#컴포즈)
* [도커파일](#도커파일)
---

# 이미지
이미지 조회
```
docker images [OPT]
# [OPT]
# -a: 모든 이미지
```
이미지 삭제
```
docker rmi $IMAGE [IMAGE...]
```
이미지 다운로드
```
docker pull $IMAGE
```
이미지 상세정보
```
docker image inspect $IMAGE
```
---
# 컨테이너
```admonish info title="조회"
~~~
docker ps [OPT]
~~~
~~~
[OPT]
-a: 모든컨테이너
~~~
```

```admonish info title="삭제"
~~~
docker rm $CONTAINER
~~~
```

```admonish info title="로그"
~~~
docker logs $CONTAINER
~~~
```

```admonish info title="생성(이미지로부터)"
~~~
docker create [OPT] $IMAGE[:TAG] [ARG]
~~~
~~~
[OPT]
--name: 생성할 컨테이너의 이름주기, ex) --name sample
-i: 표준 입력활성화(non attach에서도 컨테이너 유지)
[ARG]
입력값을 추가로줌, ex) docker create ubuntu /bin/bash
~~~
```

```admonish info title="시작"
~~~
docker start [OPT] $CONTAINER
~~~
~~~
[OPT]
-a: 표준 출력,에러를 붙인다.
-i: 표준 입력을 붙인다.
~~~
default detach이다.
```

```admonish info title="종료"
~~~
docker stop $CONTAINER
~~~
```

```admonish info title="런"
~~~
docker run [OPT] $CONTAINER [ARG]
~~~
~~~
[OPT]
-i: 표준 입력 활성화
-t: TTY모드 사용
--name: 이름을 줄수 있음 ex) --name who
--privileged: 컨테이너안에서 호스트의 리눅스 커널 기능을 모두 사용합니다.
[ARG]
추가 입력값을 줄수있음
~~~
만약 local에 image가 없다면, dockerhub로부터 이미지를 pull받는다.  
default는 attach이다.
```

```admonish info title="실행"
~~~
docker exec [OPT] $CONTAINER [ARG]
~~~
~~~
[OPT]
-i: 표준 입력 활성화
-t: TTY모드 사용
[ARG]
추가 입력값을 줄수있음
~~~
attach와 다른점중 하나는, shell을 실행하는거라 exit해도 컨테이너가 죽지않는다.
```

---
# 컴포즈
목록조회
```
docker-compose ps
```
컴포즈 컨테이너 실행
```
docker-compose up
```
컴포즈 컨테이너 종료후 삭제
```
docker-compose down
```
멈춘 컨테이너 실행
```
docker-compose start
```
재시작
```
docker-compose restart
```
---
# 도커파일
도커 이미지 생성
```
docker build .
#현재위치에 Dockerfile이 존재하는경우
```