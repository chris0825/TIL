### 프로세서 별 명령어 비교

|TOY|ARM|x86|비고|
|:-|:-|:-|:-|
|ADD R0, R0, 7|-|addl $7, %eax|EAX <- EAX + 7|
|SUB R0, R0, R1|-|subl %ebx, #eax|EAX <- EAX - EBX|
|CMP R0, 7|-|cmpl $7, %eax|EAX - 7|
|AND R1, R1, R2|-|andl %ecx, #ebx|EBX <- EBX and ECX|
|OR R1, R1, 7|-|orl $7, %ebx|EBX <- EBX or 7|
|COPY Rd, n|MOVS Rd, #n|movl $n, %Rd|EAX <- n|
|NOT Rd,Rs|MVNS Rd, Rs|notl %eax|ARM: <br>x86: EAX <- not EAX|
|XOR Rd, Rs, Rs2|EORS Rd, Rs, Rs2|xorl %ebx, %eax|ARM: <br>x86: EAX <- EAX xor EBX|
|LSL Rd, Rs, n|MOVS Rd, Rs, LSL #n|shll %eax||
|LSR Rd, Rs, n|MOVS Rd, Rs, LSR #n|shrl %eax||
|ASL Rd, Rs, n|MOVS Rd, Rs, ASL #n|sall %eax|ARM: <br>x86: EAX <- EAX << 1|
|ASR Rd, Rs, n|MOVS Rd, Rs, ASR #n|sarl %eax|ARM: <br>x86: EAX <- EAX >> 1|
|LOAD Rd, addr|LDR Rd, addr|movl addr, %eax|ARM: <br>x86: EAX <- M[addr]|
|LDR Rd, Ra, n|LDR Rd, [Ra, #n]|movl n(%ebx), %eax|ARM: <br>x86: EAX <- M[EBX+n]|
|STORE Rs, addr|STR Rs, addr|movl %eax, addr|ARM: <br>x86: M[addr] <- EAX|
|STR Rs, Ra, n|STR Rs, [Ra, #n]|movl %eax, n(%ebx)|ARM: <br>x86: M[EBX+n] <- EAX|
|BR nzp, addr|B[cond] addr|jmp addr||
|BR z, addr|-|jep addr||
|BRR nzp, Ra, n|ADD[cond] PC, Ra, #n|jmp %eax||
|LEA Rd, addr|MOV Rd, addr|LEA addr, %eax||
|LINK<br>BR nzp, addr|BLAL addr|call addr|함수 호출|
|RET|MOV PC, R14|ret|함수에서 복귀|
|SWI n|SWI #n|int $n|운영체제 n번째 기능 호출|
|RTI|MOVS PC, R14|iret|운영체제에서 복귀|
|SUB R5, R5, 1<br>STR Rs, R5, 0|STR Rs, [R13, #-4]!|pushl %eax|스택PUSH|
|LDR Rd, R5, 0<br>ADD R5, R5, 1|LDR Rd, [R13], #4|popl %eax|스택POP|
