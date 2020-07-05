# String 

* Java에서 문자열은 String Pool로 관리. 
* "a" 라는 두 개의 문자열 변수를 지정했지만 JVM Heap 메모리의 String Pool에는 "a" 라는 문자열 하나만 존재. 
* 두 변수(a, b)는 reference로 가르키게 된다.

String a = "a"; // 이렇게 선언 시 Heap Area의 Permanent area에 String Pool로 등록. (intern() 메소드 자동 호출되면서 등록)
String Pool에 등록되면 프로세스가 종료될때까지 계속 유지.
String은 사용 될 때 먼저 String Pool에 등록되있는지 체크하고 처음 등록된 것을 사용.

**new String**
String a = new String("a"); // 다른 객체 생성과 마찬가지 만들때마다 새로운 메모리에 올라가게 됨.

```
String a = "a"; // a.hashCode() -> 97
String b = "a"; // b.hashCode() -> 97, System.identityHashCode(b) -> 587820154
assertEquals(a, b);
assertSame(a, b);

String c = new String("a"); // c.hashCode() -> 97, System.identityHashCode(c) -> 1437196911
assertEquals(c, b);
assertEquals(c.intern(), b); // String pool 에 등록
assertNotSame(c, b);
assertEquals(b.hashCode(), c.hashCode());
assertNotSame(System.identityHashCode(b), System.identityHashCode(c));
```

**String hashCode**
```
public static int hashCode(byte[] value) {
        int h = 0;
        int length = value.length >> 1;
        for (int i = 0; i < length; i++) {
            h = 31 * h + getChar(value, i);
        }
        return h;
    }
```

**System.identityHashCode()**
System 클래스의 identityHashCode()메서드로 객체가 메모리에서 가진 해쉬 주소값을 출력한다. 특별한 설정을 더하지 않았을 경우 .hashCode()와 동일한 값을 나타낸다.
즉 이게 OS(System)에서 가지는 해쉬값이다.

**.hashCode()**
Object에 있는 .hashCode()메서드로 객체가 메모리에서 가진 해쉬 주소값을 출력한다. 특별한 설정을 더하지 않았을 경우 System.identityHashCode()와 동일한 값을 나타낸다.
즉, 이게 Java(Application)에서 가지는 해쉬값이다.

### 참고
* https://tomining.tistory.com/195
* https://datamod.tistory.com/57
* https://codingdog.tistory.com/entry/java-hashCode-vs-identityHashcode-%EC%9D%B4-%EB%91%98%EC%9D%80-%EB%AC%B4%EC%97%87%EC%9D%B4-%EB%8B%A4%EB%A5%BC%EA%B9%8C%EC%9A%94
* https://hoit89.tistory.com/entry/String-Stringintern-String-poolequals
