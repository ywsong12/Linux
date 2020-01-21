## 다른 서버의 특정 DB데이터를 나의 서버에 파일로 생성하기
### 다른 IP의 서버에 있는 DB에서 데이터를 가져와 파일로 생성할때 사용(가져오고자하는 서버의와 서로다른 DB를 사용한다면 ODBC를 사용하여야함)
#### 아래 스크립트 생성시에는 해당 접속 DB의 컬럼정보들을 사전에 알아야하며, 데이터를 계속 불러올 경우에는 중복을 없애기위해 시간값을 조건으로 하여 데이터를 가져와야한다.
#### 즉, 시간값을 비교하는 것으로 여기서 나는 DB데이터 포맷에 시간값이 있어서 해당 시간값만 따로 파일로생성하고 데이터를 가져올 때마다 생성된 시간값이 들어간 파일과 비교하여 해당 시간보다 이후에 들어온 데이터만 받도록 설정
```
#] vi test.sh           // DB 접속 후 데이터파일을 가져와 파일로 만들기 위한 스크립트 생성
#!/bin/bash

today=$(date +"%Y%m%d")              

#fi /home/disiem/dblink/qost.dat  ---> dt
qost=$(<qost.dat)
echo "$qost"

mysql -u disiem -pQWer1234! qos -e "select concat('172.24.130.111 ','|',ACTION_DATETIME,'|',ACTION_DETAIL,'|',USER_ID,'|',USER_IP) from V_T_HIST_LOG where ACTION_DATETIME > '$qost'" -N >> /home/disiem/dblink/QoS/LOG_QOS_$today.dat
echo "select * from V_T_HIST_LOG where ACTION_DATETIME > '$qost'"


mysql -u disiem -pQWer1234! qos -e "select max(action_datetime) from V_T_HIST_LOG" -N > /home/disiem/dblink/qost.dat

#] chmod 755 test.sh        // 실행 권한 주기
```
