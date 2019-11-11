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
###### 패키지 준비 ntp-4.2.6p5-29.el7.centos.x86_64.rpm, ntpdate-4.2.6p5-29.el7.centos.x86_64.rpm, autogen-libopts-5.18-5.el7.x86_64.rpm
###### 패키지파일은 rpm 미러사이트에서 다운로드(https://rpmfind.net/)
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
- 동기화를 위한 설정
```
#] systemctl stop ntpd               //ntp 기동 정지
#] vi /etc/ntp.conf                  //ntp 설정 파일 편집기로 수정
# Use public servers from the pool.ntp.org project.
# Please consider joining the pool (http://www.pool.ntp.org/join.html).
#server 0.centos.pool.ntp.org iburst   //필요없는 서버는 주석처리
#server 1.centos.pool.ntp.org iburst   //주석
#server 2.centos.pool.ntp.org iburst   //주석
#server 3.centos.pool.ntp.org iburst   //주석
server 'ntp서버 IP' iburst             //해당영역에 다음과 같이 내용을 추가 후 저장 ex) server 192.168.10.10 iburst (iburst 옵션 설명 : 동기화시에 기존시간과 차이가 많을 경우 동기화 시간을 단축)

#] systemctl enable ntpd             //부팅시에도 자동 실행되도록 서비스 등록
#] systemctl start ntpd              //ntp 기동
```
- 동기화를 즉시 해주는 ntpdate 사용법
```
#] ntpdate ntp서버 IP             //ntpdate 명령어 뒤에 ntp서버 IP를 입력 ex) ntpdate 192.168.10.10
#] crontab -e
* 3 * * * ntpdate 192.168.10.10  //크론테이블에 다음내용 추가 후 저장(매일 오전3시마다 ntpdate로 동기화 실행)
