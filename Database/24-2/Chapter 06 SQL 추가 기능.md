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
```
_________________
| 주질의 (외부질의) |
________|-----------------
        | 중첩질의 (내부질의) |
        ------------------
```
> 일반적으로 데이터 양이 많을 때 조인보다 중첩질의 성능⬆️<br>
> ∵ 조인은 데이터를 모두 합친 후 연산하지만, 중첩질의는 필요한 데이터를 찾아 이를 조합

# 부속질의
## SELECT 부속질의: 스칼라 부속질의
> 결과 값이 단일 행, 단일 열인 스칼라값
## FROM 부속질의: 인라인 뷰
> 상관 부속질의 사용 X
## WHERE 부속질의: 중첩질의
### 상관된 질의
> 내부질의에서 외부질의의 FROM절의 테이블을 참조하는 경우
### 중첩질의 연산자
- 비교
  |기호|의미|
  |:-:|:-|
  |=|같다|
  |>|초과|
  |>=|이상|
  |<|미만|
  |<=|이하|
  |<>|같지않다|
- 집합
  |기호|의미|
  |:-:|:-|
  |IN|집합에 속해있다|
  |NOT IN|집합에 속해있지 않다|
- 한정
  |기호|의미|
  |:-:|:-|
  |ALL|모든 것이 조건에 만족한다|
  |ANY|어떤 것이 조건에 만족한다|
- 존재
  |기호|의미|
  |:-:|:-|
  |EXISTS|공집합이 아니다(최소 1개 이상의 투플이 존재)|
  |NOT EXISTS|투플이 없다|

# JOIN
## INNER JOIN (default)

## OUTER JOIN
### LEFT OUTER JOIN(⟕)
> 왼쪽 테이블을 기반으로 오른쪽 테이블을 매칭<br>
> 왼쪽 테이블 기준 오른쪽 테이블과 매칭되는 투플이 없으면 NULL처리
### RIGHT OUTER JOIN(⟖)
> 오른쪽 테이블을 기반으로 왼쪽 테이블을 매칭<br>
> 오른쪽 테이블 기준 왼쪽 테이블과 매칭되는 투플이 없으면 NULL처리
### FULL OUTER JOIN(⟗)
> 두 테이블을 모두 매칭, LEFT OUTER JOIN결과와 RIGHT OUTER JOIN값 합친것과 결과값이 동일<br>
> 두 테이블의 투플 중 매칭되지 않는 투플은 다른 테이블값을 NULL처리

ex)
![OUTER_JOIN](https://github.com/chris0825/TIL/blob/main/Database/resource/OuterJoin.png?raw=true)

## NATURAL JOIN(*)
> 조인조건을 명시하지 않음
```sql
# 관계대수 표현
A * B

# SQL 질의어
SELECT *
FROM A, B
WHERE A.a = B.a
```
## 다중 조인
> 3개 이상의 테이블을 조인
