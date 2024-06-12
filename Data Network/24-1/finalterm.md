### GBN ( Go-Back-N, N부터 반복) 프로토콜
### = 슬라이딩 윈도 프로토콜(Sliding-window protocol)
> 확인 응답을 기다리지 않고 여러 패킷을 전송
### 윈도 크기
> 아직 확인응답(ACK)이 오지 않은 패킷을 허용할 수 있는 순서 번호 범위
### 확장된 FSM(extended FSM)
> ?
### 누적 확인 응답(Cumulative acknowledgment)
> GBN 프로토콜에서 순서번호 n을 가진 패킷에 대한 확인 응답<br>
> 모든 것에 확인 응답을 받는 것이 아니라 정상 수신한 마지막 패킷 번호만 회신
