### 동작 별 제어로직 신호
||상태|다음상태|IncPC|LdIR|LdDR|LdCCR|DataDR|DataALU|AddrPC|AddrALU|MemEn|MemWr|
|:-|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|명령어 읽기|111|110|0|1|0|0|0|0|1|0|1|0|
|명령어 해독|110|X|1|0|0|0|0|0|0|0|0|0|X|
|ALU 그룹 실행|000|111|0|0|1|1|0|1|0|0|0|X|
|LDR 그룹 실행|001|111|0|0|1|0|0|0|0|1|1|0|
|STR 그룹 실행|010|111|0|0|0|0|1|0|0|1|1|1|
|BRR 그룹 실행|011|111|0|0|1|0|0|1|0|0|0|X|

### 신호별 의미
- LdIR: 명령어 저장할거냐?
- LdDR: 레지스터에 저장할거냐?
- LdCCR: CCR레지스터 값 갱신?
- DataDR: 레지스터값 메모리에 저장할거야?
- DataALU: ALU회로 출력값 사용함?
- AddrPC: PC레지스터와 메모리 관계 있어?
- AddrALU: 메모리 주소지정해?
- MemEn: 메모리 접근해?
- MemWr: 1쓰기신호/0읽기신호
- IncPC: PC레지스터 값 +1

### Reg.File에서 디코더를 사용하는 이유
: IR에서 명령어를 읽을 때 레지스터를 의미하는 신호(DR, SR, SR2)가 3비트의 입력으로 주어지는데 이 비트 신호들의 조합으로 특정 레지스터가 결정하기 위해서 디코더를 사용한다.
