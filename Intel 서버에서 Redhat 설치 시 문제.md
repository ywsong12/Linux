### Intel 서버에 RedHat S를 올려 사용 시 화면이 나오지 않을 경우
#### Intel 서버에 RedHat OS를 설치하면 설치과정에서 검은 화면만 표출되고 다음화면으로 넘어가지 못하는 현상이 있다.
#### 원인은 인텔서버보드와 RedHat OS의 비호환성 문제로 발생되는 현상이라고 한다. 그외 IPMI pantsdown 보안 수정으로 인해 OS 설치 시 AST Driver가 로드가 되지 않는다.
##### *조치 방안
1. 부팅 후 OS 설치 초기 화면에서 'Tab' 클릭
2. 커맨드 입력창 이동 후 다음 명령어 추가 후 'Enter' 입력
    - 'nomodeset xdriver=vesa brokenmodules=ast'
3. 다음 화면넘어가며 정상 설치 진행되는지 확인

