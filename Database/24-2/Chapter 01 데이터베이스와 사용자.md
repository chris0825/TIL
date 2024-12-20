# 데이터베이스 특징
## 파일 처리
- 응용 프로그램 작성(설계)자가 데이터(파일) 구조를 결정
- 응용 프로그램은 결정된 구조에 따라 데이터를 접근 및 갱신
- 데이터 공유의 개념이 없음(적음)<br>
ex) 성적 관리 부서와 회계 부서가 따로 데이터를 구축하고, 필요한 응용 프로그램을 작성하여 사용( 데이터 중복 발생 )
## 데이터베이스
- 데이터는 한 곳에 저장되고, 여러 응용 프로그램이 목적에 맞게 이를 사용 (데이터 공유 개념)<br>
ex) 데이터는 데이터베이스에 관리하고, 각각의 응용(성적 관리, 회계)은 이를 필요에 따라 사용
## 데이터베이스의 주요 특징
### 데이터베이스 시스템의 자기 기술성(self-describing)
> 데이터베이스에 대한 정의를 가지며, 이를 DBMS catalog에 저장
- 메타 데이터(meta-data)
  > 카탈로그에 저장된 데이터베이스 구조에 대한 정보<br>
  > 데이터베이스 파일 구조, 데이터 항목의 타입과 저장 형식, 데이터에 대한 다양한 제약 조건 등
### 프로그램과 데이터의 격리(program-data independence, 프로그램-데이터 독립성)
  > 데이터베이스 내의 데이터 저장 구조가 변경되어도 데이터베이스 응용 프로그램은 영향을 받지 않는(변경될 필요가 없는) 성질<br>
  > 데이터에는 정해진 인터페이스(데이터베이스 질의)를 통해 액세스
### 데이터 추상화 (data abstraction)
  > 데이터 모델(data model)을 이용하여 데이터의 저장 구조 및 위치, 구현에 대한 상세한 정보는 숨기고 데이터에 대한 개념적인 표현만을 제공
### 데이터에 대한 다중 뷰(view) 제공
  > 전체 데이터베이스 대신 사용자가 관심 있는 관점만을 뷰로 정의하여 제공<br>
  > 뷰는 데이터베이스의 일부이거나 데이터베이스로부터 유도된 가상 데이터(virtual data)
### 데이터의 공유와 다수 사용자 트랜잭션 처리
  > 여러 동시 사용자들(concurrent users)이 같은 데이터베이스를 검색하고 갱신할 수 있음<br>
  > 다수 사용자가 동일한 데이터를 동시에 변경하더라도 일관성(consistency)을 보장하기 위한 동시성 제어(concurrency control)제공<br>
  
  ex) 여러 에이전트에서 같은 항공기 좌석을 예약할 때, 한 좌석은 한 사람에게만 배정함.
  - 트랜잭션
    > DB 작업(읽기, 쓰기)을 수행하는 단위 프로그램 또는 프로세스
  - 트랜잭션의 주요 성질
    - 고립성(isolation)
      > 각 트랜잭션은 다른 트랜잭션들로부터 고립되어 수행되는 것처럼 보이도록 보장
    - 원자성(atomicity)
      > 한 트랜잭션 내의 모든 연산은 완전히 수행되거나 아무 연산도 수행되지 않음을 보장
## 데이터베이스 사용의 장점
### 중복성(redundancy)의 제어
> 동일한 데이터가 여러곳에 중복되어 저장되는 것을 방지하기 위함
- 중복성의 문제
  - 데이터를 변경할 때 중복된 횟수만큼 반복해야 함
  - 메모리가 낭비됨
  - 데이터의 불일치(inconsistency)문제가 발생할 수 있음
- 데이터 정규화(normalization)를 통해 일관성 유지, 저장공간 절약
- 제어된 중복(controlled redundancy)
  - 질의 성능 향상을 위해서 데이터의 중복을 허용 => 반정규화(denormalization)
  - 데이터의 불일치 현상(제어되지 않은 중복)이 발생되지 않도록 제어
### 보안(security)과 권한(authorization)
- 권한 없는 사용자의 데이터 접근을 통제
- 데이터의 중요성에 따른 다양한 형태의 접근 권한을 차등 부여
- DBA만 실행할 수 있는 특권 소프트웨어(privileged software)로 사용자 생성, 접근 권한 부여
### 지속성 기억 공간 제공
- 프로그램 수행이 끝나더라도 관련 데이터/객체는 그 값을 저장하고 잇어야 함
- 데이터를 데이터베이스에 영구적으로 보관/저장
- 데이터를 관리하는 프로그램 객체 자체도 지속성 기억 공간에 저장/관리
### 효율적 질의 처리를 위한 저장 구조 제공
- 레코드의 신속한 검색을 위해 인덱스 제공
- 질의 처리 최적화 모듈을 통해 최적의 질의 수행 계획 선택
### 백업(backup)과 회복(recovery) 기능 제공
- 시스템 고장 시에도 데이터의 일관성을 보장
### 다수의 사용자 인터페이스 제공
- 각 사용자에게 적합한 인터페이스를 제공
### 데이터간 복잡한 관계의 체계적 표현
- 테이블간의 복잡하고 다양한 관련성을 표시
### 무결정 제약조건(integrity constraint)의 시행
- 데이터 항목별 데이터 타입을 검사
- 한 테이블의 레코드는 다른 테이블의 레코드와 연관성을 가져야 함
- 키 값에 대한 제약
### 규칙을 사용한 추론과 수행
- 연역적 규칙을 이용하여 데이터베이스에 저장된 사실로부터 새로운 정보를 추론
- 자동으로 수행되는 능동 규칙의 정의 및 실행(트리거 기능을 통해 저장된 절차(stored procedure) 수행)
### 동시성 제어 기능 제공(트랜잭션 개념)
- 여러 사용자가 동시에 DB를 접근하여 효율적으로 처리
- 동시 접근 시에도 데이터의 손실을 방지하고 일관성을 보장
### 데이터 독립성 제공(데이터 프로그램의 분리)
- 데이터베이스를 쉽게 사용할 수 있게 함
- 응용 프로그램 개발이 용이
- 내부 저장 구조를 변경하기 용이
- 프로그램 및 데이터베이스 유지 보수가 용이
## 데이터베이스 사용의 추가적인 효과
### 표준화된 데이터 관리
### 응용 프로그램의 개발 시간 단축
### 데이터 구조 변경에 융통성 부여
### 항상 최신의 정보를 제공(실시간성)
### 규모의 경제성(economics of scale)
## Summary
### 기존 파일 처리 시스템 대비 데이터베이스의 특징
- 카탈로그(메타 데이터), 프로그램-데이터의 독립성, 프로그램-연산의 독립성
- 데이터 추상화, 다중 뷰 지원, 여러 트랜잭션 간 데이터 공유
### 기존 파일 처리 시스템 대비 데이터베이스의 장점
- 표준화 강화, 응용 개발 시간의 단축, 융통성 증가
- 최신 정보를 즉시 이용, 규모의 경제성
