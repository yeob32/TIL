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

## 참고
* https://m.blog.naver.com/PostView.nhn?blogId=nayasis&logNo=220765123227
