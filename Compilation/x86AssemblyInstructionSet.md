## 数据传输指令

### 通用数据传送指令

1. MOV     传送字或字节。
2. MOVSX   先符号扩展，再传送。
3. MOVZX   先零扩展，再传送。
4. PUSH    把字压入堆栈。
5. POP     把字弹出堆栈。
6. PUSHA   把AX、CX、DX、BX、SP、BP、SI、DI依次压入堆栈。
7. POPA    把DI、SI、BP、SP、BX、DX、CX、AX依次弹出堆栈。
8. PUSHAD  把EAX、ECX、EDX、EBX、ESP、EBP、ESI、EDI依次压入堆栈。
9. POPAD   把EDI、ESI、EBP、ESP、EBX、EDX、ECX、 EAX依次弹出堆栈。
10. BSWAP   交换32位寄存器里字节的顺序
11. XCHG    交换字或字节。(至少有一个操作数为寄存器，段寄存器不可作为操作数)
12. CMPXCHG 比较并交换操作数。(第二个操作数必须为累加器AL/AX/EAX)
13. XADD    先交换再累加。(结果在第一个操作数里)
14. XLAT    字节查表转换。----BX指向一张256字节的表的起点，AL为表的索引值(0-255,即0-FFH)；返回AL为查表结果。([BX+AL]->AL)

### 输入输出端口传送指令

1. IN      I/O端口输入。 ( 语法：IN   累加器，{端口号│DX} )
2. OUT     I/O端口输出。 ( 语法：OUT {端口号│DX}，累加器 ) 输入输出端口由立即方式指定时，其范围是 0-255;
                       由寄存器 DX 指定时，其范围是 0-65535.

### 目的地址传送指令

1. LEA     装入有效地址。例： `LEA DX,string ;把偏移地址存到DX`
2. LDS     传送目标指针，把指针内容装入DS。例：`LDS SI,string`把段地址：偏移地址存到DS:SI
3. LES     传送目标指针，把指针内容装入ES。例：`LES DI,string`把段地址：偏移地址存到ES:DI
4. LFS     传送目标指针，把指针内容装入FS。例：`LFS DI,string`把段地址：偏移地址存到FS:DI
5. LGS     传送目标指针，把指针内容装入GS。例：`LGS DI,string`把段地址：偏移地址存到GS:DI
6. LSS     传送目标指针，把指针内容装入SS。例：`LSS DI,string`把段地址：偏移地址存到SS:DI

### 标志传送指令

1. LAHF    标志寄存器传送，把标志装入AH
2. SAHF    标志寄存器传送，把AH内容装入标志寄存器
3. PUSHF   标志入栈
4. POPF    标志出栈
5. PUSHD   32位标志入栈
6. POPD    32位标志出栈

## 算术运算指令

1. ADD     加法
2. ADC     带进位加法
3. INC     加 1
4. AAA     加法的ASCII码调整
5. DAA     加法的十进制调整
6. SUB     减法
7. SBB     带借位减法
8. DEC     减 1
9. NEG     求反(以    0 减之)
10. CMP     比较。(两操作数作减法，仅修改标志位，不回送结果)
11. AAS     减法的ASCII码调整
12. DAS     减法的十进制调整
13. MUL     无符号乘法。结果回送AH和AL(字节运算)，或DX和AX(字运算)
14. IMUL    整数乘法。结果回送AH和AL(字节运算)，或DX和AX(字运算)
15. AAM     乘法的ASCII码调整
16. DIV     无符号除法。结果回送：商回送AL，余数回送AH， (字节运算)；或 商回送AX，余数回送DX(字运算)。
17. IDIV    整数除法。结果回送：商回送AL，余数回送AH，(字节运算)；或 商回送AX，余数回送DX, (字运算)
18. AAD     除法的ASCII码调整
19. CBW     字节转换为字 (把AL中字节的符号扩展到AH中去)
20. CWD     字转换为双字(把AX中的字的符号扩展到DX中去)
21. CWDE    字转换为双字(把AX中的字符号扩展到EAX中去)
22. CDQ     双字扩展(把EAX中的字的符号扩展到EDX中去)
23. DS:SI   源串段寄存器 ：源串变址
24. ES:DI   目标串段寄存器：目标串变址
25. CX      重复次数计数器
26. AL/AX   扫描值
27. D标志    0表示重复操作中SI和DI应自动增量；1表示应自动减量
28. Z标志    用来控制扫描或比较操作的结束

## 逻辑运算指令

