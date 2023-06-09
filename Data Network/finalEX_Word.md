# 3.4 신뢰적인 데이터 전송의 원리
### 신뢰적인 데이터 전송 프로토콜(Reliable data transfer protocol)
  - 신뢰적인 채널에서는 전송된 데이터가 손상되거나 손실되지 않는다
  - 모든 데이터는 전송된 순서 그대로 전송된다
### 단방향 데이터 전송(Unidirectional data transfer)
  - 송신측으로 부터 수신 측까지의 데이터 전송만을 고려
### 양방향(전이중) 데이터 전송(Bidirectional data transfer)
  - rdt의 송신 측과 수신 측은 전송 데이터를 포함하는 패킷을 교환하는 것 외에 제어 패킷을 양쪽으로 전송해야 한다
  - rdt의 송신 측과 수신 측 모두 udt_send()를 호출함으로써 다른 쪽에 패킷을 전송한다
    ㄴ UDT는 비신뢰적인 데이터 전송(Unreliable data transfer)

## > rdt1.0: 완벽하게 신뢰적인 채널상에서의 신뢰적인 데이터 전송
### 유한상태 머신(FSM, Finite-state machine)
  - 송/수신자에 대해 분리된 FSM존재

## > rdt2.0: 비트 오류가 있는 채널상에서의 신뢰적 데이터 전송
### 긍정 확인응답(ACK, Positive Acknowledgment, OK)
  - 일반 시나리오에서 메시지 수신자는 각각의 문장을 듣고 이해하고 기록한 후에 OK라고 말함
### 부정 확인응답(NAK, Negative Acknowledgment, 그것을 반복해주세요)
  - 문장을 올바르게 듣지 못했다면 반복하라고 요청함
  - 같은 패킷에 대해 2개의 ACK(중복 ACK 수신)을 수신한 송신자는 수신자가 두번 ACK한 패킷의 다음 패킷을 정확하게 수신하지 못했다고 인지
    - 중복ACK = NAK
### 자동 재전송 요구(ARQ, Automatic Repeat reQuest)
  - 정확하게 수신되었는지 또는 잘못 수신되어 반복이 필요한지를 수신자가 송신자에게 알려주어 재전송을 기반으로 하는 신뢰적인 데이터 전송 프로토콜
### 오류 검출
: 비트 오류가 발생했을 때 수신자가 검출할 수 있는 기능
### 수신자 피드백
: 긍정 확인응답(ACK), 부정 확인응답(NAK)
### 재전송
: 오류를 가지고 수신된 패킷은 송신자에 의해 재전송
### 전송 후 대기(Stop-and-Wait)
  - 송신자는 수신자가 현재의 패킷을 정확하게 수신했음을 확신하기 전까지 새로운 데이터를 전달하지 않음
### 중복 패킷(Duplicate packet)
  - 송신자가 왜곡된 ACK/NAK 패킷을 수신할 때 현재 데이터 패킷을 단순히 다시 송신하는 것
### 순서 번호(Sequence number)
  - 데이터 패킷에 송신자가 번호를 붙임
  - 수신자는 수신된 패킷이 재전송인지를 결정할 때 순서 번호만 확인하면 됨

## > rdt3.0: 비트 오류와 손실 있는 채널상에서의 신뢰적인 데이터 전송
### 카운트다운 타이머(Countdown Timer)
  - 매 패킷이 송신된 시간에 타이머 시작
  - ACK or NAK 수신 / 아무것도 수신받지 않음
  - 타이머 종료
### 얼터네이팅 비트 프로토콜(Alternating-bit Protocol)
  - 패킷의 순서 번호가 0과 1이 번갈아 나타남
### 이용률 (또는 효율, Utilization)
### 유효 처리량(Effective Throughput)
### 파이프라이닝(Pipelining)
  - 확인 응답들(ACK/NAK)을 기다리기 전에 송신자가 N개의 패킷을 전송하도록 허용한다면 송신자의 이용률은 N배가 됨
### N부터 반복(GBN, Go-Back-N)
  - 확인 응답을 기다리지 않고 여러 패킷을 전송
  ### 윈도 크기(Window size)
    - 순서번호 공간에서 응답 없이 전송 받을 수 있는 크기
  ### 슬라이딩 윈도 프로토콜(Sliding-Window Protocol)
    - 순서번호 순으로 응답이 완료되면 응답이 된 만큼 순서번호 공간에서 오른쪽으로 밀림
  ### 누적 확인응답(Cumulative Acknowledgment)
    - N까지 순서 번호를 가진 모든 패킷이 정상 수신 되면 N까지에 대한 확인 응답 전송
  ### 이벤트 기반 프로그래밍(Event-Based Programming)
    - 다양한 이벤트에 대한 대응으로 취할 수 있는 동작 구현
### 선택적 반복(SR, Selective Repeat)
  - 수신자에서 오류가 발생한 패킷을 수신했따고 의심되는 패킷만을 송신자가 재전송
  - 각각의 개별적인 재전송은 수신자가 올바르게 수신된 패킷에 대한 개별적인 확인 응답 요구

# 3.5 TCP: 연결 지향형 트랜스포트
### 연결지향형(Connection-Oriented)
  - 애플리케이션 프로세스가 데이터를 다른 프로세스에게 보내기 전에, 두 프로세스가 서로 '핸드 셰이크'를 먼저 해야함
### 전이중 서비스(Full-Duplex Service)
  - 애플리케이션 계층 데이터는 A, B동시에 흐를 수 있음
### 점대점(Point-to-Point)
  - 단일 송신자와 단일 수신자
### 클라이언트/서버 프로세스 (Client/Server Process)
  - 클라이언트 프로세스 = 연결을 초기화하는 프로세스
  - 서버 프로세스 = 다른 프로세스
### 세 방향 핸드셰이크(Three-way Handshake)
  - 두 호스트 사이에 3개의 세그먼트가 오감
### 송신 버퍼(Send Buffer)
### 최대 세그먼트 크기(MSS, Maximum Segment Size)
  - 세그먼트로 모아 담을 수 있는 최대 데이터 양
### TCP 세그먼트(TCP Segment)
  - TCP헤더 + 클라이언트 데이터

### > TCP 세그먼트 헤더를 구성하는 필드
**- 출발지와 목적지 포트 번호(Source and Destination Port Number)**
> 상위 계층 애플리케이션으로부터 다중화와 역다중화를 하는 데 사용

**- 체크섬 필드(Checksum Field)**

**- 순서 번호 필드(Sequence Number Field)**

**- 확인응답 번호 필드(Acknowledgement Number Field)**

**- 수신 윈도(Receive Window)**

**- 헤더 길이 필드(Header Length Field)**

**- 옵션 필드(Option Field)**

**- 플래그 필드(Flag Field)**

  - ACK 비트: 성공적으로 수신된 세그먼트에 대한 확인응답 포함
  - RST, SYN, FIN 비트: 연결 설정/해제에 사용
  - PSH 비트: 수신자가 데이터를 상위 계층에 즉시 전달해야함을 가리킴
  - URG 비트: 이 세그먼트에서 송신 측 상위 계층 개체가 '긴급'으로 표시하는 데이터임을 지칭
            : 긴급 데이터 포인터 필드(Urgent Data Pointer Field)에 의해 가리켜짐
### 
