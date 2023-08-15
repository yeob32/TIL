# Java Exception
- 프로그램 실행 중 발생, 프로그램 명령의 정상적인 흐름을 방해하는 이벤트

## Java Exception Hierarchy
![exception-hierarchy](https://2.bp.blogspot.com/--f8P24mVPK0/W3v8Qq2JzrI/AAAAAAAADSA/PR-7hjBxP1QPhzc5UsYyZBgFseJ7QM2XgCLcBGAs/s1600/exception-handling.png)

- Throwable
    - 모든 Exception 및 Error 의 슈퍼 클래스
- Error
    - Throwable 의 하위 클래스
    - 시스템에 비정상적인 상황 시 발생
- Exception
    - Throwable 의 하위 클래스
    - 개발자 레벨에서 해당 예외에 대한 처리
- RuntimeException
    - Exception 의 하위 클래스
    - API의 잘못된 사용을 나타내는 예외
        - ex) NullPointerException: null 참조를 통해 객체의 멤버 접근 시 발생
            

## Checked Exception vs Unchecked Exception
- Checked Exception
    - 명시적 예외 처리
        - 예외 처리 상위 클래스로 위임 (throws)
        - (try ~ catch)
    - 컴파일 단계에서 체크 가능
    - `RuntimeException` 제외 `Exception` 의 하위 클래스
- Unchecked Exception
    - 명시적 예외 처리 x
    - 런타임 단계에서 확인
    - `RuntimeException` 의 하위 클래스
    
## Exception vs Error
- Exception
    - 개발자가 예외에 대한 처리 가능
- Error
    - Error 발생 시 복구가 불가능한 상황
    - ex
        - OutOfMemoryError : JVM 메모리 부족 시 발생
        - StackOverflowError : 스레드의 스택 공간이 부족할 떄 발생
        - ExceptionInInitializerError : 정적 초기화 시 예기치 못한 예외 발생
        - NoClassDefFoundError : 필요한 클래스 파일이 클래스 경로에 없어 클래스 로더가 클래스 로드 실패 시 발생
    
## References
- https://dzone.com/articles/java-exception-handling-interview-questions-and-an-1