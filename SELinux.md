## SELinux(security Enhanced Linux)란?
### 보안을 강화하기위한 리눅스 커널 보안 모듈로서 강력한 정책으로 주체(사용자, 프로그램, 프로세스)와 객체(파일, 디바이스)를 제어하여 사용자가 프로그램을 사용할때 해당 프로그램을 작동시키기 위해 필요한 권한만 부여해주어 보안성을 높여준다.

### SELinux 모드 종류
enforcing : 정책을 적용(default로 설정됨)  
permissive : 정책은 적용하지 않고 정책 설정 시 발생되는 로그를 기록  
disable : 정책 사용 안함  


#### SELiux 적용해제
##### SELinux가 적용되어 있을 경우 DB같은 프로그램들에서 설정변경 등의 사용이 어려워 적용을 해제한다.(보안성이 높은 만큼 사용의 편의성이 떨어진다.)
##### 단, 이 경우 보안 측면에서는 다른 보안장비 보안정책을 사용하여 보안을 강화한다.
```
#] vi /etc/selinux/config        //SELinux 설정파일 편집
SELINUX=disabled                 //다음 항목에서 enforcing을 disabled 로 변경
#] reboot                        //재부팅하여 적용(적용 시 재부팅필요)
