# Java Garbage Collection
> Heap 영역의 오브젝트 중 Stack 영역에서 도달 불가능한(Unreachable) 오브젝트들은 GC의 대상이 된다.

### Stop-The-World
- GC 를 실행하기 위해 JVM 이 애플리케이션을 멈춤
- stop-the-world 가 발생하면 GC 스레드를 제외한 모든 스레드 중지
- GC 작업을 완료한 후 중단했던 작업 다시 시작, 어떤 GC 알고리즘이든 stop-the-world 발생 
- GC 튜닝이란 stop-the-world 실행 시간을 줄이는 것

> ### 약한 세대 가설 (weak generational hypothesis)
> - 대부분의 객체는 금방 접근 unreachable 상태가 된다.
> - 오래된 객체에서 젊은 개체로의 참조는 아주 적게 존재한다.

### Hotspot Heap Structure
- Young 영역 
    - 새로 생성된 객체는 대부분 여기 위치하며 대부분 생성되었다가 금방 접근 불가능한 상태가 된다.
    - (참조가 제거된다) 이 영역에서 객체가 사라질 때 Minor GC
- Old 영역 
    - Young 영역에서 접근 불가능 상태가 되지 않고 살아남은 객체가 여기로 복사된다. 
    - Young 영역보다 메모리를 크게 할당하고 크기가 큰 만큼 Young 영역보다 GC가 적게 발생 Major GC( Full GC )
    - Eden 영역에 최초로 객체가 만들어지고, Survivor 1, 2 영역을 통해서 Old 영역으로 오래 살아남은 객체가 이동한다는 사실은 꼭 기억하기 바란다.
- Permanent 영역 (Method Area) 
    - 객체가 영구히 남아 있는 곳은 아님, 여기서도 Full GC 발생
    - Java 1.8 이후 Metaspace 영역으로 대체
        - Permanent Generation Area 에 저장되는 static 인스턴스, 리터럴 문자열을 Heap 으로 옮겨 GC 대상이 되도록했다.
        - 클래스, 메소드, 메타정보는 Metaspace 로 이동 
- Metaspace 영역
    - 클래스, 메소드, 메타정보 

### GC
```
Young Generation 
Eden, Survivor0, Survivor1
새로운 오브젝트는 Eden 영역에 할당된다.  Eden 영역이 메모리가 가득차면 Minor GC 발생 
Reachable 객체는 S0 영역으로 이동한다.
다음 Minor GC 발생 시 S0 영역의 Reachable 오브젝트는 S1 영역으로 이동하고 age 값 증가
Eden, S0 의 Unreachable 오브젝트는 모두 클리어 
다음 Minor GC 발생 시 S1 의 살아남은 오브젝트는 다시 S0으로 이동
Survivor 영역 하나는 반드시 비워져있어야 한다.
age 특정 값 초과 시 Old Generation 으로 이동 (프로모션)
Old 영역 풀되면 Major GC (Full GC) 발생
```

### Mark & Sweep
> GC 과정을 Mark & Sweep 이라고도 한다.
- Reachable 객체를 마킹하고 마킹이 안된 객체들을 지운다(Sweep:쓸다).
- 마킹 작업 시 모든 스레드 중단 ( stop-the-world )
- Mark 
    - 살아있는 객체, 즉 GC 대상이 아닌 객체를 식별하는 역할
- Sweep
    - Heap 의 앞 부분부터 mark된 객체를 제외하고 제거
- Compact
    - Sweep 이후 비어있는 Heap 공간들을 연속되게 쌓이도록 Heap 의 앞부분부터 채우는 과정


### GC 종류
- Serial GC
    - -XX:+UseSerialGC
    - 적은 메모리와 CPU 코어 개수가 적을 때 적합
    - MinorGC, MajorGC 모두 순차적으로 수행
    - Mark-Sweep-Compact
- Parallel GC
    - -XX:+UseParallelGC
    - Serial GC 와 기본적인 알고리즘은 같지만 여러개의 멀티스레드로 처리
    - 여러 CPU를 효과적으로 활용하기 위해 GC수행시 멀티스레드를 사용. 
    - Default로 young generation에서만 멀티스레드를 활용하나, 옵션을 통해 old generation에서도 멀티스레딩 활용가능. 
    - Mark-Sweep-Compact
- CMS(Concurrent Mark Sweep) Collector
    - -XX:+UseConcMarkSweepGC
    - 가비지 컬렉션 작업을 애플리케이션 스레드와 동시 수행. 
    - stop-the-world시간 최소화. 
    - Compacting 수행하지 않아서 memory를 더 많이 차지.
        - 초기 STW를 줄일 수 있지만, 장기적으로는 ....
- G1 Garbage Collector
    - -XX:+UseG1GC
    - Java7부터 사용가능. 
    - 여러 CPU와 아주 큰 memory에서 효과적인 GC를 활용하기 위함. 
    - Oracle문서에 따르면 heap size가 6GB보다 클 경우 GC의 latency를 0.5sec이하로 낮출수 있다고 한다.
    - (Oracle G1 GC문서) Java9에서는 default GC로 설정되어 있다.(이전까지는 Parallel GC가 default)

### GC 튜닝
- CUI
    - jstat, -verbosegc (jvm 옵션, 시작 시 옵션 설정, 런타임 확인)
- GUI
    - VisualVM + Visual GC