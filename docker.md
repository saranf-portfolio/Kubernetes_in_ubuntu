#   ubuntu 18.04 설치& 컨테이너 실행 간단과정 

## ubuntu 18.04에 도커 설치 

#### 도커는 기본적으로 root 권한이 필요 합니다. root 가 아닌 사용자가 sudo 없이 사용하려면 해당 사용자를 docker 그룹에 추가 해 주어야 합니다.
```
  -  sudo usermod -aG docker $USER  # 현재 접속중인 사용자에게 권한주기 
```

1. 우분투는 데비안 계열로 apt 패키지 관리자를 사용 하므로 패키지 목록 업데이트를 먼저 실행합니다..
```
  -   sudo apt update -y
```

2. 도커 패키지 저장소를 apt 패키지 관리자에 등록 합니다. 
```
  -   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
  -   sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
```

3. 도커 패키지 저장소를 apt 관리자에 등록한 후 패키지 목록을 업데이트 해야 apt 패키지 관리자로 도커 설치가 가능합니다.
```
  -   sudo apt update -y
```

4. 도커CE 를 설치 합니다.
```
  -    sudo apt install -y docker-ce
```

5. 도커를 시작하는 명령어 입니다.
```
  -  sudo systemctl start docker 
```

5-1. 도커 정지 명령어 입니다.
```
  -   sudo systemctl stop docker 
```

5-2. 도커 상태 확인 명령어 입니다.
```
  -   sudo systemctl status docker 
```

6. 도커 버전 확인 명령어 입니다. 
```
  -   docker version
```

7. ubuntu 18.04 이미지를 다운 받습니다.
```
  -   docker run ubuntu:18.04 
```

8. ubuntu 18.04 이미지를 컨테이너로 실행한 뒤 bash shell 로 실행 합니다.
```
  -   sudo docker run --it ubuntu:18.04 /bin/bash

도커를 실행하는 명령어는 하단과 동일 합니다.
  -   docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]

옵션	설명
-d	detached mode 흔히 말하는 백그라운드 모드
-p	호스트와 컨테이너의 포트를 연결 (포워딩)
-v	호스트와 컨테이너의 디렉토리를 연결 (마운트)
-e	컨테이너 내에서 사용할 환경변수 설정
–name	컨테이너 이름 설정
–rm	프로세스 종료시 컨테이너 자동 제거
-it	-i(interactive) -t(tty)를 동시에 사용한 것으로 터미널 입력을 위한 옵션
–link	컨테이너 연결 [컨테이너명:별칭]

```

