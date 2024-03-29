![KakaoTalk_20231031_060722951](https://github.com/chris0825/TIL/assets/62418972/c218075c-ec3b-4337-81c3-2a4517a6721f)
![KakaoTalk_20231031_061506017](https://github.com/chris0825/TIL/assets/62418972/b457d385-76a8-4323-8303-718c28674d03)
# 관계 모델
### 관계 모델의 구성
- 관계 모델에서 데이터베이스는 릴레이션들의 모임(Collection)으로 표현
- 릴레이션과 투플
|릴레이션|투플|
|:-:|:-:|
|투플들의 집합으로 표현|애트리뷰트들로 구성|

# 릴레이션의 특성
### 릴레이션에서 투플의 순서
- 의미X (집합도 순서 무의미하잖아)
### 튜풀 내에서 값들의 순서와 릴레이션의 또 다른 정의
- n-투플은 n개 값의 순서 리스트이며, 한 투플 내에서 값들의 순서는 중요함
- 반면에, 각 애트리뷰트와 값이 서로 대응될 수 있다면 순서 중요하지 않을 수 있음
### 투플 내에서의 값들과 널
- 투플 내의 각 값은 더이상 나눌 수 없는 원자값들
- ER 모델에서의 다치 애트리뷰트나 복합 애트리뷰트는 관계 모델에서는 허용X -> 별도 릴레이션으로 표현
- 값을 알 수 없거나 해당되는 값이 없을 때 null이라는 특수 값 사용
### 스키마와 릴레이션의 해석(의미)
- 릴레이션 스키마는 일종의 선언 또는 주장으로 해석
- 릴레이션 내 각 투플은 선언/주장에 대한 사실 또는 인스턴스로 해석

# 관계 모델 제약 조건(Constraint)
### 제약 조건은 모든 릴레이션 인스턴스들이 만족해야 하는 조건
### 스키마 기반 제약 조건
- 데이터 모델 스키마에서 DDL을 통해 직접 표현이 가능한 조건
1. 도메인 제약 조건(Domain constraints)
  2. 속성 값은 도메인에 속해야 함
3. 키 제약 조건(Key constraints)
  4. 모든 투플은 유일해야 함(키의 성질)
5. 널에 대한 제약조건(Constraints on nulls)
  6. 널이 허용되지 않는 경우 널이면 안됨
7. 엔티티 무결성 제약조건(Entity integrity constraints)
  8. 기본키 != NULL
9. 참조 무결성 제약조건(Referential integrity constraints)
  10. 두 릴레이션 간 기본키-외래키 참조 관계

# 관계 데이터베이스와 스키마
### 관계 데이터베이스 스키마 = SIC: Schema Integrity Constraint
### 데이터 정의어(DDL)
- 관계 스키마를 정의하기 위한 언어

# 관계 모델의 갱신 연산
### 삽입 연산
- 제약 조건
  1. 도메인 제약 조건: 삽입되는 투플에서 애트리뷰트 값이 도메인에 없는 경우
  2. 키 제약 조건: 삽입되는 투플에서 기본키 값이 다른 투플에 존재하는 경우
  3. 엔티티 제약 조건: 삽입되는 투플에서 기본키의 값이 널인 경우
  4. 참조 무결성 제약 조건: 삽입되는 투플에서 외래키의 값이 참조되는 릴레이션의 기본키 값으로 존재하지 않는 경우
  5. 널에 대한 제약 조건: 엔티티 제약 조건에 포함
- 제약조건 위반 시, 삽입 거부 또는 사용자에게 알려 정정 요청
### 삭제 연산
- 참조(무결성) 제약 조건: 삭제하려는 투플을 다른 투플에서 참조하고 있는 경우
- 제약조건 위반 시
  1. 삭제 거부
  2. 삭제되는 투플을 참조하는 투플들까지 모두 삭제(연쇄 삭제)
  3. 삭제되는 투플을 참조하는 투플들에서 외래키 값을 널로 바꾸거나 다른 유요한 투플을 참조하도록 변경
### 수정 연산
- 수정 연산은 기본적으로 '삭제 후 삽입'이 원칙
- PK나 FK가 아닌 애트리뷰트 값 변경은 문제 X
- 도메인 제약조건 위반 여부만 확인하면 됨

# 관계 모델 용어
- 행 = 투플 = 레코드
- 열 = 애트리뷰트
- 테이블 = 릴레이션 = 엔티티
### 도메인(Domain)
- 원자값들의 집합
### 데이터 타입
- 도메인은 실제 데이터 타입으로 명시함
- 정수, 실수와 같은 표준 숫자형
- 문자, 고정길이 문자열, 가변길이 문자열
- 날짜, 시간
- 타임스탬프
- 화폐단위 등
### 릴레이션 스키마 (Relation schema)
- 릴레이션 이름과 애트리뷰트들의 집합으로 표기
- 릴레이션의 차수(Degree): 릴레이션의 애트리뷰트 개수
### 표기법
- 릴레이션 스키마 = Q, R, S등
- 릴레이션 상태 = q, r, s등(Q, R, S와 대응)
- 투플 = t, u, v등
### 슈퍼키(Superkey, SK)
- 어떠한 투플도 동일한 SK는 가지면 안됨
- 여러 애트리뷰트를 포함(최소 1개 이상의 애트리뷰트가 포함되어 있어야 함 => 최소 슈퍼키)
### 기본키(Primary key, PK)
- 일반적으로 릴레이션은 여러 키를 가질 수 있는데, 이들을 후보기라고 함
- 릴레이션이 여러 후보키를 가지면 이중 하나를 임의로 선택하여 기본키로 지정
- 기본키 = 밑줄로 표시
- 물리적인 인덱스 등을 구성하여 접근속도 향상
### 외래키(Foregin key, FK)
- 특정 애트리뷰트가 다른 애트리뷰트를 참조하면 참조하는 애트리뷰트를 외래키라고 함
