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
###### 패키지 준비 ntp-4.2.6p5-29.el7.centos.x86_64.rpm, ntpdate-4.2.6p5-29.el7.centos.x86_64.rpm, autogen-libopts-5.18-5.el7.x86_64.rpm   ###### 패키지파일은 rpm 미러사이트에서 다운로드(https://rpmfind.net/)
###### 준비된 패키지를 서버에 업로드(서버에 직접 저장매체 삽입하여 마운트또는 sftp 이용)
```
#] rpm -Uvh autogen-libopts-5.18-5.el7.x86_64.rpm  
#] rpm -Uvh ntpdate-4.2.6p5-29.el7.centos.x86_64.rpm
#] rpm -Uvh ntp-4.2.6p5-29.el7.centos.x86_64.rpm
ntp, ntpdate, libopt 패키지 설치 순서는 의존성 문제로 인하여 다음과 같이 진행 다만 다른 순서로 상관없이 진행 시에는  
명령어 뒤에 --nodeps(의존성 무시하고 강제설치) 추가
#] rpm -qa | grep ntp                //ntp 패키지가 설치되었는지 확인
#] systemctl start ntpd              //ntpd 구동
#] systemctl status ntpd             //ntp 상태 정보확인
```

