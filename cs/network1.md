# Network

### HTTP / HTTPS (Application Layer)
> 클라이언트와 서버 간의 자원 전송을 위한 통신 규약

* HyperText Transfer Protocol Secure
* SSL(Secure Socket Layer) 프로토콜 이용하여 정보 암호화
* 평문 통신에 비해 암호화 통신은 리소스 소비가 큼 (HTTP2 에서는 HTTPS 가 더 빠르다네)

### TCP / UDP (Transport Layer)
> 데이터 전송 프로토콜

* TCP (Transmission Control Protocol)  
    - 연결형 서비스로 가상 회선 방식(패킷 교환) 사용
    - 3-way handshaking 과정을 통해 연결을 설정하고 4-way handshaking을 통해 해제
    - 높은 신뢰성(흐름 제어, 혼잡 제어)
    - 클라이언트와 서버간 1:1 통신

* UDP (User Datagram Protocol)  
    - 비연결형(정보를 보내거나 받는 절차 없음) 서비스로 데이터그램 방식(패킷 교환) 제공
    - 낮은 신뢰성
    - 높은 속도
    - 클라이언트와 서버간 1:1, 1:N, M:N 통신

### HTTP / TCP

* HTTP  
    - 단방향 통신 (클라이언트가 요청을 보내는 경우 서버가 응답, 응답 완료 후 연결 종료)

* Socket  
    - 양방향 통신 (클라이언트와 서버가 특정 포트를 통해 연결)
    - 실시간 데이터 통신 시 용이 (동영상 스트리밍, 온라인 게임)

### 참고
* https://12bme.tistory.com/297?category=734721
* https://kgh940525.tistory.com/entry/CS-part2%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC
* https://yamalab.tistory.com/73
* https://mangkyu.tistory.com/15



