# 쿠버네티스 전 컨테이너에 대한 개념 정리




## 리눅스 컨테이너란?
```
리눅스 컨테이너는 운영체제 수준의 가상화 기술로, 리눅스 커널을 공유하면서 프로세스를 격리된 환경에서 실행하는 기술입니다.
하드웨어를 가상화하는 가상 머신과 달리 커널을 공유하는 방식이기 때문에 실행 속도가 빠르고 성능 상 손실이 거의 없습니다.

리눅스 namespace, cgroup 등의 커널 분리 기능을 활용해 컨테이너로 실행된 프로세스는 커널을 공유합니다.
```



### cgroup 이란
------------------------------------------------
1. cgroup 개요 
  - cgroups는 프로세스들의 자원의 사용을 제한하고 격리시키는 리눅스 커널 기능이다.
  
2. cgroup 서브 시스템
```
  1. CPU
    - CPU 사용량 제한

  2. CPUacct
    - CPU 사용량 통계

  3. CPUset
    - CPU나 메모리 배치를 제어

  4. memory 
    - 메모리 사용량 제한

  5. devices
    - 디바이스 엑세스 허가/ 거부

  6. freezer
    - 그룹에 속한 프로세스 정지/ 재개
  
7. net_cls
  - 네트워크 제어 태그를 부가

8. blkio
  - 블록 디바이스 입출력량 제어
 ```
 
 ### ubuntu 에서 cgroup 으로 실습해보기
------------------------------------------------
 1. 실습 환경 
  - Ubuntu 18.04.2 LTS
  
2. 실습 목표 
  - cgroup-tools 이용해서 간단 실습 해보기
  
```
1. cgroup tools 설치 
  - sudo apt install cgroup-tools
  
2. 예제 설정 파일 복사
  - cp /usr/share/doc/cgroup-tools/examples/cgred.conf /etc/
  
3. 설정 파일 생성
/etc/cgconfig.conf
==============================
group web2 {
cpu {
         cpu.cfs_quota_us=10000;
     }
     memory {
         memory.limit_in_bytes = 1024m;
     }
}
==============================
cpu.cfs_quota_us =  10000은 CPU 사용량 
memory.limit_in_bytes = 1024는 시스템 메모리의 1G에 해당합니다.
group web2 = web2 그룹 생성 

4.룰 설정 파일 생성 
/etc/cgrules.conf
=============================
# <user> <controllers> <destination> 
web2 cpu, memory web2
=============================
사용자 web2의 모든 프로세스를 10 % CPU와 1G 메모리로 제한

5.테스트 명령어 
 - /usr/sbin/cgconfigparser -l /etc/cgconfig.conf
 - /usr/sbin/cgrulesengd -vvv
 
6. 동작 확인 
  - cat /sys/fs/cgroup/cpu/web2/tasks 
  - cat /sys/fs/cgroup/memory/web2/tasks 

```

  

