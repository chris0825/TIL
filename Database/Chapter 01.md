# 데이터베이스 개요
### 데이터(Data)
- 의미를 가지면서 기록될 수 있는 알려진 사실
### 데이터베이스(Database)
- 서로 연관이 있는 데이터들의 모임
### 데이터베이스 관리 시스템(DBMS: DataBase Management System)
- 데이터베이스의 생성과 관리를 담당하는 소프트웨어 패키지
- DBMS는 운영체제와 함께 중요한 시스템 소프트웨어 패키지로 분류
### 데이터베이스 시스템 = DBMS + 응용 프로그램 = DBMS
### 작은 세계(UoD: Universe of Database, Mini-World)
- 데이터베이스 구축의 대상이 되는 실세계의 일부분
- 데이터베이스는 특정한 목적을 위해 구축 및 운용되며, 이는 그 목적에 적합한 작은 세계를 구축하는 것에 해당

|파일 처리|데이터베이스|
|:-|:-|
|응용 프로그램 작성(설계)자가 데이터(=파일) 구조를 결정<br>응용 프로그램은 결정된 구조에 따라 데이터를 접근하거나 갱신<br>데이터 공유의 개념이 없음(적음)|데이터는 한 곳에 저장되고, 여러 응용 프로그램이 목적에 맞게 이를 사용<br>데이터 공유의 개념이 기본|

# 데이터베이스의 특징
### 데이터베이스 시스템의 자기 기술성(Self-describing)
### 프로그램과 데이터의 분리(격리) = 프로그램-데이터 독립성
- 데이터베이스 내의 데이터 저장 구조가 변경되어도 데이터베이스 응용 프로그램은 영향을 받지 않음
- 데이터에는 정해진 인터페이스(질의)를 통해 액세스
### 데이터 추상화(Data abstraction)
- 데이터 모델(Data model)을 사용하여 저장 구조의 자세한 내용은 사용자로부터 은닉시키고, 사용자에게는 각자의 요구에 맞는 개념적인 뷰만 제공
### 데이터에 대한 다양한 뷰(View) 제공
- 사용자는 전체 데이터베이스 보다는 관심이 있는 데이터베이스의 일부를 뷰로 정의할 수 있음
### 데이터의 공유와 다수 사용자 트랜잭션 처리
- 여러 사용자가 (동시에) 동일한 데이터베이스를 공유 가능하도록 지원
- 동시에 사용하더라도 일관성(Consistency)을 보장하기 위한 동시성 제어(Concurrency control) 기능 제공
### 트랜잭션 주요 성질
- 원자성 Atomicity = 트랜잭션은 수행되었거나, 아님 말거나
- 일관성 Consistency = 데이터베이스 상태는 일관되어야 함
- 고립성 Isolation = 트랜잭션이 마치 혼자서 수행된 것 같아야 함
- 지속성 Durability = 한번 반영된 정보는 지속적으로 반영되어 있어야 함

**= ACID**

# 데이터베이스 사용자의 분류
### 데이터베이스 관리자(DBA: DataBase Administrator)
- 데이터베이스 시스템의 관리를 총괄하여 책임진 사람
- DBMS 자체는 물론 데이터베이스 구축, 관리에 해박한 지식과 많은 경험 요구
### 데이터베이스 설계자(Database designer)
- 데이터베이스의 설계를 책임진 사람
- 실세계 현상을 모델링하는 기술이 요구됨
### 최종 사용자
- 데이터베이스에 대하여 질의하고, 변경하고, 보고서를 작성하는 사람
- 비정기적인 데이터베이스 사용자, 매번 다른 형태 질의를 수행하는 중상급의 관리자
- 미리 일정한 용도로 작성된 프로그램을 사용하는 사용자
- DBMS 기능을 이용하는 응용 개발자
### 시스템 분석가/응용 프로그래머(소프트웨어 공학자)
- 초보 사용자를 위하여 잘 정의된 기능의 응용을 분석/설계하고 구현하는 사람
- 그래픽 인터페이스 등의 구현을 통해 최종 사용자의 이용 편의성을 제공
### DBMS 설계 및 구현자
- DBMS 소프트웨어 자체를 설계하고 구현하는 업무를 담당하는 사람들
- 응용 및 시스템 프로그래밍에 익숙하고, DB이론에 해박한 전문가
### 도구 개발자
- 데이터베이스를 사용하는데 필요한 도구들을 설계하고 구현하는 사람들
- 일반적으로 DBMS 엔진 업체와는 별도의 많은 업체가 개발하여 판매
### 운영 및 유지 보수 요원
- 데이터베이스 시스템 운영에 필요한 HW및 SW 운영 및 유지보수 담당 요원들
- 전문적 지식은 부족해도 시스템의 청소, 백업 파일 관리 등 꼭 필요한 업무 수행

# DBMS의 장점
### 데이터 중복성(Redundancy)의 제어 및 중복의 최소화
- 동일한 데이터가 이곳 저곳에 중복되어 저장되는 것을 방지
- 중복 제어를 통한 데이터의 일치성(Consistency) 보장
- 중복 최소화를 통한 메모리 낭비 방지
- 제어된 중복과 데이터 불일치
  |제어된 중복|데이터 불일치|
  |:-|:-|
  |성능 향상을 위해서, 응용 프로그램 책임 하에 데이터를 중복 관리함|중복 저장으로 인해 발생하는 불일치|

