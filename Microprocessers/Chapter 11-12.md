### 프로세서 별 명령어 비교

|TOY|ARM|x86|비고|
|:-|:-|:-|:-|
|ADD R0, R0, 7|-|addl $7, %eax|EAX <- EAX + 7|
|SUB R0, R0, R1|-|subl %ebx, %eax|EAX <- EAX - EBX|
|CMP R0, 7|-|cmpl $7, %eax|EAX - 7|
|AND R1, R1, R2|-|andl %ecx, %ebx|EBX <- EBX and ECX|
|OR R1, R1, 7|-|orl $7, %ebx|EBX <- EBX or 7|
|COPY Rd, n|MOVS Rd, #n|movl $n, %Rd|EAX <- n|
|NOT Rd,Rs|MVNS Rd, Rs|notl %eax|ARM: <br>x86: EAX <- not EAX|
|XOR Rd, Rs, Rs2|EORS Rd, Rs, Rs2|xorl %ebx, %eax|x86: EAX <- EAX xor EBX|
|LSL Rd, Rs, n|MOVS Rd, Rs, LSL #n|shll %eax||
|LSR Rd, Rs, n|MOVS Rd, Rs, LSR #n|shrl %eax||
|ASL Rd, Rs, n|MOVS Rd, Rs, ASL #n|sall %eax|ARM: MOV에 시프트 연산<br>x86: EAX <- EAX << 1|
|ASR Rd, Rs, n|MOVS Rd, Rs, ASR #n|sarl %eax|ARM: MOV에 시프트 연산<br>x86: EAX <- EAX >> 1|
|LOAD Rd, addr|LDR Rd, addr|movl addr, %eax|ARM: MOV에 시프트 연산<br>x86: EAX <- M[addr]|
|LDR Rd, Ra, n|LDR Rd, [Ra, #n]|movl n(%ebx), %eax|ARM: MOV에 시프트 연산<br>x86: EAX <- M[EBX+n]|
|STORE Rs, addr|STR Rs, addr|movl %eax, addr|x86: M[addr] <- EAX|
|STR Rs, Ra, n|STR Rs, [Ra, #n]|movl %eax, n(%ebx)|x86: M[EBX+n] <- EAX|
|BR nzp, addr|B[cond] addr|jmp addr|ARM: cond는 EQ, PL,,,|
|BR z, addr|-|jep addr||
|BRR nzp, Ra, n|ADD[cond] PC, Ra, #n|jmp %eax|ARM: cond는 EQ, PL,,,|
|LEA Rd, addr|MOV Rd, addr|LEA addr, %eax||
|LINK<br>BR nzp, addr|BLAL addr|call addr|함수 호출|
|RET|MOV PC, R14|ret|함수에서 복귀|
|SWI n|SWI #n|int $n|운영체제 n번째 기능 호출|
|RTI|MOVS PC, R14|iret|운영체제에서 복귀|
|SUB R5, R5, 1<br>STR Rs, R5, 0|STR Rs, [R13, #-4]!|pushl %eax|스택PUSH|
|LDR Rd, R5, 0<br>ADD R5, R5, 1|LDR Rd, [R13], #4|popl %eax|스택POP|

### 프로세서 별 특징
||TOY|ARM|x86|
|:-|:-|:-|:-|
|레지스터 집합|- 8개 32비트 레지스터 + CCR 레지스터|16개 32비트 레지스터 + CPSR|8개 32비트 범용 레지스터 + EFLAGS|
|기계어 코드 구조<br>(32비트 기준)|-|모든 명령어 32비트로 고정|명령어별 크기 1~15바이트로 다양|
|운영체제 기능 호출과<br>복귀 관련 명령어|호출: SWI n<br>복귀: RTI|호출: SWI #n<br>복귀: MOVS PC, R14|호출: int $n<br>복귀: iret|
|메모리 접근(읽기/쓰기)<br>관련 명령어들||LOAD/STORE 명령어<br>B/W/L비트를 통해 처리 단위 선택 가능|mov명령어 외에도 다양한 명령어로 접근 가능<br>ALU관련 명령어도 메모리 주소 사용 가능|
|기타<br>명령어 구성 특징||- 모든 명령어가 조건부 실행이 가능<br>- CPSR레지스터 갱신 여부를 명령어에 's'를 붙임으로써 제어 가능<br>- 오퍼랜드에 '#'를 붙이면 즉석값, 안붙이면 주소를 의미<br>- 모든 명령어 32비트로 고정|- 명령어 끝에 'l'을 붙이면 32비트 단위로 처리<br>- 오퍼랜드에 '%'를 붙이면 레지스터 이름, 안붙이면 레이블 이름<br>- 오퍼랜드 앞에 '$'를 붙으면 즉석값, 안붙이면 주소값<br>- 산술/논리 연산시 소스 오퍼랜드, 목적지 오퍼랜드 각 1개씩|
