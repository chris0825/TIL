### 자동 재전송 요구 (ARQ, Automatic Repeat reQuest)
: 수신자가 송신자에게 데이터 수신 상태를 알려주어 재전송을 기반으로 하는 신뢰적인 데이터 전송 프로토콜

### 긍정 확인 응답(ACK, positive ACKnowledgment)
  : 오류없이 데이터를 수신했을 때 수신자가 송신자에게 보내는 응답

### 부정 확인 응답(NAK, Negative AcKnowledgment)
  : 수신받은 데이터에 오류가 있을 경우 송신자에게 보내는 부정 응답
  : 중복 ACK도 NAK과 같은 역할 (1 전송 1 대답이 정상인데 1 전송에 2 대답이 왔다는것은 무언가 잘못됐다는 것을 의미)

### 시분할 다중화 (TDM, Time-Division Multiplexing)
### 주파수 분할 다중화 (FDM, Frequency-Division Multiplexing)
### 왕복 시간(RTT, Round-Trip Time)
### TTL (Time-To-Live)
### 소프트웨어 정의 네트워킹 (SDN, Softwar-Defined Networking)
### 인터넷 제어 메시지 프로토콜 (ICMP, Internet Control Message Protocol)
### SNMP (Simple Network Management Protocol)
### 네트워크 기능 가상화 (NFV, Network Functions Virtualization)



# Chapter 5. 네트워크 계층: 제어 평면

### 제어 에이전트(CA, Control Agent)

### 링크 상태(LS, Link-State)
: 중앙 집중형, 완전한 전체 정보 가짐 -> 다익스트라 알고리즘 / 프림 알고리즘
### 거리 벡터(DV, Distance-Vector)
: 분산형, 직접 연결된 링크 정보만 가짐, 반복적, 비동기적 -> 벨만-포드 알고리즘

### 자율 시스템 (AS, Autonomous System)

### 개방형 최단 경로 우선 (OSPF, Open Shortest Path First)
: 링크 상태 정보를 플러딩하고 다익스트라 최소 비용 경로 알고리즘을 사용하는 링크 상태 알고리즘

### 경계 게이트웨이 프로토콜 (BGP, Border Gateway Protocol)

### MOSPF (Multicast OSPF)
: 멀티캐스트 라우팅 기능을 제공하기 위해 OSPF를 단순 확장
: 기존의 OSPF 링크 데이터베이스를 사용하고 OSPF 링크 상태 브로드캐스트 메커니즘에 새로운 형태의 링크상태 일림 추가

### CIDR (Classless Inter-Domain Routing)

### 외부 BGP(eBGP, external BGP)
### 내부 BFP(iBGP, interal BGP)

### 네트워크 기능 가상화 (NFV, Network Functions Virtualization)
: SDN의 일반화 = 단순한 상용 서버, 스위칭 및 저장소를 가지고 복잡한 미들박스를 혁신적으로 교체하는 것

### 인터넷 제어 메시지 프로토콜 (ICMP, Internet Control Message Protocol)
: 호스트와 라우터가 서로 간 네트워크 계층 정보를 주고받기 위해 사용

### 계약된 서비스 수준 계약 (SLA, Service Level Agreement)

### 네트워크 운영 센터 (NOC, Network Operations Center)

### 명령줄 인터페이스 (CLI, Command Line Interface)

### MIB (Management Information Base)

### SMI (Structure of Management Information)

### PDU (Protocol Data Unit)

### 원격 프로시저 호출(RPC, Remote Procedure Call)

### TLS (Transport Layer Security)

### 최대 전송 단위 (MTU, Maximum Transmission Unit)



# Chapter 6. 링크 계층과 근거리 네트워크

### AP (Access Point)

### 매체 접속 제어 (MAC, Midium Access Control)

### 네트워크 인터페이스 컨트롤러 (NIC, Network Interface Controller)

### 오류 검출 및 정정 (EDC, Error Detection and Correction)

### 순방향 오류 정정 (FEC, Forward Error Correction)
: 오류를 검출 및 정정하는 수신자의 능력

### 순환 중복 검사 코드 (CRC, Cyclic Redundancy Check = 다항식 코드, Polynomial Code)
: 

### 점대점 링크 (Point-to-Point Link)

### PPP (Point-to-Point Protocol)

### HDLC (High-level Data Link Control)

### 코드 분할 다중 접속 (CDMA, Code Division Multiple Access)

### 알로하 프로토콜(ALOHA)

### CSMA (Carrier Sense Multiple Access)

### CSMA/CD (CSMA with Collision Detection)

### FDDI (Fiber Distributed Data Interface)

### 케이블 모뎀 종단 시스템 (CMTS, Cable Modem Termination System)

### DOCSIS (Data-Over-Cable Service Interface Specifications)

### ARP(Address Resolution Protocol)
