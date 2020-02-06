## iptables 를 활용한 설정 방법
### IPTABLE 체인
##### 체인 뒤에 번호를 붙임으로서 규칙의 순서를 정할 수 있다. ex)1,2,3...  
INPUT : 호스트를 향한 모든 패킷  
OUTPUT : 호스트에서 발생한 모든 패킷  
FORWARD : 호스트가 목적지가 아닌 모든 패킷  

### IPTABLE 옵션
-A : 새로운 규칙 추가  
-D : 규칙삭제  
-C : 패킷 테스트  
-R : 새로운 규칙으로 교체  
-I : 새로운 규칙 삽입
-P : 기본정책 변경  
-L : IPTABLE 리스트 출력  
-N : 새로운 체인 생성  
-F : 체인으로부터 모든 규칙을 삭제  
-Z : 모든 체인의 패킷, 바이트 카운터 값을 0으로 만듦  
-X : 비어있는 체인을 삭제  

### IPTABLE 매칭 옵션
-s : 출발지 패킷의 주소나 포트 입력  
-d : 목적지 패킷의 주소나 포트 입력  
-p : 프로토콜 입력  
-i : 입력 인터페이스 입력  
-o : 출력 인터페이스 입력  
-j : 규칙에 맞는 패킷의 처리를 어떻게 할지 입력(accept, drop..)  
-y : SYN 패킷 허용안함  

### IPTABLE Action 설정
ACCEPT : 패킷 허용  
DROP : 패킷 차단  
REJECT : 패킷을 버리고 적절한 응답 패킷 전송  
LOG : 패킷을 Syslog에 기록  
RETURN : 호출 체인 내에서 패키 처리를 계속함  

### IPTABLE 정책 설정 예시
1) 514(Syslog)포트에 대해 혀용 설정
*Iptable 설정 시 권한은 root 권한필요
```
#] iptables -I INPUT 1 -p udp --dport 514 -j ACCEPT   //514 포트에 대해 허용 설정과 동시에 규칙의 는 1번으로 설정
```

### IPTABLE 정책 설정 저장
정책 설정 후 리부팅이나 IPTABLE을 재시작하여도 정책이 남아있도록 저장
```
#] service iptables save
```


