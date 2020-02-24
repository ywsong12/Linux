## SSH 키 생성 및 암호없이 자동 로그인
클라이언트에서 진행  
```
#] ssh-keygen -t rsa  //rsa 암호화로 키를 생성
Enter file in which to save the key (/root/.ssh/id_rsa) :   //저장경로에 대한 설정 입력란으로 경로설정없이 엔터 시 기본 저장 경로(접속한 계정 .ssh 파일 밑)로 저장됨.
Enter passphrase (empty for no passphrase):                 //암호 입력란으로 자동으로 로그인 시에는 입력없이 엔터(보안상 문제점이 될 수 있음)
#] ll .ssh                         //.ssh 리스트를 확인하여 id_rsa, id_rsa_pub 파일이 생성되었는지 확인
id_rsa
id_rsa_pub    
```
생성된 id_rsa_pub 파일 안에 내용을 복사하여 접속할 서버의 계정 밑 .ssh/authorized_keys 파일에 붙여넣는다.(authorized_keys없으면 파일 생성)  
이후 클라이언트에서 암호없이 접속이 되는지 확인.
#### 암호를 통한 접속은 막고 ssh 키 접속만 가능하게 설정하는 방법
```
#] vi /etc/ssh/sshd_config
PermitRootLogin without-password        //다음 내용을 추가하거나 PermiRootLogin yes 부분을 변경
#] systemctl restart sshd               //ssh 데몬 재시작하여 적용
```

※ .ssh 파일은 보안상 중요 파일이기에 해당 디렉토리 및 아래 파일들의 적절한 권한 부여가 필요
