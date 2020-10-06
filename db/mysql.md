# MySql

## MySql 구조
* 서버 엔진 : 클라이언트(또는 사용자)가 Query를 요청했을때, Query Parsing과, 스토리지 엔진에 데이터를 요청하는 작업을 수행.                                      
* 스토리지 엔진 : 물리적 저장장치에서 데이터를 읽어오는 역할을 담당.

### 대표 스토리지 엔진
* InnoDB : 따로 스토리지 엔진을 명시하지 않으면 default 로 설정되는 스토리지 엔진이다. InnoDB는 transaction-safe 하며, 커밋과 롤백, 그리고 데이터 복구 기능을 제공하므로 데이터를 효과적으로 보호 할 수 있다.
InnoDB는 기본적으로 row-level locking 제공하며, 또한 데이터를 clustered index에 저장하여 PK 기반의 query의 I/O 비용을 줄인다. 또한 FK 제약을 제공하여 데이터 무결성을 보장한다.
* MyISAM : 트랜잭션을 지원하지 않고 table-level locking을 제공한다. 따라서 multi-thread 환경에서 성능이 저하 될 수 있다. 특정 세션이 테이블을 변경하는 동안 테이블 단위로 lock이 잡히기 때문이다.
텍스트 전문 검색(Fulltext Searching)과 지리정보 처리 기능도 지원되는데, 이를 사용할 시에는 파티셔닝을 사용할 수 없다는 단점이 있다.
* Archive : '로그 수집'에 적합한 엔진이다. 데이터가 메모리상에서 압축되고 압축된 상태로 디스크에 저장이 되기 때문에 row-level locking이 가능하다.
다만, 한번 INSERT된 데이터는 UPDATE, DELETE를 사용할 수 없으며 인덱스를 지원하지 않는다. 따라서 거의 가공하지 않을 원시 로그 데이터를 관리하는데에 효율적일 수 있고, 테이블 파티셔닝도 지원한다. 다만 트랜잭션은 지원하지 않는다.

### InnoDB
* 대용량 데이터 컨트롤 필요 시
* 트랜잭션 관리 및 복구 필요 시
* 정렬 구문 필요 시
* IUD 등이 빈번하게 발생하는 경우 (Row-Level-Rocking 때문)

### MyISAM
* 읽기 위주 작업 시
* 전문 검색 필요 시
* 트랜잭션 및 복구 x
* 한번에 대량의 데이터를 입력하는 배치성 테이블

## 이슈
### public key retrieval is not allowed
    - allowPublicKeyRetrieval=true&useSSL=false
    - mysql 8.x 버전 이후로 발생
### ERROR 3730 (HY000)
```
ERROR 3730 (HY000): Cannot drop table 'account' referenced by a foreign key constraint 'FKfh5cx2k6kh8rpb9l5t0a24xxi' on table 'coupon'.

$ SET FOREIGN_KEY_CHECKS=0; 
$ DROP TABLE bericht; 
$ SET FOREIGN_KEY_CHECKS=1;
```

### 참고
* http://asuraiv.blogspot.com/2017/07/mysql-storage-engine.html
* https://needjarvis.tistory.com/45