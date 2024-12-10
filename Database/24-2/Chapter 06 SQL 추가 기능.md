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

# 집단함수 (Aggregate Functions)
## 사용 위치
- SELECT절, HAVING절
## 종류
- 내장 집단 함수
  - COUNT()
    > 투플의 갯수를 반환<br>
    > 서로 다른 값만 카운트 하려면 COUNT(DISTINCT 애트리뷰트) 하면 됨
  - SUM()
    > 결과 값의 애트리뷰트 값의 합을 반환
  - MAX()
    > 결과 값 중에서 최대 값을 반환
  - MIN()
    > 결과 값 중에서 최소 값을 반환
  - AVG()
    > 결과 값의 애트리뷰트 평균 값을 반환
## 특징
- COUNT(*)
  > 투플 개수를 카운트 하므로 NULL값도 카운트<br>
  > 공집합의 경우는 카운트 하지 않음(0 반환)

# ASSERT: 주장으로 제약 조건 명시
> 테이블 생성시 해당되지 않는 각종 제약 및 무결성 조건 외의 제약 조건 설정
```sql
# 해당 테이블에 투플이 존재하면 안된다는 주장(제약 조건)

CREATE ASSERTION 주장이름
CHECK( NOT EXISTS( SELECT *
                   FROM 테이블
                   WHERE 조건 ));
```

# TRIGGER
> 조건이 발생할 때 데이터베이스를 모니터하기 위해 행동의 유형을 명시
- ECA
  - 사건(Event): 어떤 사건이 발생하면 검사를 시작
  - 조건(Condition): 동작을 수행할 조건
  - 동작(Action): 조건이 만족되면 수행

ex)
```sql
CREATE TRIGGER 트리거이름
# EVENT (BEFORE/AFTER) -----
BEFORE INSERT OR UPDATE OF
FOR EACH ROW
# CONDITION: 생략 시 EVENT 발생마다
  WHEN 조건문
# ACTION: 실행할 SQL, 트랜잭션, 외부프로그램
  수행문;
```

# 뷰의 구현
## 질의 수정 방식
- 뷰에 대한 질의를 기본 테이블들에 대한 질의로 변환하여 처리
- 단점: 실행 시간이 많이 걸리는 복잡한 질의로 정의된 뷰에서 비효율적
## 뷰의 실체화
- 뷰를 생성하거나 처음 질의할 때 뷰 테이블을 물리적으로 생성 및 유지
- 문제: 기본 테이블 갱신시 뷰 테이블에 연동 X -> 점진적 갱신 전략으로 해결
## 실체 뷰의 갱신
- 즉시 갱신: 기본 테이블 갱신 즉시 뷰 수정
- 지연 갱신: 뷰 질의가 필요할 때 갱신
- 주기적 갱신: 일정 주기 갱신(뷰 질의가 항상 최신이 아닐 가능성 존재)
## 뷰의 종류별 갱신
- 집계 연산X, 단일 테이블 정의 뷰
