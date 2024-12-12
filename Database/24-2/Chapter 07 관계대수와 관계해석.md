# 데이터 모델의 구성 요소
> 데이터베이스 구조와 제약 조건, 데이터를 다루기 위한 연산들의 집합
# 관계 대수
> 관계 모델의 기본 연산들의 집합<br>
> 검색 질의 기술에 사용
## 연산 종류
### 단항 관계 연산
- SELECT(σ)
- PROJECT(π)
- RENAME(ρ)
### 집합 연산
- UNION(∪)
- INTERSECTION(∩)
- DIFFERENCE(-)
- CARTESIAN PRODUCT(x)
### 이진 관계 연산
- JOIN(⋈)
- DIVISION(÷)
### 추가 관계 연산
- OUTER JOINS
- OUTER UNION
- AGGREGATE FUNCTIONS(SUM, COUNT etc...)

# SELECT: σ
## 관계 대수 표현
σ<sub>선택조건</sub>(R)
## SQL 표현
```sql
SELECT *
FROM R
WHERE 선택조건;
```
ex)
EMPLOYEE테이블에서 5번 부서이거나 5번 부서가 아니라면 나이가 18이상이면서 남자인 직원을 보이시오<br>
관계대수<br>
σ<sub>Dno=5 OR (Age≥18 AND Sex='M'</sub>(EMPLOYEE)
## 특징
1. 연산의 결과는 기본 테이블과 동일한 스키마를 갖는 테이블 생성
2. 결과 투플 수는 기본 테이블의 투플 수와 같거나 작음
3. 교환법칙, 결합법칙 성립
   > 교환법칙: σ<sub>A</sub>(σ<sub>B</sub>(R)) = σ<sub>B</sub>(σ<sub>A</sub>(R))<br>
   > 결합법칙: σ<sub>A</sub>(σ<sub>B</sub>(R)) = σ<sub>A AND B</sub>(R)

# PROJECT(π)
## 관계 대수 표현
π<sub>애트리뷰트집합</sub>(R)
## SQL 표현
```sql
SELECT 애트리뷰트집합
FROM R;
```
## 특징
1. 결과 투플 값 중복X
2. 결과에 키값 포함시 기본 테이블과 결과값이 같음(∵ 키는 중복X)
3. 교환 법칙X
4. A가 B의 부분집합인 경우 더 큰 집합 B만 표기 가능
   ex) π<sub>A</sub>(π<sub>B</sub>(R)) = π<sub>A</sub>(R)

# ←: 화살표
> R1 ← σ<sub>A</sub>(R)<br>
> R2 ← π<sub>B</sub>(R1)
## 기능
1. 연산의 순서 명확화
2. 결과 릴레이션의 이름 변경

# RENAME(ρ)
## 관계 대수 표현
ρ<sub>변경할이름</sub>(기존테이블)
> ex)<br>
> 1. 테이블 이름 변경<br>
> ρ<sub>R2</sub>(R)<br>
> 2. 애트리뷰트 이름 변경<br>
> ρ<sub>(a, b)</sub>(R)<br>
> 3. 테이블과 애트리뷰트 이름 변경<br>
> ρ<sub>R2(a, b)</sub>(R)

## SQL 표현
```sql
# 테이블 이름 변경
테이블명 AS 변경할이름;
테이블명 변경할이름;

# 애트리뷰트 이름 변경
애트리뷰트 AS 변경할이름;
애트리뷰트 변경할이름;

# 테이블, 애트리뷰트 이름 변경
테이블명 AS 변경할테이블명(변경할애트리뷰트명);
```

# 집합 연산
> 관행적으로 테이블의 애트리뷰트 이름은 좌측 테이블의 이름을 따른다
## 타입 호환성(합집합 호환성)
집합 연산을 하려는 두 테이블은
   1. 애트리뷰트수가 같아야 한다
   2. 대응되는 도메인(dom(A<sub>i</sub>) = dom(B<sub>i</sub>)<sub>(i=1, 2, ..., n)</sub>)이 같아야 한다
## 특징
1. 교환법칙과 결합법칙<br>
   ||합집합|교집합|차집합|
   |:-:|:-:|:-:|:-:|
   |교환법칙|O|O|X|
   |결합법칙|O|O|-|
2. 교집합 연산은 합집합과 차집합으로 표현이 가능
   > R ∩ S = ((R ∪ S) - (R - S)) - (S - R)
## 완전집합
> 모든 관계 대수식을 표현할 수 있는 최소한의 연산자 집합<br>
> '관계적으로 완전하다'라고 정의

# 카티션 곱(X): Cross product
## 관게 대수 표현
R X S (R과 S는 어떤 릴레이션)
## 결과 값
> R(A<sub>1</sub>, ..., A<sub>n</sub>, B<sub>1</sub>, B<sub>n</sub>) ← R(A<sub>1</sub>, ..., A<sub>n</sub>) X S(B<sub>1</sub>, B<sub>n</sub>)
- 애트리뷰트 수
  > = R의 애트리뷰트 수 X S의 애트리뷰트 수
- 투플 수
  > = R의 투플 수 X S의 투플 수

# JOIN
## (세타) 조인(⋈)
### 관계 대수 표현
R ⋈<sub>조인조건</sub> S
### 특징
- 각 조건의 형태 = A<sub>i</sub> θ B<sub>i</sub>
   > A<sub>i</sub>와 B<sub>i</sub>는 각 R과 S의 애트리뷰트이다.<br>
   > 대응되는 애트리뷰트는 서로 같은 도메인을 갖는다.<br>
   > θ는 비교연산자(=, <, ≤, >, ≥, ≠)를 의미한다.

