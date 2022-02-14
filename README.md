## Dockerfile
```bash
# base 이미지를 지정한다
# FROM ubuntu:20.04
FROM alpine

# 환경변수를 지정
ENV MYHOME /my/home

# 디렉토리를 생성하고 현재 경로를 해당 디렉토리로 변경한다
WORKDIR $MYHOME
RUN touch $MYHOME/myfile.txt

WORKDIR /aa
# host 안의 파일을 container 안으로 복사한다
COPY file1.txt /aa/fileA.txt

# /app 디렉토리가 없으면 생성하고 파일을 카피한다
COPY target/myapp.jar /app/app.jar

# container 가 실행될 때 동작할 명령을 지정
ENTRYPOINT ["tail", "-f", "/dev/null"]
```

## docker pull
```bash
docker pull ubuntu:20.04
```

## docker build
```bash
docker build -t myubuntu:20.04 -f ubuntu/Dockerfile .
```

## docker run
```bash
# -p 8080:80 | 호스트 8080 포트를 컨테이너 80 포트로 포워딩
docker run -itd -p 8080:80 --name ubuntu ubuntu:20.04
```

## docker exec
```bash
docker exec -it ubuntu bash
```

## 도커 컨테이너 모두 삭제
```bash
docker rm -f `docker ps -aq`
```

## 도커 이미지 모두 삭제
```bash
docker rmi `docker images -q`
```

## docker ps
```bash
docker ps
docker ps -a
```

## docker best practices
[docker best practices](DockerBestPractices.md)
