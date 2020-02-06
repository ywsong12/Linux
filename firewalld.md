## firewalld 사용법
#### 명령어
1. firewall-cmd --reload      //리로드를 진행, 방화벽 설정 후에는 리로드를 해줘야 적용 가능
2. firewall-cmd --get-zones   //Zone 리스트 출력
3. firewall-cmd --get-active-zones   //활성화된 Zone 리스트 출력
4. firewall-cmd --list-all    //사용 가능한 모든 서비스, 포트 리스트 출력
5. firewall-cmd --zone=public --ilst-all   //Public zone에 속한 사용 가능한 모든 서비스, 포트 리스트 출력

* --permanent : 영구적인 설정 등록(리로드 및 리부팅 시에도 규칙이 남아있음) 단, 사용시 리로드 명령어 실행하여야 적용됨.  
* --add-rich-rule : 규칙 생성  
* --rmove-rich-rule : 규칙제거  

#### 사용예제
##### Syslog(514) 포트 추가
```
#] firewall-cmd --permanent --zone=public --add-port=514/udp
```
##### Syslog(514) 포트 제거
```
#] firewall-cmd --permanent --zone=public --remove-port=514/udp
```
##### http 서비스 추가
```
#] firewall-cmd --permanent --zone=public --add-service=http
```
##### http 서비스 추가
```
#] firewall-cmd --permanent --zone=public --remove-service=http
```
##### 특정IP 차단
```
firewall-cmd --zone=public --add-rich-rule 'rule family="ipv4" source address=차단할IP drop'
```
##### 특정IP 허용
```
firewall-cmd --zone=public --add-rich-rule 'rule family="ipv4" source address=허용할IP accept'
```
