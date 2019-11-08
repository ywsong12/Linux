## ntp 설치 및 설정
##### 서버실들에는 시간을 하나로 맞추기위한 기준인 NTP 서버가 있고 이 서버와의 시간동기화 방법에 관한 내용
- 인터넷을 통한 NTP 설치(OS - RHEL7, CeontOS 7)
``` 
#] yum install ntp                   //yum repository에서 ntp패키지와 해당 의존성을 가진 다른 패키지도 모두 다운받아 설치
#] rpm -qa | grep ntp                //ntp 패키지가 설치되었는지 확인
#] systemctl start ntpd              //ntpd 구동
#] systemctl status ntpd             //ntp 상태 정보확인
```
- 외부 인터넷사용 제한적일 경우의 설치(OS - RHEL7, CeontOS 7)
```
#] yum 
