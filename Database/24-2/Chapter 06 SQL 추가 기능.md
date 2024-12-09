# NULL
- 정의
  1. 알려지지 않은 값
  2. 이용할 수 없거나 보류해둔 값
  3. 적용할 수 없는 애트리뷰트
     
  **➡️ 각 NULL값은 서로 다른 값으로 간주됨**
  ```
  NULL = NULL    # FALSE
  NULL <> NULL   # FALSE
  ```
 - 연산
```sql
애트리뷰트 IS NULL     # NULL값을 찾는 조건
애트리뷰트 IS NOT NULL # NULL이 아닌 값을 찾는 조건
```

# BOOLEAN
|1|논리연산자|2|결과|
|:-:|:-:|:-:|:-:|
|TRUE|AND|TRUE|TRUE|
|||FALSE|FALSE|
|||UNKNOWN|UNKNOWN|
||OR|TRUE|TRUE|
|||FALSE|TRUE|
|||UNKNOWN|TRUE|
||NOT|-|FALSE|
|FALSE|AND|TRUE|FALSE|
|||FALSE|FALSE|
|||UNKNOWN|FALSE|
||OR|TRUE|TRUE|
|||FALSE|FALSE|
|||UNKNOWN|UNKNOWN|
||NOT|-|TRUE|
|UNKNOWN|AND|TRUE|UNKNOWN|
|||FALSE|FALSE|
|||UNKNOWN|UNKNOWN|
||OR|TRUE|UNKNOWN|
|||FALSE|FALSE|
|||UNKNOWN|UNKNOWN|
||NOT|-|UNKNOWN|

# 중첩질의

