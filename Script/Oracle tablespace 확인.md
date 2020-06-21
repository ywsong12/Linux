#### ORACLE 테이블스페이스 용량 확인
###### 각각의 테이블스페이스의 전체용량, 사용량, 남은량, 사용% 를 표로 표출
```
#!/bin/bash

sqlplus DISLIS/wjdqhqhdks  <<EOF   // <<EOF는 EOF(End of Escape가 나올때까지 명령을 실행하라는 것으로 없을시에는 오라클 접속이후 다음명령이 실행안됨.  
select substr(a.tablespace_name,1,30) tablespace, round(sum(a.total1)/1024/1024/1024,1) "Total(GB)",  
       round(sum(a.total1)/1024/1024/1024,1)-round(sum(a.sum1)/1024/1024/1024,1) "Use(GB)",  
       round(sum(a.sum1)/1024/1024/1024,1) "Free(GB)", round((round(sum(a.total1)/1024/1024,1)-round(sum(a.sum1)/1024/1024,1))/round(sum(a.total1)/1024/1024,1)*100,2) "Used%"  
from
      (select   tablespace_name,0 total1,sum(bytes) sum1,max(bytes) MAXB,count(bytes) cnt
       from     dba_free_space
       group by tablespace_name
       union
       select   tablespace_name,sum(bytes) total1,0,0,0
         from     dba_data_files
          group by tablespace_name) a
group by a.tablespace_name
order by tablespace;

exit
EOF
```
