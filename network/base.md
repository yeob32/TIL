## HTTP / HTTPS
> 클라이언트와 서버 간의 자원 전송을 위한 통신 규약
- 평문 통신 -> 도청 가능 -> 암호화 필요 SSL(Secure Socket Layer)
- HTTP + SSL 즉, TCP 소켓 통신 부분을 SSL 프로토콜로 대체
	- HTTP -> SSL -> TCP
- 암호화 리소스 비용
> Http2.0 에서는 Http 보다 Https 가 더 빠르다고 한다.

### TLS (Transport Layer Security) = SSL (Secure Socket Layer) = SSL/TLS
- Cipher Suite
	- TLS 암호통신 시 필요한 알고리즘 집합
	- RSA
		- 공개키 암호화 방식
		
## TCP / UDP
TCP (Transmission Control Protocol)
- 연결형 서비스 (3-way hands shake) <-> 해제시 (4-way hands shake)
- 높은 신뢰성(흐름 제어, 혼잡 제어)
- 멀티캐스팅이나 브로드캐스팅 지원 안함
- 1:1 통신

UDP (User Datagram Protocol)
- 비연결형 서비스
- 속도 빠름
- 1:N 통신		

- 비연결형(정보를 보내거나 받는 절차 없음) 서비스로 데이터그램 방식(패킷 교환) 제공
    - 낮은 신뢰성
    - 높은 속도
    - 클라이언트와 서버간 1:1, 1:N, M:N 통신