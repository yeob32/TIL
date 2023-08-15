# MySQL Operation

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
- http://asuraiv.blogspot.com/2017/07/mysql-storage-engine.html
- https://needjarvis.tistory.com/45