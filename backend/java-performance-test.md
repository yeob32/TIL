# Java Performance Test

## 성능 테스트

### 목적

- 서비스가 목표하는 최대 사용자 수에 도달하기 위해 현재 성능을 파악하고, 개선하는 작업

### 테스트 종류

**성능(Performance) 테스트**

- 시스템의 요소가 특정 상황에서 어느 정도의 성능을 보이는지 측정
    - 기존 시스템에 대한 벤치마킹, 애플리케이션의 결함을 찾기 위함이 아니다.

**부하(Load) 테스트**

- 임계치의 한계에 도달할 때까지 시스템에 부하를 꾸준히 증가시키며 진행
    - 부하 상황에서의 시스템 동작을 모니터링 한다.
    - 발생시키는 부하는 실제 시스템에 적용될 예상 트래픽이어야 한다.
    - Web Server, Database, Infra 등 모든 요소의 한계를 찾아서 미래에 발생할 부하 대비하는 것이 목표
        - ex) 연말 정산, 수강 신청하는 인원 예상 수치

**스트레스(Stress) 테스트**

- 시스템이 과부하 상태에서 어떻게 동작하는지 모니터링
    - 시스템의 실패를 확인하고 모니터링하는 과정이 정상적으로 이루어지는지 테스트
    - 민감 정보 또는 보안상의 문제 노출 여부 테스트
    - 장애 조치와 복구 절차가 효과적이고 효율적인지 테스트

### 서비스 성능 지표

- Throughput
    - 시간당 처리량, TPS(Transaction Per Second), RPS(Request Per Second) 라고도 한다.
    - 1초에 처리하는 단위 작업의 수, 또는 1초에 처리하는 HTTP 요청의 수
- Latency
    - 서버가 클라이언트 요청을 응답하기 까지 걸리는 시간

### 성능 분석 예제 (전체서비스의 Throughput, Latency 분석)

|            | Web Server | Web Application Server | Database |
|------------|------------|------------------------|----------|
| Throughput | 500 TPS    | 2000 TPS               | 1000 TPS |
| Latency    | 200ms      | 50ms                   | 100ms    |

- 500 TPS, 350ms
- 성능에 대한 비유는 고속도로와 같다. Web Server 에서 정체(병목) 되어 성능은 결국 500 TPS
- WAS, Database 의 TPS 를 각각 1000 TPS 씩 개선하더라도 여전히 Web 서비스는 초당 500개의 트랜잭션만 통과할 수 있다.
- 서비스 전체의 성능을 높이기 위해서는 이러한 병목 구간을 찾고, 해당 병목 구간의 TPS 가 증가해야만 한다.

### 정리

- Throughput
    - 서비스의 하위 시스템들 중 가장 낮은 처리량
    - 병목 구간 해결
- Latency
    - 하드웨어 처리 성능, 애플리케이션 로직, 쿼리 인덱스 등 다양항 원인으로 작업의 Latency 발생 가능
    - Throughput 이 한계점에 도달하면 대기시간 또한 길어지므로 Latency 발생 가능
    - 하나의 하위 시스템 Latency 가 줄어들면 전체 Latency 도 줄어들게 되므로 병목 구간을 찾기보다 가장 Latency 가 큰 하위 시스템을 개선하는 것이 서비스의 Latency 를 대폭 줄일 수
      있는 방법이다.
    - 병목 지점과 관계없이 각 하위 시스템들의 Latency 개선이 전부 영향을 줄 수 있다.

### 개선 방법

- 전체 서비스의 성능을 개선하기 위해서는 하위 시스템의 병목 구간을 찾아 개선하여 Throughput 이 증가해야만 하고, 각 하위 시스템의 Latency 를 줄여서 전체 서비스의 Latency 를 줄여야만
  합니다.

## 성능 테스트 시나리오

- Contoller, Agent, Target 서버가 필요하고, 이는 각각 다른 서버로 구성되어 있어야 한다.

### 서버 구성

- WAS (Java, Spring) 2대
- Redis 1대
    - 캐싱 유무에 따른 TPS 확인
- MySql
- 웹서버 (Nginx ) 1대
    - 웹서버 유무, 로드밸런싱 유무에 따른 TPS 확인
    - gzip 설정 사용
        - Json 응답 압축

### Ngrinder

- 서버 성능 측정 (부하 테스트)
- 네이버 오픈 소스
- groovy script 기반으로 다양한 시나리오 작성 가능
- TPS(Througput), 평균 테스트 시간(Latency), CPU 등 체크

### Pinpoint

- Java 로 작성된 대규모 분산 시스템용 APM 도구
- 모니터링 툴, Transaction 추적 제공

### jstack

- pinpoint 로 애플리케이션 전반적인 상황 파악 가능
- pinpoint Trace 기능으로 모든 패키지와 클래스를 탐색하는 것은 과하다.
- Thread 간의 경합으로 발생되는 예기치 않은 현상들을 탐지하기는 어렵다.
- 이 때 Thread Dump 분석한다.

### 결론

- User 가 증가함에 따라 Throughput 이 한계에 도달하면 현 상태의 최대 처리량으로 추정 가능. (단위 테스트)
- JVM 튜닝, 슬로우 쿼리 분석 등 다양한 성능 개선 작업 가능

- 어느 정도의**부하**를 견딜 수 있는지 알고 있다.
- 한계치에서**병목**이 생기는 지점을 알고 있다.
- 자원을**효율적**으로 사용한다.
- **메모리 누수, 오류, 오버플로우**는 발생하지 않는다.
- **최악의 상황**에서 어떤 동작을 하는지 직접 확인하였다.
- **장애 조치와 복구**의 동작을 직접 확인하였다.

## Reference

- https://nesoy.github.io/articles/2018-08/Testing-Performance
- https://woowabros.github.io/experience/2018/05/08/billing-performance_test_experience.html
- https://www.softwaretestinghelp.com/what-is-performance-testing-load-testing-stress-testing/