# Lombok TS

### @EqualsAndHashCode
```
warning: Generating equals/hashCode implementation but without a call to superclass, 
even though this class does not extend java.lang.Object. 
If this is intentional, add '@EqualsAndHashCode(callSuper=false)' to your type.
```
### 해결
- @EqualsAndHashCode(callSuper = true) , default => false
  - 객체 동일 비교 시 부모 클래스 필드 값들도 동일한지 체크한다.
