# MySQL Trigger

## Trigger ?
- 특정 조건이 만족하면 자동으로 실행되는 일종의 장치
- 설정 -> 동작 감시 -> 조건 만족 -> 실행

## 트리거 구조
```
DELIMITER $$
    CREATE TRIGGER trigger_name
    {BEFORE | AFTER} {INSERT | UPDATE | DELETE}
    ON table_name FOR EACH ROW
    BEGIN
        -- process
    END
DELIMITER;
```

## 트리거 종류
- 행 트리거 : 테이블 행 각각 실행
- 문장 트리거 : insert, update, delete 문 이벤트 발생 시 실행

## 트리거 이벤트 
- 트리거 동작 시점
    - Before : 이벤트 발생 이전 트리거 실행
    - After : 이벤트 발생 이후 트리거 실행
- 이벤트
    - INSERT : 삽입 시 트리거 실행
    - UPDATE : 수정 시 트리거 실행
    - DELETE : 삭제 시 트리거 실행
    
## 트리거 키워드
- old : 이벤트 발생 기준 이전 데이터
- new : 이벤트 발생 기준 이후 데이터

| 이벤트 | old | new |
|:---:|:---:|:---:|
| `INSERT` | X | O |
| `UPDATE` | O | O |
| `DELETE` | O | X |

    
### 사용 예시
```
-- 삽입 전 
BEFORE INSERT ON PRODUCT
-- 수정 후
AFTER UPDATE ON USER
-- 삭제 전
BEFORE DELETE ON COUPON

-- 실제 사용 예시
DELIMITER $$
	CREATE TRIGGER autoBackup
	BEFORE DELETE ON chat
	FOR EACH ROW
	BEGIN
		DECLARE idTemp VARCHAR(32);
		DECLARE answerTemp VARCHAR(32);

		SET idTemp = OLD.id;
		SET answerTemp = OLD.answer;

		INSERt INTO chatBackup VALUE (idTemp, answerTemp);

	END $$
DELIMITER;

-- chat 테이블 삭제 시 트리거 발생
DELETE FROM chat WHERE id = 'some';
```

# Reference
- https://blog.naver.com/PostView.nhn?blogId=alcmskfl17&logNo=221859839012