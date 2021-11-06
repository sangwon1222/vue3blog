# DB 실행

### 윈도우

~/docker/postgres 경로에 있는 `compose-up.bat`실행

또는

```bash
docker-compose -f docker-compose-win.yml up --build -d
```

### linux / mac os

~/docker/postgres 경로에 있는 `compose-up`실행

또는

```bash
docker-compose -f docker-compose.yml up --build -d
```


# nginx 실행

DB와 ~/docker/nginx 경로만 다름

### hosts 파일 수정

C:\Windows\System32\drivers\etc\hosts

hosts 파일에 아래 내용 추가하기

```
127.0.0.1 www.devlog.com
```

 - 프론트는 www.devlog.com 으로 접속
   - 참고: axios 사용 시 baseUrl 는 필요없고 /api 등으로만 사용한다. nginx 에서 자동으로 설정되어있기 때문

 - API 문서는 www.devlog.com/apidoc 으로 접속
 

# apidoc 실행

DB와 ~/docker/apidoc 경로만 다름


# 서버 소스 빌드 (windows)
서버 내용 중 바뀐 내용이 있을 경우 적용을 위해 새로 빌드를 해야 한다.

(java IDE 가 있으면 상관없겠지만...)

./server 로 경로 이동(필수)을 한 후 (batch 파일이 현재 경로를 기준으로 실행되기 때문)

build.bat 파일 실행

또는 아래 명령어 실행
```bash
gradle clean build --exclude-task test
```


# 서버 실행 (windows)

./server 로 경로 이동(필수)을 한 후

server.bat 파일을 아래 명령어 실행
```bash
./server.bat auth start  // authapp 실행
./server.bat auth stop   // authapp 중지
./server.bat web start   // webapp 실행
./server.bat web stop    // webapp 실행
```
