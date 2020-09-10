# 이슈 모음

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