### 동등 조인: EQUI JOIN
> 조인 조건의 비교 연사자로 '='를 사용하는 조인
R ⋈<sub>A=B</sub> S

### 자연 조인: NATURAL JOIN (*)
> 이름이 서로 같은 애트리뷰트를 별도로 명시하지 않고 알아서 조인<br>
> 애트리뷰트 이름이 다르다면 RENAME 과정을 통해 같게 만들어준 후 NATURAL JOIN 수행<br>
> ex)<br>
> R1 ← ρ<sub>(a, ..., n)</sub>(R)<br>
> RN ← R1 * S<br>
> 또는<br>
> RN ← R * ρ<sub>(a, ..., n)</sub>(S)

## 셀프 조인: SELF JOIN
> 하나의 같은 테이블을 조인<br>
> ex)<br>
> R1 ← π<sub>(a, b, c)</sub>(R)<br>
> S ← R ⋈<sub>A=a</sub> R1

## 외부 조인
> 자연조인, 동등조인과 달리<br>
> 1. 결과값의 중복을 허용
> 2. 관계된 투플이 없어도 조인이 가능
### 종류
- LEFT OUTER JOIN(⟕)
  > 자연조인 결과 + 왼쪽 테이블의 투플 중 매칭되지 않은 값은 NULL로 채움
- RIGHT OUTER JOIN(⟖)
  > 자연조인 + 오른쪽 테이블의 투플 중 매칭되지 않은 값은 NULL로 채움
- FULL OUTER JOIN(⟗)
  > 자연조인 + 두 테이블의 투플 중 매칭되지 않은 값은 NULL로 채움
### OUTER UNION
> 타입 호환성이 없는 두 테이블의 합집합<br>
> R(x, y) OUTER UNION S(x, z) -> T(x, y, z)<br>
> : 결과에 서로 호환되는 애트리뷰트는 한번만 나타내고 그렇지 않은 애트리뷰트는 모두 포함

# 선택률과 조인선택률
- 선택률
  > = 결과 투플의 수 / 전체 가능한 투플의 수
- 조인선택률
  > = 조인 결과로 선택된 투플의 수 / (R의 투플 수 X S의 투플 수)
  
# 카디션 곱과 조인 연산
> R ⋈<sub>조인조건</sub> S = σ<sub>선택조건</sub>(R X S)

# 디비전 연산(÷): DIVISION
## 관계 대수 표현
R ÷ S (R과 S는 릴레이션)
## 디비전 연산의 다른 표현
T = R ÷ S<br>
T<sub>1</sub> = π<sub>B</sub>(R)<br>
T<sub>2</sub> = π<sub>B</sub>((S X T<sub>1</sub>) - R)<br>
T = T<sub>1</sub> - T<sub>2</sub>

# 집계 함수
> 표준 관계대수로 표현이 불가
## 종류
- SUM
- AVERAGE
- MAXIMUM
- MINIMUM
- COUNT
## 표현
<sub>그룹애트리뷰트(선택)</sub>F<sub>집계함수및애트리뷰트</sub>(R)<br>
ex)<br>
EMPLOYEE테이블에서 부서 번호별 사원의 수와 평균 월급을 구하시오.<br>
<sub>DNO</sub>F<sub>COUNT SSN, AVERAGE SALARY</sub>(R)<EMPLOYEE><br>

# 순환적 폐포
> 동일한 테이블의 투플간 연산을 의미
> 순환 레벨의 수를 알지 못해 관계 연산으로 표현이 불가


# 관계 해석
> '무엇을' 검색할 것인가를 기술하는 선언적 표기법을 사용하는 비절차적 질의어
# 관계적 완전성
> 관계 질의어가 관계 대수(관계 해석)로 표현이 가능한 경우
## 관계 대수와 관계 해석
|관계대수|관계해석|
|:-:|:-:|
|절차적|비절차적|
|연산을 순차적으로 작성|선언적 해석식으로 명시|

➡️ 관계 대수와 관계 해석의 표현력은 동등
## 관계 해석 질의
### 형식
{ 변수 | 테이블(변수) and 조건식 }<br>
ex)<br>
급여가 5,000이 넘는 사원의 이름을 조회하시오<br>
{ x.name | EMPLOYEE(x) and x.salary>5000 }
### SQL 질의
```sql
SELECT x.name
FROM EMPLOYEE AS x
WHERE x.salary>5000;
```
### 특징
- 관계해석식은 원자들로만 구성됨
- 각 원자는 True, False로만 계산됨

# 존재 정량자와 전체 정량자
- 존재 정량자(∃)
  > (∃ 투플변수)(식): 하나 이상의 투플이 식의 결과가 참이면 True
- 전체 정량자(∀)
  > (∀ 투플변수)(식): 모든 투플이 식의 결과가 참이면 True, 하나라도 참이 아니라면 False

# 안전식 (↔️ 불안전식)
> 유한개의 투플을 결과로 생성하는 식(불안전식은 결과 투플이 무한개)<br>
> ex) {t | not (R)}: R을 제외한 모든 투플 ▶️ 결과값 무한대 = 불안전식)

# 도메인 관계 해석
> 투플변수 대신 도메인 변수를 사용하는 관계 해석<br>
> 투플 관계 해석(=투플 중심), 도메인 관계 해석(=애트리뷰트 중심)<br>
> 조건에 참여하는 애트리뷰트는 존재 정량자에 속박됨<br>
> ex)<br>
> {q, s, v | (∃z)(∃l)(∃m)EMPLOYEE(qrstuvwxyz) AND DEPARTMENT(lmno) AND l='Research' AND z=m}
