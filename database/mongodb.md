# MongoDB

Document 기반 데이터베이스

### 특징

- Document
- BASE
    - ACID 대신 BASE 를 택하여 성능과 가용성을 우선시한다.
    - MongoDB 4.2 부터 Shard Cluster Transaction (분산트랜잭션) 제공
- Open Source

### ACID,BASE

- ACID
    - 데이터베이스 트랜잭션이 안전하게 수행된다는 것을 보장하기 위한 성질
- BASE
    - 가용성과 성능을 중요시하는 특성을 가진 분산시스템의 특성
    - **B**asically **A**valiable
        - 언제든지 사용할 수 있다. 가용성
    - **S**oft state
        - 외부의 개입이 없어도 정보가 변경될 수 있다.
        - 네트워크 파티션 등 문제가 발생되어 일관성이 유지되지 않는 경우 일관성을 위해 데이터를 자동으로 수정한다.
    - **E**ventually consistent
        - 일시적으로 일관적이지 않은 상태가 되어도 일정 시간 후 일관적인 상태가 되어야한다는 의미
        - 장애 발생 시 일관성을 유지하기 위한 이벤트 발생

### Document

- BSON 형태 (Binary JSON)
- 계층 구조
    - Database > Collection > Document > Field
- ObjectId
    - RDB 의 PK 같은 고유키
        - _id : PK
    - RDB 는 디비에서 직접 고유키를 부여하는 반면 ObjectId 는 클라이언트에서 생성한다.
    - 636f6d4d72a00506901b7a7d
    - 첫 4byte 는 UNIX Timestamp, 다음 5 byte 는 랜덤값, 마지막은 Auto Increment 값
- Secondary Index
    - Array, Embedded Document 내의 필드에도 인덱스 설정이 가능

### MongoDB Replica Set

### MongoDB 패턴

**Model Tree Structure**

**Model Relationships**

- RDB 와 마찬가지로 1:1, 1:N, N:M 구조로 구성 가능
- MongoDB 는 아래 두가지 방식 제공
    - 포함(Embedded)
        - 1:1, 1:N
        - Document 에 Object 로 데이터를 포함
        - 고려사항
            - 16MB 제한
            - 읽기 성능 향상(쿼리 한번으로 조회 가능)
            - 빈번한 업데이트, 크기가 증가하는 업데이트일 때는 권장하지 않음
    - 참조(Linked)
        - 1:N, N:M
        - Foreign Key 처럼 키를 이용하여 참조
        - N:M
            - 단방향 참조

            ```jsx
            [Categories 컬렉션]
            { "_id" : 1, "name" : "한식", "desc" : "불고기, 식혜 등" }
            { "_id" : 2, "name" : "분식", "desc" : "라면, 김밥 등" }
            { "_id" : 3, "name" : "음료", "desc" : "식혜,콜라,사이다 등" }
            
            [Products 컬렉션]
            {
              "_id" : 1001, "productname" : "김밥", "unitprice" : 2000, 
              "categoryid" : [ 1, 2 ]
            }
            {
              "_id" : 1002, "productname" : "식혜", "unitprice" : 3000, 
              "categoryid" : [ 1, 3 ]
            }
            ```

            - 양방향 참조

            ```jsx
            [Categories 컬렉션]
            { "_id" : 1, "name" : "한식", "desc" : "불고기, 식혜 등", productid : [ 1001, 1002 ] } 
            ......
            
            [ Products 컬렉션 ]
            { "_id" : 1001, "productname" : "김밥", "unitprice" : 2000, "categoryid" : [ 1, 2 ] }
            { "_id" : 1002, "productname" : "식혜", "unitprice" : 3000, "categoryid" : [ 1, 3 ] }
            ```

        - 고려사항
            - 복잡하지만 유연한 데이터 구조
            - 읽기 성능 저하, 데이터 일관성이 상대적으로 중요할 때
            - 데이터 크기 제한 없음
- **Embedded VS Linked**

  ![mongodb_modeling.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7d4fa530-3baa-45a5-90a3-25f9995e898d/mongodb_modeling.png)

- 목적에 따라 잘 사용할 것
    - 읽기 성능, 데이터 일관성, 쓰기 성능

### 마무리

- NoSQL 은 최대한 단순하게 사용하는 것이 옳은 방향
    - NoSQL 은 최대한 단순하면서 많은 데이터
    - RDB 는 복잡하면서 무결성이 중요한 데이터

### References

- https://kciter.so/posts/about-mongodb#fn-2
- https://blog.voidmainvoid.net/241