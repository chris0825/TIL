### 프로세서 별 명령어 비교

|TOY|ARM|x86|비고|
|:-|:-|:-|:-|
|ADD R0, R0, 7|-|addl $7, %eax||
|SUB R0, R0, R1|-|subl %ebx, #eax||
|CMP R0, 7|-|cmpl $7, %eax||
|AND R1, R1, R2|-|andl %ecx, #ebx||
|OR R1, R1, 7|-|orl $7, %ebx||
|COPY Rd, n|MOVS Rd, #n|movl $n, %Rd||
|NOT Rd,Rs|MVNS Rd, Rs|notl %eax||
|XOR Rd, Rs, Rs2|EORS Rd, Rs, Rs2|xorl %Rs, %Rd||
|LSL Rd, Rs, n|MOVS Rd, Rs, LSL #n|shll %eax||
|LSR Rd, Rs, n|MOVS Rd, Rs, LSR #n|shrl %eax||
|ASL Rd, Rs, n|MOVS Rd, Rs, ASL #n|sall %eax||
|ASR Rd, Rs, n|MOVS Rd, Rs, ASR #n|sarl %eax||
|LOAD Rd, addr|LDR Rd, addr|movl addr, %eax||
|LDR Rd, Ra, n|LDR Rd, [Ra, #n]|movl n(%ebx), %eax||
|STORE Rs, addr|STR Rs, addr|movl %eax, addr||
|STR Rs, Ra, n|STR Rs, [Ra, #n]|movl %eax, n(%ebx)||
|BR nzp, addr|B[cond] addr|jmp addr||
|BR z, addr|-|jep addr||
|BRR nzp, Ra, n|ADD[cond] PC, Ra, #n|jmp %eax||
|LEA Rd, addr|MOV Rd, addr|LEA addr, %eax||
|LINK<br>BR nzp, addr|BLAL addr|call addr||
|RET|MOV PC, R14|ret||
|SWI n|SWI #n|int $5||
|RTI|MOVS PC, R14|iret||
|SUB R5, R5, 1<br>STR Rs, R5, 0|STR Rs, [R13, #-4]!|pushl %eax||
|LDR Rd, R5, 0<br>ADD R5, R5, 1|LDR Rd, [R13], #4|popl %eax||
