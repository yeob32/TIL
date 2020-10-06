# Sonarqube

## Install
```
// SonarQube Docker 이미지 다운로드
$ docker pull sonarqube
// SonarQube 서버 시작
$ docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube
```

## Configuration

### 초기 계정
- admin / admin

### Gradle
- gradle/wrapper/gradle-wrapper.properties
```
systemProp.sonar.host.url=http://localhost:9000
systemProp.sonar.login=<token>
```

```
id 'org.sonarqube' version '3.0'
```

```
sonarqube {
    properties {
        property 'sonar', 'http://localhost:9000'
        property 'sonar.projectName', 'sonarqube_sample'
    }
}
```

```
$ ./gradlew sonarqube -Dsonar.host.url=http://localhost:9000 -Dsonar.verbose=true
```

## Intellij & SonarQube 연동
- 인텔리J 플러그인
	- sonarLint 
- SonarLint를 사용하면 IDE에서 정적 분석을 실행할 수 있고 코드 편집창에서 정적 분석 결과 확인할 수 있어 편하다.

### 설치
- plugin 설치 후 view > tool Windows -> sonarlint

### 설정
- sonarlint configure > Bind project to SonarQube / SonarCloud > configure the connection
- project > search in list
