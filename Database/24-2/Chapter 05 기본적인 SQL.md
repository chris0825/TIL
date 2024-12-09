목차
CREATE문
SELECT문
DELETE문
UPDATE문
WHERE문
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
# SELECT문

# WHERE문
## 문자열 비교
- LIKE
  - _: 자리수 지정
    > ex) '_a': aa, ba, ca와 같은 2자리 단어 중 a로 끝나는 단어
  - %: 포함여부
    > ex) '%a': 자리수 무관 a로 끝나는 단어
- =: 일치하는 단어
  > ex) 

# 제약조건
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
# UPDATE문

# DELETE문
: 릴레이션에서 투플을 제거하는 명령
