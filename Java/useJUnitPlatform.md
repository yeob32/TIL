

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
