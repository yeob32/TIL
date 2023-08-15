### Spring MVC
- Model View Controller
- 책임 분리하여 해당 모듈 개발에 집중 할 수 있게 해준다.

## Filter, Interceptor, AOP
- 순서
    - Filter → Interceptor → AOP → Interceptor → Filter
- Filter
    - spring context 외부에서 동작
    - 인코딩, XSS(Cross Site Scripting) 방어 등의 요청에 대한 처리
- Interceptor
    - spring context 내부에서 동작 (spring bean 접근 가능)
    - 권한, 로그인, 프로그램 실행시간 체크