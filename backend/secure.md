# Secure

## 암호화

- 단방향 암호화
    - 해시 함수
    - SHA, MD5
- 양방향 암호화
    - 대칭키 암호화
        - 암복호화 시 동일 암호 키 사용, 노출되면 위험
        - AES,DES 등
    - 비대칭키 암호화
        - private key, public key 로 이루어진 서로 다른 한쌍의 암호 키
        - RSA,DSA 등
        - SSH Key → id_rsa(비밀키),id_rsa.pub(공개키)

## 시큐어 코딩

## 개요
- 웹사이트의 취약점을 이용하여 사용자가 의도치 않은 요청을 통한 공격

## CORS (Cross Origin Resource Sharing)
- 허용되지 않은 Domain(protocol, host, port)의 요청을 제한함

### SOP (Same-Origin Policy)
- 오리진 사이의 리소스 공유에 제한을 걸어 위험요소 방지
    - XSS
    - CSRF
    
### 요청 허가 방법
- Access-Control-Allow-Origin response 헤더 추가

## XSS (Cross Site Scripting)
- 사용자가 의도치 않은 스크립트를 이용한 공격
- 대부분의 해킹 기법과는 다르게 클라이언트 대상 공격

### 해결 방안
- 유저가 입력한 값의 검증을 서버 측에서 수행
- 요청 값에 포함된 HTML 코드 치환 

## CSRF (Cross Site Request Forgery)
- 크로스 사이트 요청 위조
- 로그인한 피해자의 브라우저를 통해 세션,쿠키 또는 기타 다른 인증정보가 포함된 변조된 HTTP 요청을 전송하여 정상적인 요청

### 해결 방안
- CSRF 토큰 사용 (ex Spring Security)
- 사용자와 상호 처리 기능 적용
- 재인증 요구

## XSS vs CSRF
- 공격대상
    - XSS -> Client 
        - 사이트 변조, 백도어를 통해 클라이언트 공격
    - CSRF -> Server (세션,쿠키 등)
        - 요청을 위조하여 사용자의 권한 도용 
        
## SQL Injection
- 외부입력값을 동적으로 SQL실행문을 만들어서 사용할때 주로 나타남.

### 해결 방안
- 유저에게 받은 값을 그대로 넘기지 않는다.
- 클라이언트측에서 값을 입력받을 때 regex 등으로 검증하여 입력받는다.
- 서버측에서 클라이언트에서 넘어온 값을 regex 등으로 검증하여 입력받는다.