1. AND     与运算
2. OR      或运算
3. XOR     异或运算
4. NOT     取反
5. TEST    测试。(两操作数作与运算，仅修改标志位，不回送结果)
6. SHL     逻辑左移
7. SAL     算术左移(=SHL)
8. SHR     逻辑右移
9. SAR     算术右移(=SHR)
10. ROL     循环左移
11. ROR     循环右移
12. RCL     通过进位的循环左移
13. RCR     通过进位的循环右移

    > **Tips:**以上八种移位指令，其移位次数可达255次
    >
    > 移位一次时， 可直接用操作码。 如 SHL AX,1
    >
    > 移位>1次时， 则由寄存器CL给出移位次数
    >
    > 如 MOV CL,04   SHL AX,CL

## 串指令

1. MOVS    串传送( MOVSB 传送字符。 MOVSW 传送字。 MOVSD 传送双字。 )
2. CMPS    串比较( CMPSB 比较字符。 CMPSW 比较字。 )
3. SCAS    串扫描。把AL或AX的内容与目标串作比较，比较结果反映在标志位
4. LODS    装入串。把源串中的元素(字或字节)逐一装入AL或AX中( LODSB 传送字符、 LODSW 传送字、LODSD 传送双字 )
5. STOS    保存串。是LODS的逆过程
6. REP         当CX/ECX<\>0时重复
7. REPE/REPZ   当ZF=1或比较结果相等，且CX/ECX<\>0时重复
8. REPNE/REPNZ 当ZF=0或比较结果不相等，且CX/ECX<\>0时重复
9. REPC        当CF=1且CX/ECX<\>0时重复
10. REPNC       当CF=0且CX/ECX<\>0时重复

## 程序转移指令

### 无条件转移指令(长转移)

1. JMP         无条件转移指令
2. CALL        过程调用
3. RET/RETF    过程返回

### 条件转移指令

短转移，-128到+127的距离内。当且仅当(SF XOR OF)=1时,OP1

1. JA/JNBE     不小于或不等于时转移。

2. JAE/JNB     大于或等于转移。

3. JB/JNAE     小于转移。

4. JBE/JNA     小于或等于转移。

    以上四条，测试无符号整数运算的结果(标志C和Z)。

5. JG/JNLE     大于转移。

6. JGE/JNL     大于或等于转移。

7. JL/JNGE     小于转移。

8. JLE/JNG     小于或等于转移。

    以上四条，测试带符号整数运算的结果(标志S,O和Z)。

9. JE/JZ       等于转移。

10. JNE/JNZ     不等于时转移。

11. JC          有进位时转移。

12. JNC         无进位时转移。

13. JNO         不溢出时转移。

14. JNP/JPO     奇偶性为奇数时转移。

15. JNS         符号位为 "0" 时转移。

16. JO          溢出转移。

17. JP/JPE      奇偶性为偶数时转移。

18. JS          符号位为 "1" 时转移

### 循环控制指令(短转移)

1. LOOP            CX不为零时循环
2. LOOPE/LOOPZ     CX不为零且标志Z=1时循环
3. LOOPNE/LOOPNZ   CX不为零且标志Z=0时循环
4. JCXZ            CX为零时转移
5. JECXZ           ECX为零时转移

### 中断指令

1. INT         中断指令
2. INTO        溢出中断
3. IRET        中断返回

### 处理器控制指令

1. HLT         处理器暂停,  直到出现中断或复位信号才继续
2. WAIT        当芯片引线TEST为高电平时使CPU进入等待状态
3. ESC         转换到外处理器
4. LOCK        封锁总线
5. NOP         空操作
6. STC         置进位标志位
7. CLC         清进位标志位
8. CMC         进位标志取反
9. STD         置方向标志位
10. CLD         清方向标志位
11. STI         置中断允许位
12. CLI         清中断允许位

## 伪指令

1. DW          定义字(2字节)
2. PROC        定义过程
3. ENDP        过程结束
4. SEGMENT     定义段
5. ASSUME      建立段寄存器寻址
6. ENDS        段结束
7. END         程序结束.

## 处理机控制指令

1. CLC     进位位置0指令
2. CMC     进位位求反指令
3. STC     进位位置为1指令
4. CLD     方向标志置1指令
5. STD     方向标志位置1指令
6. CLI     中断标志置0指令
7. STI     中断标志置1指令
8. NOP     无操作
9. HLT     停机
10. WAIT    等待
11. ESC     换码
12. LOCK    封锁

## 参考地址

知乎用户：[爱是等待是细水长流](https://zhuanlan.zhihu.com/p/53394807)

> **Tips：**还有浮点运算指令集
