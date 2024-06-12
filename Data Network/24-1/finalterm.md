### GBN (Go-Back-N, N부터 반복) 프로토콜
### = 슬라이딩 윈도 프로토콜(Sliding-window protocol)
> 확인 응답을 기다리지 않고 여러 패킷을 전송
### 윈도 크기
> 아직 확인응답(ACK)이 오지 않은 패킷을 허용할 수 있는 순서 번호 범위
### 확장된 FSM(extended FSM)
> ?
### 누적 확인 응답(Cumulative acknowledgment)
> [GBN 프로토콜](#gbn-go-back-n-n부터-반복-프로토콜)에서 순서번호 n을 가진 패킷에 대한 확인 응답<br>
> 모든 것에 확인 응답을 받는 것이 아니라 정상 수신한 마지막 패킷 번호만 회신
### 이벤트 기반 프로그래밍(Event-based Programming)
> 다양한 이벤트에 대한 대응으로 취할 수 있는 동작을 구현
### SR(Selective Repeat, 선택적 반복)
> 수신자에서 오류(손실되거나 변조)가 발생한 패킷을 수신했다고 의심되는 패킷만을 송신자가 다시 전송하므로 불필요한 재전송을 피함<br>
> 개별적인 재전송은 수신자가 올바르게 수신된 패킷에 대한 개별적인 확인응답(ACK)을 요구
## TCP : 트랜스포트 계층(layer 4) 프로토콜
### 연결지향형
> 데이터를 보내기 전에 두 프로세스가 서로 '핸드셰이크'를 먼저 해야 함
### 전이중 서비스(full-duplex service)
> TCP 연결은 전이중 서비스를 제공
### 점대점(point-to-point)
> TCP 연결은 항상 단일 송신자와 단일 수신자 사이 점대점
### 클라이언트 프로세스(Client Process)
> 연결을 초기화하는 프로세스
### 서버 프로세스(Server Process)
> 클라이언트 프로세스가 아닌 것
### 세 방향 핸드 셰이크
> TCP 연결 시 두 호스트 사이 3개의 세그먼트가 보내지므로 세 방향 핸드셰이크라고 불림
### 송신 버퍼(send buffer)
> TCP는 초기 세 방향 핸드셰이크 동안 준비된 버퍼 중 하나인 연결의 송신 버퍼로 데이터를 보냄
---
### 최대 세그먼트 크기(MSS, Maximum Segment Size)
> 세그먼트로 모아 담을 수 있는 최대 데이터의 양
### 최대 전송 단위(MTU, Maximum Transmission Unit)
> 로컬 송신 호스트에 의해 전송될 수 있는 가장 큰 링크계층 프레임의 길이
### TCP 세그먼트 (TCP Segment)
> = TCP 헤더 + 클라이언트 데이터
### TCP 헤더
- 출발지와 목먹지 포트번호(Source and Destination port number)
- 체크섬 필드(Checksum field)
- 32bit 순서번호 필드(Sequence number field)
- 32bit 확인응답번호 필드(Acknowledgement number field)
- 16bit 수신 윈도(Receive window)
- 4bit 헤더길이 필드(Header length field)
- 가변 길이 옵션 필드(Option field)
- 6bit 플래그 필드(Flag field)
  - RST, SYN, FIN: 연결 설정과 해제
  - PSH: 수신자가 데이터를 상위 계층에 즉시 전달해야 함
  - URG: 송신 측 상위 계층 개체가 '긴급'으로 표시하는 데이터
- 16bit 긴급 데이터 포인터 필드(Urgent Data Pointer field)
### 세그먼트에 대한 순서번호
> 세그먼트에 있는 첫 번째 바이트의 바이트 스트림 번호
### 호스트가 자신의 세그먼트에 삽입하는 확인응답 번호는 다른 호스트에게 기대하는 다음 바이트의 순서번호를 의미
### TCP는 누적 확인 응답(Cumulative acknowledgment)를 제공
### 피기백(Piggybacked)
> 클라이언트/서버 데이터에 대한 확인 응답이 데이터 세그먼트 상에서 피기백 됨
### 지수적 가중 이동 평균(EWMA, Exponential Weighted Moving Average)
> 최신 샘플이 네트워크상 현재 ㅎ노잡을 더 잘 반영하기 때문에 최근 샘플에 높은 가중치를 부여<br>
> 가중치 갱신 절차가 진해오딤에 따라 빠르게 지수적으로 감소
$$추정된RTT = (1 - \alpha) 추정된RTT + \alpha \times sampleRTT  \tag{권장 a = 0.125}$$
### 신뢰적인 데이터 전송 서비스(Reliable data transfer service)
> TCP는 IP의 비신뢰적인 최선형 서비스에게 신뢰적인 데이터 전송 서비스를 제공
### 중복 ACK(Duplicate ACK)
> 송신자가 이미 이전에 받은 확인 응답에 대한 재확인 응답 세그먼트 ACK
### 빠른 재전송(Fast retransmit)
> 타이머가 만료되기 이전 손실 세그먼트 재전송
### 선택적 확인응답(Selective acknowledgment)
> 누적 확인응답과 달리 '순서가 틀린' 세그먼트에 대해 선택적 확인응답
### 흐름제어 서비스(flow-control service)
> 수신자가 수신받을 수 있는 만큼만 송신조절
### SYN 플러드 공격
> 공격자는 세번째 핸드셰이크를 완료하지 않은 무수한 TCP SYN 세그먼트를 보내 수 많은 연결 자원이 공격자에게 할당<br>
> = 합법적인 클라이언트의 서비스가 거부됨<br>
:arrow_forward: SYN쿠키로 해결 가능
### SYN 쿠키
> 세그먼트가 정당한 사용자로부터 왔는지 확인되기 전까지 연결을 만들지 않고 해시 함수를 보내 이를 ACK 세그먼트로 회신하면 연결을 열고 보내지 못하면 연결을 열어주지 않음
### 연결당-처리량(per-connection throughtput)
> 송신되는 데이터 양에 따른 수신되는 데이터의 양<br>
> 링크 용량을 넘기 전까지는 송신량 = 수신량링크 용량이 넘어가면 송신량이 늘어도 수신량은 동일(최대치)
### 패킷 도착률이 링크 용량에 근접함에 따라 큐잉 지연이 커진다
### 송신율 = 바이트/초
### 제공된 부하(Offered load)
> = 원래 데이터 + 재전송 데이터
- 재전송 데이터: 이전에 버려진 패킷
### 혼잡 제어
- 종단간 혼잡 제어
  > 세그먼트 손실이나 RTT가 증가하면 혼잡으로 받아들이고 윈도우 크기를 줄임
- 네트워크 지연 혼잡 제어
  > 라우터가 네트워크 안에서 혼잡 상태 관련하여 송수진자 모두에게 피드백을 전송
### ABR(Avilable Bite Rate)
> 혼잡제어에서 라우터가 자신이 출력 링크에 제공할 수 있는 전송률을 송신자에게 명확하게 전달 가능
### 혼잡 윈도(cwnd, Congestion WiNDow)
> TCP 송신자가 네트워크로 트래픽을 전송할 수 있는 속도에 제약을 가함
### 자체 클로킹(Self-clocking)
> TCP는 확인 응답을 혼잡 윈도 크기의 증가를 유발하는 트리거(trigger) 또는 클록(clock)을 사용
## TCP 혼잡제어 알고리즘(TCP congestion-control algorithm)
- 슬로 스타트(slow start)
- 혼잡 회피(congestion avoidance)
- 빠른 회복(fast recovery)
### 슬로 스타트(Slow start)
1. TCP 연결이 시작
    > 혼잡 윈도(cwnd) = 1MSS
2. 확인 응답을 받을 때마다 cwnd 지수적 증가
    > cwnd += 1MSS
3. 타임 아웃(혼잡) 발생
    > cwnd = 1MSS,<br>
    > 슬로스타트 임곗값(ssthresh) = cwnd / 2
4. 다시 cwnd 지수적 증가 하다가 sstrech 도달하면 '<ins>***혼잡 회피***</ins>'모드로 전환
### TCP 분할
> 클라우드 서비스에서 TCP의 슬로스타트로 인해 발생하는 성능 저하를 TCP 분할을 활용하여 개선할 수 있다
### 혼잡 회피(Congestion Avoidance)
> cwnd = 마지막_혼잡_발견시점 / 2
- RTT 마다 cwnd += 1MSS
### 빠른 회복
> cwnd값을 손실된 세그먼트에 대해 수신된 모든 중복된 ACK에 대해 MSS만큼 증가
### TCP 혼잡 회피 알고리즘 = 타임아웃이 발생한 슬로스타트
### TCP 타호(Tahoe)와 리노(Reno)의 혼잡 발생 시 혼잡 윈도 비교
- TCP 타호(Tahoe): 초기 TCP 버전
  > 슬로 스타트
- TCP 리노(Reno)
  > 빠른 회복

![혼잡 발생 시 타호와 리노 cwnd](../resource/타호와리노cwnd.png)
### TCP 혼잡제어 = AIMD
### 가법적 증가 승법적 감소(AIMD, additive-increase multiplicative-decrease)
> TCP의 혼잡제어는 RTT마다 1MSS씩 cwnd의 선형(가법적) 증가, 3개의 중복 ACK 이벤트에서 cwnd를 반감(승법적 감소)
### 명시적 혼잡 알림(ECN, Explicit Congestion Notification)
> 인터넷 내에서 수행되는 네트워크 지원 혼잡 제어의 한 형태<br>
> 라우터가 혼잡(정체)을 겪고 있으면 IP 데이터그램 헤더의 ECN 비트를 설정
### 명시적 혼잡 알림 에코(ECE, Explicit Congestion Notification Echo)
> IP헤더의 ECN 필드가 설정된 데이터를 수신 받으면 송신자에게 TCP ACK 보낼 때  ECE 비트를 설정하여 보냄
> 송신자는 ECE를 받으면 빠른 재전송을 사용하여 cwnd를 1/2로 변경하고 수신자 세그먼트 헤더에 CWR(Congestion Window Reduced)비트를 1로 설정
### 데이터그램 혼잡 제어 프로토콜(DCCP, Datagram Congestion Control Protocol)
> ECN을 활용하여 적은 오버헤드
> 혼잡제어가 되는 (UDP와 같은)신뢰할 수 없는 서비스를 제공
### 데이터 센터 정량화된 혼잡 알림(DCQCN, Data Center Quantized Congestion Notification)
### QUIC(빠른 UDP 인터넷 연결, Quick UDP Internet Connections)
- 애플리케이션 계층(layer 5) 프로토콜
- 혼잡 제어로 TCP 뉴리노 기반
- 연결지향적이고 안전함
  > (연결 지향) 연결 상태를 설정<br>
  > +<br>
  > (안전) 인증 및 암호화<br>
  > => 결합된 핸드셰이크 수행
- 스트림
  > 2개의 QUIC 종단 간 데이터를 순서대로 안정적으로 전달하기 위한 추상화<br>
  > 스트림 제어 전송 프로토콜(SCTP, Stream Control Transmission Protocol)
- 신뢰적이고 TCP 친화적인 혼잡 제어 데이터 전송
  > QUIC는 각 QUIOC스트림에 대해 독립적이고 신뢰적인 데이터 전송을 제공
# ch4
### 소프트웨어 정의 네트워크(SDN, Software-Defined Network)
> 제어 평면의 기능을 분리된 서비스처럼 사용하여 데이터 평면과 제어 평면을 뚜렷하게 구분
### 라우팅 알고리즘(Routing algorithm)
> 송신자가 수신자에게 패킷을 전송할 때 패킷 경로를 계산하는 알고리즘
### 포워딩(Forwarding)
> 단순 전달/이동 개념, 나노 초 단위로 수행, HardWare에서 실행
### 라우팅(Routing)
> 네트워크 전반에 걸쳐 데이터 그램의 경로를 결정
### 포워딩 테이블(Forwarding table)
> 라우터가 패킷에 대한 출력 링크 인터페애스를 결정하기 위한 요소
### 네트워크 서비스 모델(Network Service Model)
> 송/수신 호스트간 패킷 전송 특성을 정의한 것\
- 보장된 전달
  > 패킷이 출발지 호스트에서 목적지 호스트까지 도착하는 것을 보장
- 지연 제한 이내의 보장된 전달
  > 보장된 전달 + 특정 지연 제한 안에 전달
- 순서화 패킷 전달
  > 패킷이 송신된 순서대로 목적지에 도착하는 것을 보장
- 최소 대역폭 보장
  > 송신과 수신 호스트 사이에 특정한 비트율의 전송 링크를 에뮬레이트
- 보안 서비스
  > 출발지 호스트 암호화, 목적지 호스트 복호화<br>
  > = 기밀성 유지
### 최선형 서비스(best-effort service)
> 순서 보장X, 보장된 전달X, 지연 보장X<br>
> 그러나, 좋음
### 라우터(router, 패킷 스위치)
> 네트워크 계층(layer 3) 필드 값에 근거하여 포워딩을 결정하는 장치
- 입력 포트(input port)
- 스위치 구조
  > 라우터의 입력 포트와 출력 포트를 연결
- 출력 포트(output port)
  > 스위치 구조에서 수신한 패킷을 저장하고 필요한 링크 계층 및 물리 계층 기능을 수행하여 출력 링크로 패킷을 전송
- 라우링 프로세서
### 제어 평면(control plane)
> 소프트 웨어로 구현<br>
> 라우팅 프로세서에서 실행
### 목적지 기반 포워딩
### 일반화된 포워딩
### 프리픽스(prefix)
> 포워딩 테이블에서 라우터는 패킷 목적지 주소의 프리픽스 테이블 엔트리와 매치하여 매치되면 연관린 링크로 보냄