**데이터를 독립/유일적으로 두면 각 데이터간 연동/조인/부분집합을 해야 하지만, 자주 발생하는 질의의 경우 중복을 허용하면 성능 향상**
**제어된 중복 사용 시, 책임이 중요. 수정 시 중복 데이터 같이 수정해야 함**

### 보안 기능
- 권한 없는 사용자의 데이터 접근을 통제
- 데이터의 중요성에 따른 다양한 형태의 접근 권한을 부여
- 다양한 권리를 가지는 다양한 접근 제어
### 지속성(영속성 Persistence) 기억 공간 제공
- 프로그램 수행이 끝나더라도 관련 데이터/객체는 그 값을 저장하고 있어야 함
- 데이터를 데이터베이스에 영구적으로 보관/저장
- 데이터를 관리하는 프로그램 객체 자체도 지속성 기억 공간에 저장/관리
### 효율적 질의처리를 위한 저장 구조 제공
- 레코드의 신속한 검색을 위해 인덱스 제공
- 질의 처리 최적화 모듈을 통해 최적의 질의 수행 계획 선택
### 백업(Backup)과 회복(Recovery) 기능 제공
- 시스템 고장 시에도 데이터의 일관성 보장
### 다수의 사용자 인터페이스 제공
- 초보 사용자 -> GUI I/F
- 응용 프로그래머 -> 프로그래밍 언어 I/F
- 전문 사용자 -> SQL I/F
### 데이터베이스의 무결성(Integrity) 제약 조건의 시행
- 각 속성 값이 가져야 하는 제약 조건
- 테이블들 사이에 가져야 하는 제약 조건
### 규칙을 사용한 추론과 수행
- 연역적 규칙을 이용하여 데이터베이스에 저장된 사실로부터 새로운 정보를 추론
- 자동으로 수행되는 능동 규칙의 정의 및 실행
### 동시성 제어 기능 제공(트랜잭션 개념)
- 여러 사용자가 동시에 DB를 접근하여 효율적으로 처리
- 동시 접근 시에도 데이터의 손실 방지, 일관성 보장
### 데이터 독립성 제공(데이터와 프로그램의 분리)
- 데이터베이스를 쉽게 사용할 수 있게 함
- 응용 프로그램 개발이 용이
- 내부 저장 구조를 변경하기 용이
- 프로그램 및 데이터베이스 유지 보수가 용이

# 데이터베이스 사용의 효과
### 표준화된 데이터 관리
- 조직 내 모든 부서에서 표준화된 문서 관리로 업무 효율성 증대
- 부서, 프로젝트, 사용자 사이 의사 교환 및 협조 용이
### 응용 프로그램 개발 시간 단축
- 응용 프로그램의 상당한 부분을 DBMS 및 관련 소프트웨어가 처리
- DBMS 사용하면 전통적 파일 시스템 사용할 때 보다 개발 시간 단축
### 데이터 구조 변경에 융통성 부여
- DB 내부의 자료 구조가 변경 되어도 사용자에 대한 영향 거의 X
- DBMS는 기존 데이터, 응용 프로그램에 영향을 주지 않고 내부 구조 변경이 가능
### 항상 최신의 정보 제공 => 실시간성
- 사용자 중 한 사람의 갱신으로 나머지 사람은 즉시 변경된 값 접근 가능
### 규모의 경제성
- 부서마다 다른 방식으로 자료를 관리하는 것보다 통합 DB로 관리하는 것이 전체적 관점에서 저비용(반대로 소규모는 투머치)

# 데이터 모델
- 데이터 추상화를 제공하기 위한 주요 도구
- 데이터베이스 구조를 명시하기 위해 사용할 수 있는 개념들의 집합
- 데이터베이스에서 검색과 갱신을 수행하는 기본 연산들의 집합을 포함
### 데이터 모델 개념의 변화
- DB 응용의 동적 측면 또는 행동을 명시하기 위한 개념들(ex 정의 연산)이 점차적으로 데이터 모델에 포함
### 데이터 모델의 분류
||물리적(저수준) 데이터 모델|표현(구현) 데이터 모델|개념적(고수준) 데이터 모델|
|:-|:-:|:-:|:-:|
|데이터 세부 사항|명시|은폐(구현 가능)|구현 어려움|
|하드웨어|의존적|-|독립적|
|일반인 이해도|어려움|개념 제공|쉬움|
|특징|레코드 형식/순서, 접근경로 정의||엔티티 관계 다이어그램|

# 용어 정리
**- 데이터 항목(Data item) =** 레코드를 저장하는 항목(Attribute)<br>
**- 데이터 타임(Data type) =** 데이터 항목이 가질 수 있는 값<br>
**- 관계(Relationship) =** 여러 파일에 속하는 레코드들 사이의 연관성<br>
**- 데이터베이스 카탈로그(Catalog) =** 메타 데이터(Meta-data)가 저장되어 있음<br>
**- 메타 데이터(Meta-data) =** 데이터베이스 자체에 대한 정보를 말함<br>
**- 트랜잭션(Transaction) =** 데이터베이스 작업을 수행하는 작업 단위<br>
