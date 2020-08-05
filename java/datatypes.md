# Data Types


## Primitive Data Types
### Default Values
| Data Type | Bits | Scope | Default Value ( for fields ) |
| `byte` | 8bits | -2^7 ~ 2^7-1 (-128 ~ 127) | 0 |
| `short` | 16bits | -2^15 ~ 2^15-1 (-32,768 ~ 32,767) | 0 |
| `int` | 32bits | -2^31 ~ 2^31-1 (-2,147,483,648 ~ 2,147,483,647) | 0 |
| `long` | 64bits | -2^63 ~ 2^63-1 (-9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807) | 0L |
| `float` | 32bits | 0x0.000002P-126f ~ 0x1.fffffeP+127f | 0.0f |
| `double` | 64bits | 0x0.0000000000001P-1022 ~ 0x1.fffffffffffffP+1023 | 0.0d |
| `char` | 16bits | '\u0000' (0) ~ '\uffff' (65,535) | '\u0000' |
| `String` (or any object) |  |  | null |
| `boolean` | 1bits | true and false | false |

## 참고
* https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html
