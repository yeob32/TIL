# Java Warm Up

> 1. 서버 사양이 낮아서 war 파일에 담긴 static resource 를 서비스 하기 어려운 경우
> 2. 성능 극대화를 위해 웹서버에서 static resource 를 바라볼 수 있도록 WAR 압축을 플어주고 싶을 경우

```
-- War 또는 Jar 압축 해제

$ mkdir $SOURCE
$ cp demo-springboot-0.0.1-SNAPSHOT.war $SOURCE
$ cd $SOURCE
$ jar xf demo-springboot-0.0.1-SNAPSHOT.war
```

### War

```
nohup /usr/bin/java $JAVA_OPTS -Dspring.profiles.active="$PROFILENAME" -classpath "$CLASS_PATH" org.springframework.boot.loader.WarLauncher < /dev/null > $WORKDIR/app.log 2>&1
```

### Jar

```
nohup /usr/bin/java $JAVA_OPTS -Dspring.profiles.active="$PROFILENAME" -classpath "$CLASS_PATH" org.springframework.boot.loader.JarLauncher < /dev/null > $WORKDIR/app.log 2>&1
```

### 자바 운영 관련

### 참고

* [https://www.holaxprogramming.com/2017/10/09/java-jvm-performance/](https://www.holaxprogramming.com/2017/10/09/java-jvm-performance/)

## SLF4J 충돌 시

```
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/Users/sykim/.gradle/caches/modules-2/files-2.1/org.slf4j/slf4j-simple/1.7.30/e606eac955f55ecf1d8edcccba04eb8ac98088dd/slf4j-simple-1.7.30.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/Users/sykim/.gradle/caches/modules-2/files-2.1/ch.qos.logback/logback-classic/1.2.3/7c4f3c474fb2c041d8028740440937705ebb473a/logback-classic-1.2.3.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [org.slf4j.impl.SimpleLoggerFactory]
```

```
# SLF4J 충돌 의존 찾아서 제외 시켜주면 됨
implementation ('it.ozimov:embedded-redis:0.7.3') {
    exclude group: "org.slf4j", module: 'slf4j-simple'
}
```

### 테스트 작성 중 에러 발생

```
FAILURE: Build failed with an exception.
* What went wrong:
Execution failed for task ':demo-initialize:test'.
> No tests found for given includes: [com.example.initialize.ConfigurationTest.test](filter.includeTestsMatching)
* Try:
```

### 해결 build.gradle

> gradle, JUnit5 사용 시

```
test { 
        useJUnitPlatform()
    }
```

## Refactoring

- if 문이 많으면 클래스가 두 가지 이상의 책임을 담당하고 있다는 신호 -> 가독성 하락 및 단위테스트 만들기 어려움
    - 추상화 필요한 시점이 아닌지 고민 필요
- null 을 리턴하는 로직이 많아질수록 테스트가 어려워짐
    - null object 패턴 또는 Optional 사용 고려
        - null object 패턴
            - 우리는 함수가 실패한 경우에도 항상 유효한 객체를 반환한다는 것을 보장
            - 실패를 나타내는 객체들은 `아무일도` 하지 않는다.

### Java features

- https://www.techgeeknext.com/java/java17-features
- shadowJar

### session-clustering

- 세션 관리 서버가 따로 있다는 가정
    - 세션 서버 먹통이 되면?
- redis
    - sentinel 구성하여 감시
- hazelcast
    - was 간 동일한 데이터 유지

### @EqualsAndHashCode

```
warning: Generating equals/hashCode implementation but without a call to superclass, 
even though this class does not extend java.lang.Object. 
If this is intentional, add '@EqualsAndHashCode(callSuper=false)' to your type.
```

### 해결

- @EqualsAndHashCode(callSuper = true) , default => false
    - 객체 동일 비교 시 부모 클래스 필드 값들도 동일한지 체크한다.
