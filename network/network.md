# Network

### TCP, UDP
> 데이터 전송 프로토콜

- **UDP (User Datagram Protocol)**
    - 비연결형 프로토콜로써 흐름 제어,오류 제어,재전송 없음
    - 높은 속도(TCP 보다 빠름)
    - 클라이언트와 서버간 1:1, 1:N, M:N 통신
- **TCP (Transmission Control Protocol)**
    - 연결 지향 프로토콜로써 신뢰성 과 순서 보장(흐름 제어, 혼잡 제어)
    - 3-way handshaking 과정을 통해 연결을 설정하고 4-way handshaking을 통해 해제
    - 클라이언트와 서버간 1:1 통신

### TCP 3-way Handshake 와 4-way Handshake

- **연결 성립 (Connection Establishment) - 3-way Handshake**
    - 클라이언트가 서버에 접속 요청 패킷 SYN(a) 을 전송
    - 서버는 요청 SYN(a) 을 받고 해당 요청을 수락한다는 패킷 ACK(a+1), SYN(b) 을 전송
    - 클라이언트는 서버의 수락 응답인 ACK(a+1), SYN(b) 패킷을 받고 ACK(b+1) 을 서버로 보내면 연결이 성립됨(establish)
- **연결 해제 (Connection Termination) - 4-way Handshake**
    - 클라이언트가 연결 종료 요청 FIN 플래그을 보냄
    - 서버는 클라이언트 연결 종료 요청 FIN 플래그 을 받고 ACK 전송
    - 서버는 데이터 전송을 완료하고 클라이언트에게 연결을 종료하겠다는 FIN 플래그 전송
    - 클라이언트는 FIN 플래그를 확인 후 ACK 전송
    - 서버는 ACK 메세지를 받은 후 소켓 연결 Close

### HTTP, HTTPS
> 클라이언트와 서버 간의 자원 전송을 위한 통신 규약

- HTTP 은 평문 통신
- HTTPS 는 암호화
  - SSL(Secure Socket Layer) 프로토콜 이용하여 정보 암호화
  - 평문 통신에 비해 암호화 통신은 리소스 소비가 큼 (HTTP2 에서는 HTTPS 가 더 빠르다네)

### HTTP의 GET, POST

- **POST**
    - HTTP Request Body 에 데이터를 담아서 전송하고, 보안 면에서 이점이 있으나 크지 않음
- **GET**
    - 가져오기, POST 는 보내기 의 용도로 구분하여, 브라우저에서 캐시가 가능함

## OSI 7 Layer


## Proxy
- 클라이언트와 서버간의 중계 서버, 통신을 대리 수행하는 서버
- 특징
    - 캐싱: 클라이언트가 요청한 내용을 캐싱
        - 네트워크 통신 비용 감소 -> 응답 속도 향상
    - 필터: 프록시 서버를 거치는 요청 및 응답 확인
        - 보안성 향상
        - 프록시를 통한 모든 응답/요청 로깅
    - 트랜스코더: 프록시 서버로 넘어온 데이터 조작 (데이터 압축, 언어 변환 등)
        - 압축으로 인한 통신 비용 감소
        - 원래 서버의 역할 감소
    - 익명성: HTTP 식별 정보 헤더를 제외할 수 있다.
        - 보안성 향상

## Forward Proxy / Reverse Proxy
> Clients <-> Forward proxy <-> internet <-> Reverse Proxy <-> Servers
### Forward Proxy
- 보통 프록시가 이거임
    - 기업 망에서 특정 사이트 url 접근 못하게 할 때 (근무 중 인스타그램 접근 할 수 없어 !)

### Reverse Proxy
- 일반적인 WEB(Apache, nginx) - WAS(Tomcat)분리 형태
- 특징
    - DMZ: 보통 기업의 네트워크환경에서는 DMZ 라고 부르는 내부/외부 네트워크 사이에 위치하는 구간이 존재
        - 메일 서버, 웹 서버, FTP 서버 등 외부 서비스를 제공하는 서버가 위치 -> 서비스(WAS) 서버는 내부망에 위치
        - 일반적인 서비스 구조, 보안상 아주 중요
            - 물론 DMZ 구간에 WAS 위치해도 되지만 아주 위험 (WAS 해킹 -> DB 해킹 -> 끔찍)
    - Load Balancing (L4): 부하분산
        - 여러 대의 서버가 요청을 분산 처리할 수 있도록 나눠줌

## 프록시 서버를 통한 무중단 배포
- request -> Nginx(proxy) -> WAS 1, WAS 2
    - Nginx 요청 포인트를 WAS 1,2 로 자유롭게 변경 가능

