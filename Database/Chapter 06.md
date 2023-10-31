# 질의 결과 정렬
### ORDER BY 절
- Default: 오름차순(ASC)
- 오름차순 정렬: ORDER BY ATTRIBUTE ASC
- 내림차순 정렬: ORDER BY ATTRIBUTE DESC

# 삽입, 삭제, 갱신
### INSERT 문
- 릴레이션에 투플 하나 추가
- INSERT INTO SCHEMA VALUES();
- INSERT INTO SCHEMA() VALUES(); -> 제약조건에 따라 삽입 실패 가능성
### SELECT와 결합된 INSERT
- 질의의 결과로 생성된 여러 투플들을 또 다른 릴레이션에 삽입하는 경우
- INSERT INTO SCHEMA SELECT-FROM-WHERE 문
### DELETE 구문
- 릴레이션에서 투플들을 제거하는 명령
- WHERE 절 조건 만족하는 투플 모두 삭제(WHERE 생략 시 테이블 제외 모두 삭제)
### UPDATE 구문
- 투플의 애트리뷰트 값을 수정하기 위해 사용
UPDATE SCHEMA
SET ATTRIBUTE='Attribute', ATT2 = 'att2'
WHERE ATT = Att;

# SQL 기타 기능
### 권한 부여/취소
- SQL은 데이터베이스 사용자에게 권한을 부여하고 취소하는 기능 제공
- GRANT/REVOKE 구문 사용
### 호스트 언어와 결합되어 사용
- SQL은 다른 범용 프로그래밍 언어 내에서 사용될 수 있음
### 트랜잭션 기능
- SQL: 트랜잭션 제어 명령문 가짐
- 동시성 제어(ACID)와 회복
### VIEW 관련 명령어 (TABLE과 유사)
- 가상 테이블 생성
- CREATE VIEW, DROP VIEW
### 인덱스 생성/삭제 명령어
- CREATE INDEX, DROP INDEX
- 물리적 데이터베이스 설계 매개변수와 릴레이션을 위한 파일 구조, 인덱스와 같은 접근경로를 명시하기 위한 명령어 집합 보유

# VIEW 특성
- SQL에서 뷰는 다른 테이블들에서 유도된 가상 테이블
- 기본 테이블들의 열로 구성
- 뷰에 대한 질의는 아무런 제한을 받지 않음
- 몇 개 연산들을 뷰로 표현하여 사용하는데 편리함
- 데이터 접근제어로 보안성 제공
- 뷰에 적용할 수 있는 갱신(삽입, 삭제) 연산들은 제한됨
