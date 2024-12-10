목차
CREATE문
SELECT절
DELETE문
UPDATE문
WHERE절
데이터타입

# CREATE문
- DDL: 데이터 정의를 위한 기본적인 SQL명령
- 스키마, 테이블, 타입, 도메인, 뷰 주장, 트랙 정의
## CREATE TABLE
- 새로운 릴레이션을 생성하는데 사용
- 릴레이셔의 이름, 애트리뷰트 이름, 값 집합, NOT NULL 제약조건, 키, 엔티티 무결성, 참조 무결성 제약조건 명시
- 선택적 스키마 지정이 가능

| | CREATE TABLE | CREATE VIEW |
|:-:|:-:|:-:|
| 테이블 생성 | 기본(물리적) | 논리적(가상) |

# 데이터 타입
## 기본 데이터 타입
### 숫자
- 정수
  - INTEGER
  - INT
  - SMALLINT
- 실수(부동소수점)
  - FLOAT
  - REAL
  - DOUBLE PRECISION
### 문자열
- 고정길이
  - CHAR(n)
  - CHARACTER(n)
- 가변길이
  - VARCHAR(n)
  - CHAR VARYING(n)
  - CHARACTER VARYING(n)
### 비트열
- 고정길이
  - BIT(n)
- 가변길이
  - BIT VARYING(n)
### 불리언
- True
- False
- Unknown
### 날짜와 시간
- 날짜(10자리 포멧): YYYY-MM-DD
- 시간(8자 포멧): HH:MM:SS

## 추가 데이터 타입
### 타임스탬프
> DATE + TIME + 소숫점 6자리 <br> ➡️ YYYY-MM-DD HH:MM:SS.XXXXXX
### INTERVAL 데이터 타입

## CREATE DOMAIN
> 새 도메인 설정시 사용하는 구문
```sql
CREATE DOMAIN 도메인명 AS 데이터타입;
```
### 애트리뷰트 DEFAULT
- NULL 허용(허용하지 않으려면 NOT NULL명시)
- 값 지정
  ```sql
  애트리뷰트명 데이터타입 DEFAULT 디폴트값
  ```
# SELECT절
## DISTINCT
> 중복 값 제거

## 연산자 사용
- +, -, *, / 연산자의 사용이 가능함

# WHERE절
## 문자열 비교
- LIKE
  - _: 자리수 지정
    > ex) '_a': aa, ba, ca와 같은 2자리 단어 중 a로 끝나는 단어
  - %: 포함여부
    > ex) '%a': 자리수 무관 a로 끝나는 단어
- =
  > 일치하는 단어를 찾을때는 = 연산자 사용
## 숫자 범위 BETWEEN
```sql
BETWEEN 시작(이상) AND 끝(이하)
```
## *
> ALL의 의미<br>
> 모든 애트뷰트가 질의 결과로 출력됨

# 제약조건
## 참조 무결성 제약 조건
- 조건 위반 가능성이 있는 질의어
  - ON DELETE
  - ON UPDATE
- 위반시 조치
  - ON DELETE CASCADE
    > 삭제할 투플과 연관된 투플 모두 삭제
  - ON UPDATE CASCADE
    > 수정할 투플과 연관된 투플 모두 수정
## 키 지정 키워드
- PRIMARY KEY
  > 기본키
- UNIQUE
  > 대체키
- FOREIGN KEY
  > 외래키

## CONSTRAINT
> 제약조건을 명확하게 식별하고 관리를 용이하게 함
```sql
CONSTRAINT 제약조건이름 제약조건유형
```
## CHECK
- 투플 기반 제약조건 명시(2개 이상 애트리뷰트에 대한 제약 조건)
  > ex) 학생(학번, 입학년도, 졸업년도)라는 테이블이 존재할 때 졸업년도는 입학년도보다 이전일 수 없다는 조건
  ```sql
  CHECK(입학년도 < 졸업년도)
  ```
- 도메인값 제약조건 명시
  > 테이블 생성시 
  ```sql
  애트리뷰트명 데이터타입 CHECK(제약조건)
  ```

# INSERT문
> 삽입하는 투플 값은 지정한 애트리뷰트 순서와 동일해야 함(지정한 순서와 다르게 지정하려면 삽입하려는 순서에 따른 애트리뷰트를 지정해주어야함)<br>
> 특정 애트리뷰트 값만 삽입하려면 삽입하려는 값의 애트리뷰트를 명시해주어야 함(명시하지 않은 애트리뷰트는 Default값이 지정되어있으면 default값, 그렇지 않으면 NULL값이 채워짐)
## SELECT절과 결합
> 질의의 결과로 생성된 다중 투플을 또 다른 릴레이션에 삽입하는 경우
```sql
INSERT INTO 삽입할테이블(애트리뷰트A, ..., N)
SELECT a, ..., n
FROM 조회할테이블
WHERE 조회조건
```

# UPDATE문
> 투플의 애트리뷰트 값을 수정하기 위해 사용
```sql
UPDATE 테이블
SET 새로설정할값
WHERE 수정할투플조건
```

# DELETE문
> 릴레이션에서 투플을 제거하는 명령
```sql
DELETE FROM 테이블
WHERE 삭제할투플조건

# WHERE절 생략가능 -> 테이블 내 모든 투플삭제(빈 테이블만 남음)
```

# ORDER BY절
- 오름차순(ASC)
  > default는 ASC오름차순 정렬
  ```sql
  # DEFAULT ASC
  ORDER BY 정렬기준애트리뷰트
  
  # ASC 명시
  ORDER BY 정렬기준애트리뷰트 ASC
  ```
- 내림차순(DESC)
  ```sql
  # DESC
  ORDER BY 정렬기준애트리뷰트 DESC
  ```
- 다중정렬
  > 왼쪽에서부터 정렬 우선권
  ```sql
  ORDER BY 우선순위1 DESC, 우선순위2 ASC
  ```
# GROUP BY절
> 특정 애트리뷰트의 값이 같은 투플을 모아 그룹화<br>
> 집계 함수를 적용하기 용이

# HAVING절
> GROUP BY에서 묶인 집합에 대한 조건문을 정의

# CASE문
> 투플의 검색(R), 삽입(C), 수정(U)시 조건에 따라 다른 질의가 가능
```sql
UPDATE 테이블
SET 애트리뷰트 = 
    CASE WHEN 조건 THEN 실행문
                  ELSE 실행문
    END;
```

# 질의 평가 순서
1. FROM
2. WHERE
3. GROUP BY
4. HAVING
5. SELECT
6. ORDER BY

# AS: 별명
> 다른 테이블에 동일한 애트리뷰트 이름이 있을 수 있어 모호함을 방지하고자 사용(중첩질의)<br>
> 동일 테이블을 참조하는 경우에도 사용
- 애트리뷰트 또는 테이블 별명
  ```sql
  애트리뷰트명 AS 별명
  # 또는 (AS 키워드 생략 가능)
  애트리뷰트명 별명
  ```
- 테이블과 애트리뷰트 동시에 별명짓기
  ```sql
  테이블 AS 테이블별명(애트리뷰트별명)
  ```

# VIEW
> 실제 물리적으로 저장되지 않는 유도된 가상 테이블<br>
> 항상 최신의 정보를 유지함(DBMS가 자동으로 최신화)
- 명령어
  - 뷰 생성
    ```sql
    CREATE VIEW 뷰이름
    ```
  - 뷰 삭제
    ```sql
    DROP VIEW 뷰이름
    ```
