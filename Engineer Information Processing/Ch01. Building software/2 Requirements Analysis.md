# 요구사항 분석
## 요구 사항
  > 어떤 문제를 해결하기 위해 필요한 조건 및 제약사항을 요구<br>소프트웨어 개발/유지보수 과정에서 필요한 기준과 근거를 제공
## 요구사항의 유형
### 기능적 요구사항
  > 실제 시스템 수행에 필요한 기능 관련 요구사항<br>Ex) 금융 시스템은 조회/인출/입금/송금 기능이 있어야 한다
### 비기능적 요구사항
  > 성능, 보안, 품질, 안정성 등 실제 수행에 보조적인 요구사항<br>Ex) 모든 화면이 3초 이내에 사용자에게 보여야 한다
## 요구사항 개발 프로세스(순서 중요)
### ① 도출/추출
  > 이해관계자들이 모여 요구사항 정의(식별하고 이해하는 과정)<br>Ex) 인터뷰, 설문, 브레인스토밍, 청취, 프로토타이핑, 유스케이스
### ② 분석
  > 사용자 요구사항에 타당성 조사<br>비용 및 일정에 대한 제약 설정<br>Ex) 관찰, 개념 모델링, 정형 분석, 요구사항 정의 문서화
### ③ 명세
 > 요구사항 체계적 분석 후 승인이 가능하도록 문서화
### ④ 확인/검증
  > 요구사항 명세서가 정확하고 완전하게 작성됐는지 검토
## 요구사항 분석 도구
### 요구사항 분석 CASE(Computer Aided SW Engineering)
- **SADT**: SoftTech사에서 개발, 구조적 분석 빛 설계 분석
- **SREAM**: 실시간 처리 SW 시스템에서 요구사항에 명확한 기술을 하기 위함
- **PSL/PSA**: 문제 기술언어 및 요구사항 분석 보고서 출력
- **TAGS**: 시스템 공학 방법 응용에 대한 자동 접근 방법
### HIPO(Hierarchy Input Process Output)
  > 하향식 설계 방식<br>가시적, 총체적, 세부적 다이어그램으로 구성<br>기능과 자료의 의존 관계 동시 표현<br>이해가 쉽고 유지보수 간단
## 구조적 분석 모델
### 데이터/자료 흐름도(DFD, Data Flow Diagram)
- **원**: 프로세스(Process)<br>
- **화살표**: 자료 흐름(Flow)<br>
- **평행선**: 자료 저장소(Data store)<br>
- **사각형**: 단말(Terminator)<br>
  **-> 구조적 분석 기법에 이용 / 시간 흐름 명확한 표현 불가 / 버블(Bubble) 차트**
### 자료 사전(DD, Data Dictionary)
  > 자료 흐름도에 기재된 모든 자료의 상세 정의/설명

|=|[ ]|( )|+|**|{ }|
|:-:|:-:|:-:|:-:|:-:|:-:|
|정의|택일/선택|생략|구성|설명/주석|반복|

### 소단위 명세서
### 개체 관계도(ERD, Entity Relationship Diagram)
### 상태 전이도
## 객체지향 분석 모델
### Booch(부치)
  > 미시적, 거시적 개발 프로세스를 모두 사용(클래스/객체 분석 및 식별)
### Jacobson(제이콥슨)
  > Use case를 사용 (사용자, 외부 시스템이 시스템과 상호작용)
### Coad-Yourdon
  > E-R 다이어그램 사용/객체의 행위 모델링
### Wirfs-Brock
  > 분석과 설계 구분이 없고 고객 명세서 평가 후 설계 작업까지 연속해서 수행함
### <ins>Rumbaugh(럼바우)</ins>
  > 가장 일반적으로 사용, 객체/동적/기능 모델로 구분됨
  - **객체 모델링(Object)** -> 객체 다이어그램 / 객체들 간의 관계를 규정 및 정의
  - **동적 모델링(Dynamic)** -> 상태 다이어그램 / 시스템 동적 행위를 기술
  - **기능 모델링(Function)** -> **자료 흐름도(DFD)** / 다수의 프로세스들 간의 처리 과정을 표현
## 요구사항 명세
### 정형 명세
  > 수학적 원리<br>정확하고 간결한 요구사항 표현 가능<br>어려운 표기법으로 사용자 이해가 힘듦(VDM, Z, Petri-net, CSP)
### 비정형 명세
  > 자연어, 그림 중심<br>쉬운 자연어 사용으로 의사소통이 용이하나 작성자에 따라 모호한 내용으로 일관성이 떨어짐(FSM, Decision Table, E-R 모델, State Chart)
