# Java JVM

### Java Runtime 구성 요소
- JVM
- JRE
    - JVM(Java Virtual Machine) + Library
- JDK
    - JRE(Java Runtime Environment) + Development Kit
    
### Java 실행 과정
1. Java 소스 작성
2. Java Compiler ( javac ) 에 의해 Byte Code 로 변환 ( .class )
3. ClassLoader 가 class 파일을 로드하여 JVM (Runtime Data Area) 메모리 영역 할당 ( 런타임 )
4. Execution Engine 에 의해 메모리에 적재된 클래스(byte code) 들을 기계어로 변경해 명령어 단위로 실행

## JVM
![jvm](http://coding-geek.com/wp-content/uploads/2015/04/jvm_overview.jpg)
![jvm2](https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/images/gcslides/Slide1.png)

## JVM 구성 요소
- Class Loader
- Execution Engine
- Runtime Data Area
- Native

## Class Loader
### Java 8 기본 클래스 로더
- 부트스트랩 클래스 로더 (Bootstrap Class Loader)
    - 최상위 클래스 로더
    - `jre/lib/rt.jar` 에 담긴 JDK 클래스 파일 로딩 
    - Native 코드로 구현 되어 있다.
- 확장 클래스 로더 (Extention Class Loader)
    - `jre/lib/ext` 경로에 위치한 확장 클래스 파일 로딩
- 애플리케이션 클래스 로더 (Application Class Loader)
    - -classpath(또는 -cp) 경로에 위치한 클래스를 로딩
    - 개발자가 애플리케이션 구동을 위해 직접 작성한 대부분의 클래스는 해당 클래스로더에 의해 로딩
    
### 계층적 구조
- 부모-자식 관계의 계층적 구조를 가진다.

## Execution Engine
- 런타임 데이터 영역에 배치된 바이트코드를 명령어 단위로 실행
    - 인터프리터 
        - 바이트코드 명령어를 하나씩 읽어서 실행 
        - 하나씩 해석하고 실행되기 때문에 하나하나의 해석은 빠르지만 전체적인 결과는 느림
    - JIT (Just In Time)
        - 바이트코드 전체를 컴파일해 네이티브 코드로 변경하고, 이후에 해당 메서드를 더 이상 인터프리팅하지 않고 네이티브 코드로 직접 실행
    - 딱 한번만 실행되는 코드라면 컴파일 보단 인터프리팅이 좋다. 


## Runtime Data Area
- JVM 프로그램이 실행되어 운영체제에서 할당받은 메모리 영역
![runtime-data-area](http://coding-geek.com/wp-content/uploads/2015/04/jvm_memory_overview.jpg)

- Method Area (= Class Area, Code Area, Static Area)
    - 클래스,변수,메서드,static 변수, 상수 정보 저장되는 영역 (모든 쓰레드 공유)
- Heap Area
    - 동적할당된 `인스턴스`,`배열`들이 저장되는 영역, gc의 주대상 (모든 쓰레드 공유)
- Stack Area
    - Heap영역에 생성된 Object 타입의 참조 값을 할당하고 해당 타입의 원시타입 데이터 할당
    - 메서드에서 사용하는 정보들이 저장되는 영역
    - 각 스레드는 자신만의 스택을 가진다.
    - 메서드 호출 시 생성되었다가 완료 시 사라진다. LIFO ( 스레드 별로 하나씩 생성 → Thread Safe )
- PC registers
    - 현재 실행 중인 JVM 명령의 주소 저장
- Native Method stack
    - C / C++ 메서드 호출을 위해 할당 되는 영역으로 각 언어에 맞게 스택 형성 
    - native 키워드



## References
- https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html
- http://coding-geek.com/jvm-memory-model/