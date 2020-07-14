# encoding (ASCII, Unicode)

### 준비
```
컴퓨터 기본 저장 단위 -> 1byte
1byte -> 8bits
1bit -> 2진수
2^8 -> 256 개의 고유한 값 저장
```

### 인코딩
- 문자나 기호들의 집합을 컴퓨터에서 저장하거나 통신에 사용하기 위해 부호화 하는 방법
### 인코딩 방식
- 문자 집합: 정보를 표현하는 글자 집합 (ASCII, Unicode)
- 문자 인코딩 형태: UTF-8 과 같이 유니코드를 8비트의 숫자집합으로 나타냄

### ASCII
- 128개의 문자 집합을 제공하는 7bit 부호
- ascii -> 2^7 , 나머지 1bit -> 통신 에러 검출용 (Parity Bit)

### Unicode
- 모든 문자를 하나의 통일된 문자집합 ( Character set )으로 표현하기 위해 만든 코드
- UTF-8, UTF-16 등
  - UTF-8: 한글 3byte, 영어,숫자 1byte, 문자 크기가 달라서 다루기 어려움 (가변크기)
  - UTF-16: 1byte로 표현되는 영어, 숫자가 2byte 고정크기로 표현되어 용량이 커지는 단점
  > 인터넷 통신 시 전송 속도 중요해 문서의 크기가 작을수록 유리
  
### 참고
- https://whatisthenext.tistory.com/103
- https://lovefor-you.tistory.com/173
