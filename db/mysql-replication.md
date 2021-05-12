# MySQL Replication

## Database Replication

- 한 DB 서버의 데이터를 다른 DB 서버들에 복제하는 기술
- master 서버는 쓰기 연산을 담당
- slave 서버는 읽기 연산을 담당
- slave 서버를 여러 대 두고 읽기 연산 분산 시켜 서버의 부하를 줄일 수 있다.

### Docker container

```yml
# docker-compose.yml

version: "3" # 파일 규격 버전
services: # 이 항목 밑에 실행하려는 컨테이너 들을 정의
  mysql-master: # 서비스 명
    image: mysql:8.0.17 # 사용할 이미지
    container_name: mysql-master # 컨테이너 이름 설정
    ports:
      - "13306:3306" # 접근 포트 설정 (컨테이너 외부:컨테이너 내부)
    environment: # -e 옵션
      MYSQL_ROOT_PASSWORD: "1234" # MYSQL 패스워드 설정 옵션
    command: # 명령어 실행
      - --character-set-server=utf8mb4
      - --collation-server=utf8mb4_unicode_ci
    restart: "always"
    volumes:
      - /Users/ksy/dockers/mysql/master/cnf:/etc/mysql/conf.d
    #  - /Users/ksy/datadir:/var/lib/mysql # -v 옵션 (다렉토리 마운트 설정)
  mysql-slave:
    image: mysql:8.0.17
    container_name: mysql-slave
    ports:
      - "23306:3307"
    environment:
      MYSQL_ROOT_PASSWORD: "1234"
    command:
      - --character-set-server=utf8mb4
      - --collation-server=utf8mb4_unicode_ci
    restart: "always"
    links:
      - mysql-master
    volumes:
      - /Users/ksy/dockers/mysql/slave/cnf:/etc/mysql/conf.d
```

```txt
# /Users/ksy/dockers/mysql/master/cnf

[mysqld]
log-bin=mysql-bin
server-id=1

# /Users/ksy/dockers/mysql/slave/cnf

[mysqld]
server-id=2
```

```bash
$ docker-compose up -d
```

#### REPLICATION 계정 생성

- master 서버에 REPLICATION SLAVE 권한의 계정 생성

```bash
mysql> CREATE USER 'ksy-repl'@'%' IDENTIFIED WITH mysql_native_password BY '1234';
mysql> GRANT REPLICATION SLAVE ON *.* TO 'ksy-repl'@'%';
```

#### test db 생성

```bash
mysql> CREATE DATABASE testdb;
mysql> USE testdb;
mysql> CREATE TABLE test ( no INT(8), PRIMARY KEY (no) );
mysql> DESC test;
```

#### master db dump

```bash
$ docker exec -it mysql-master /bin/bash
$ mysqldump -uroot -p testdb > dump.sql

# container -> local
$ docker cp mysql-master:/root/dump.sql .
```

#### dump.sql -> slave db

```bash
# local -> container
$ docker cp dump.sql mysql-slave:/root
$ docker exec -it mysql-slave /bin/bash
$ mysql -uroot -p

mysql> CREATE DATABASE testdb;

$ mysql -uroot -p testdb < dump.sql

// 덤프 확인
```

#### slave -> master 연동

```sql
# mysql-master
mysql> show master status\G

************\*\*\************* 1. row ************\*\*\*************
File: mysql-bin.000003
Position: 1382
Binlog_Do_DB:
Binlog_Ignore_DB:
Executed_Gtid_Set:
1 row in set (0.00 sec)
```

- `File` : 바이너리 로그 파일명
- `Position` : 현재 로그의 위치

```sql
# mysql-slave
mysql> CHANGE MASTER TO MASTER_HOST='mysql-master', MASTER_USER='ksy-slave', MASTER_PASSWORD='1234', MASTER_LOG_FILE='mysql-bin.000003', MASTER_LOG_POS=3141;
mysql> START SLAVE; ### 종료 시 STOP SLAVE;
```

- `MASTER_HOST` : 호스트명
- `MASTER_USER` : master 서버의 REPLICATION SLAVE 권한을 가진 계정
- `MASTER_PASSWORD` : master 서버의 REPLICATION SLAVE 권한을 가진 계정 비밀번호
- `MASTER_LOG_FILE` : master 바이너리 로그 파일명
- `MASTER_LOG_POS` : master 현재 로그의 위치

#### 연동 확인

```sql
mysql> SHOW SLAVE STATUS\G

# Last_Error, Last_IO_Error 필드 에러 유무 확인
************\*\*\************* 1. row ************\*\*\*************
Slave_IO_State: Waiting for master to send event
Master_Host: mysql-master
Master_User: ksy-slave
Master_Port: 3306
Connect_Retry: 60
Master_Log_File: mysql-bin.000003
Read_Master_Log_Pos: 3141
Relay_Log_File: f8733451ebba-relay-bin.000002
Relay_Log_Pos: 322
Relay_Master_Log_File: mysql-bin.000003
Slave_IO_Running: Yes
Slave_SQL_Running: Yes
Replicate_Do_DB:
Replicate_Ignore_DB:
Replicate_Do_Table:
Replicate_Ignore_Table:
Replicate_Wild_Do_Table:
Replicate_Wild_Ignore_Table:
Last_Errno: 0
Last_Error:
Skip_Counter: 0
Exec_Master_Log_Pos: 3141
Relay_Log_Space: 537
Until_Condition: None
Until_Log_File:
Until_Log_Pos: 0
Master_SSL_Allowed: No
Master_SSL_CA_File:
Master_SSL_CA_Path:
Master_SSL_Cert:
Master_SSL_Cipher:
Master_SSL_Key:
Seconds_Behind_Master: 0
Master_SSL_Verify_Server_Cert: No
Last_IO_Errno: 0
Last_IO_Error:
Last_SQL_Errno: 0
Last_SQL_Error:
Replicate_Ignore_Server_Ids:
Master_Server_Id: 1
Master_UUID: 8e01189b-b261-11eb-b118-0242ac130002
Master_Info_File: mysql.slave_master_info
SQL_Delay: 0
SQL_Remaining_Delay: NULL
Slave_SQL_Running_State: Slave has read all relay log; waiting for more updates
Master_Retry_Count: 86400
Master_Bind:
Last_IO_Error_Timestamp:
Last_SQL_Error_Timestamp:
Master_SSL_Crl:
Master_SSL_Crlpath:
Retrieved_Gtid_Set:
Executed_Gtid_Set:
Auto_Position: 0
Replicate_Rewrite_DB:
Channel_Name:
Master_TLS_Version:
Master_public_key_path:
Get_master_public_key: 0
Network_Namespace:
1 row in set (0.00 sec)

# 동기화 동작 확인
insert into test values(2);
```
