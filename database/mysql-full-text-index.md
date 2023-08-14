# MySQL Full-Text Index

## 풀텍스트 인덱스

- 긴 문자의 텍스트 데이터를 빠르게 검색하기 위한 MySQL 기능
- 긴 문장 전체를 대상으로 인덱싱하고, InnoDB 와 MyISAM 테이블만 지원
- char,varchar,text 타입 문자만 인덱싱 가능
- 여러개의 열에 풀텍스트 인덱스 지정 가능

## 풀텍스트 인덱스 사용법

```
CREATE TABLE table_name(
    열이름 데이터형식,
    FULLTEXT 인덱스이름 (열이름)
);

CREATE FULLTEXT INDEX 인덱스이름 ON 테이블이름 (열이름);
```

## 데이터 인덱싱 기법

#### Stop-word parser

- 공백이나 Tab, 문장 기호, 또는 사용자가 정의한 문자열을 기준으로 토큰을 나누는 기법
    - ex) 아빠가 방에 들어갔다. → 아빠가 / 방에 / 들어갔다.
- 공백을 구분자로 단어 단위로 저장하기 때문에 검색하는 단어가 정확히 일치해야지만 결과를 받을 수 있음

#### N-gram parser

- n-gram 기법을 사용하여 할당한 토큰의 크기 n만큼씩 데이터를 인덱스로 파싱해두었다가 사용하는 기법
    - ex) 아빠가 방에 들어갔다. → 아빠 / 빠가 / 방에 / 들어 / 어갔 / 갔다.

## 텍스트 검색

- 자연어 검색(natural search)
    - 특별히 옵션을 지정하지 않거나 뒤에 in natural language mode를 붙이면 자연어 검색을 한다.
  ```
  SELECT * FROM newspaper WHERE MATCH(article) AGAINST('영화');
  SELECT * FROM newspaper WHERE MATCH(article) AGAINST('영화' in natural language mode);
  ```
- 불린 모드 검색(boolean mode search)
    - 검색 문자열을 단어 단위로 분리한 후, 해당 단어가 포함되는 행을 찾는 규칙을 추가적으로 적용하여 해당 규칙에 매칭되는 행을 검색한다.
  ```
  SELECT * FROM FulltextTbl
    WHERE MATCH(description) AGAINST('+남자* 여자*' IN BOOLEAN MODE);
  ```
- 쿼리 확장 검색(query extension search)
    - 2단계에 걸쳐서 검색을 수행한다. 첫 단계에서는 자연어 검색을 수행한 후, 첫 번째 검색의 결과에 매칭된 행을 기반으로 검색 문자열을 재구성하여 두 번째 검색을 수행한다. 이는 1단계 검색에서 사용한
      단어와 연관성이 있는 단어가 1단계 검색에 매칭된 결과에 나타난다는 가정을 전제로 한다.

### 자연어 검색 vs 불린 모드 검색 비교

|    | 자연어 검색                          | 	불린 모드 검색                       |
|----|---------------------------------|---------------------------------|
| 장점 | 검색속도가 빠르다. <br>정확도 순에 따라 결과가 정렬 | 구문 검색이 가능하다. <br>검색의 정확도가 더 높다. |
| 단점 | 관련이 없는 데이터도 리턴                  | 시간이 너무 오래 걸린다.                  |

### Reference
- https://scarelt.tistory.com/10