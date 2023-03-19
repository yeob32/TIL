# Java Version

### Java Version 변경 - Mac
```
$ java -version

java version "17.0.6" 2023-01-17 LTS
Java(TM) SE Runtime Environment (build 17.0.6+9-LTS-190)
Java HotSpot(TM) 64-Bit Server VM (build 17.0.6+9-LTS-190, mixed mode, sharing)

$ /usr/libexec/java_home -V

Matching Java Virtual Machines (4):
    17.0.6 (x86_64) "Oracle Corporation" - "Java SE 17.0.6" /Library/Java/JavaVirtualMachines/jdk-17.jdk/Contents/Home
    15.0.1 (x86_64) "Oracle Corporation" - "OpenJDK 15.0.1" /Users/sykim/Library/Java/JavaVirtualMachines/openjdk-15.0.1/Contents/Home
    1.8.291.10 (x86_64) "Oracle Corporation" - "Java" /Library/Internet Plug-Ins/JavaAppletPlugin.plugin/Contents/Home
    1.8.0_291 (x86_64) "Oracle Corporation" - "Java SE 8" /Library/Java/JavaVirtualMachines/jdk1.8.0_291.jdk/Contents/Home
/Library/Java/JavaVirtualMachines/jdk-17.jdk/Contents/Home

$ export JAVA_HOME=$(/usr/libexec/java_home -v 15)
$ source ~/.zshrc
$ java -version

openjdk version "15.0.1" 2020-10-20
OpenJDK Runtime Environment (build 15.0.1+9-18)
OpenJDK 64-Bit Server VM (build 15.0.1+9-18, mixed mode, sharing)
```
