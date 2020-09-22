# 읭

## Refactoring
- if 문이 많으면 클래스가 두 가지 이상의 책임을 담당하고 있다는 신호 -> 가독성 하락 및 단위테스트 만들기 어려움
    - 추상화 필요한 시점이 아닌지 고민 필요 
- null 을 리턴하는 로직이 많아질수록 테스트가 어려워짐
    - null object 패턴 또는 Optional 사용 고려
        - null object 패턴
            - 우리는 함수가 실패한 경우에도 항상 유효한 객체를 반환한다는 것을 보장
            - 실패를 나타내는 객체들은 `아무일도` 하지 않는다.  

### Java features
- https://www.techgeeknext.com/java/java17-features
- shadowJar

### session-clustering
- 세션 관리 서버가 따로 있다는 가정
    - 세션 서버 먹통이 되면?
- redis
    - sentinel 구성하여 감시
- hazelcast 
    - was 간 동일한 데이터 유지
    
    
### tcpdump
- sudo tcpdump host 127.0.0.1