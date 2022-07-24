# 2022/7/17  
今天做完了Lab02，无他。 
```
        .ORIG x3000
        AND R1,R1,#0    ;STORE THE VALUE IN DEC
        
INPUT   TRAP x20
        LD  R3,ASCII
        ADD R0,R0,R3    ;R0<-n
        BRn CONPUT      ;CHECK ENTER
        JSR TIMES10     ;R1<-R1*10
        ADD R1,R1,R0    ;R1<-N
        BRnzp INPUT
        
CONPUT  AND R4,R4,#0
        ADD R4,R4,#-4
LP      BRz FINAL
        JSR OUTPUT
        ADD R4,R4,#1
        BRnzp LP
        
FINAL   TRAP X25

TIMES10 AND R3,R3,#0
        ADD R1,R1,R1    ;R1<-R1*2
        ADD R3,R3,R1    ;R3<-R1*2
        ADD R1,R1,R1    ;R1<-R1*4
        ADD R1,R1,R1    ;R1<-R1*8
        ADD R1,R1,R3    ;R1<-R1*10
        RET
        
OUTPUT  AND R2,R2,#0
        AND R3,R3,#0
        ADD R3,R3,#-4
LOOP    BRz BACK
        ADD R2,R2,R2
        ADD R1,R1,#0
        BRzp NEXT
        ADD R2,R2,#1
NEXT    ADD R1,R1,R1
        ADD R3,R3,#1
        BRnzp LOOP
BACK    ADD R2,R2,#-9
        BRp CHPUT
        LD  R3,ASCII0
        ADD R0,R2,R3
        TRAP x21
        RET
CHPUT   LD R3,CH
        ADD R0,R2,R3
        TRAP x21
        RET

ASCII   .FILL xFFD0     ;-48,TO CONVERT ASCII
ASCII0  .FILL x0039     ;57
CH      .FILL x0040     ;64
        .END
```  
***
# 2022/7/18  
今天的时间在休息，以后不通宵了，做了ICS的作业，验收通过了Lab2，无他。
*** 
# 2022/7/19
## ICS  
做完了Lab3，精疲力尽，简单问题复杂化了，很蠢。
```
        .ORIG x3000
        LD  R1,BASEL    ;PTR LEFT
        LD  R2,BASEL
        ADD R2,R2,#1    ;PTR RIGHT
        LD  R4,RES
        
INPUT   TRAP    x20
        TRAP    x21
        LD  R3,ENTER
        ADD R3,R3,R0
        BRz OUTPUT
        LD  R3,PLUS
        ADD R0,R0,R3
        BRzp F1
        JSR PUSHL
        BRnzp   INPUT
F1      BRp F2
        JSR POPL
        BRnzp   INPUT
F2      ADD R0,R0,R3
        ADD R0,R0,#-1
        BRp F3
        JSR PUSHR
        BRnzp   INPUT
F3      JSR POPR
        BRnzp   INPUT
OUTPUT  NOT R3,R4
        ADD R3,R3,#2
        LD  R4,RES
FINAL   ADD R0,R3,R4
        BRp FIN
        LDR R0,R4,#0
        TRAP    x21
        ADD R4,R4,#1
        BRnzp   FINAL
        
FIN     TRAP    x25

PUSHL   TRAP    x20
        TRAP    x21
        STR R0,R1,#0
        ADD R1,R1,#-1
        RET

PUSHR   TRAP    x20
        TRAP    x21
        STR R0,R2,#0
        ADD R2,R2,#1
        RET

POPL    NOT R3,R1
        ADD R3,R3,R2
        BRp F4
        LD  R0,US
        STR R0,R4,#0
        ADD R4,R4,#1
        RET
F4      ADD R1,R1,#1
        LDR R0,R1,#0
        STR R0,R4,#0
        ADD R4,R4,#1
        RET
        
POPR    NOT R3,R1
        ADD R3,R3,R2
        BRp F5
        LD  R0,US
        STR R0,R4,#0
        ADD R4,R4,#1
        RET
F5      ADD R2,R2,#-1
        LDR R0,R2,#0
        STR R0,R4,#0
        ADD R4,R4,#1
        RET
        
PLUS    .FILL #-45
BASEL   .FILL x3200
US      .FILL #95
RES     .FILL x3400
ENTER   .FILL #-10
        .END
```
***
# 2022/7/20-2022/7/23
## ICS
只是写完了Lab4，其他时间都烂。
```
;PREPARE
        .ORIG   x0200
        LD  R6,OS_SP
        LD  R0,USER_PSR
        ADD R6,R6,#-1
        STR R0,R6,#0
        LD  R0,USER_PC
        ADD R6,R6,#-1
        STR R0,R6,#0
        
        LD  R0,CODE_ADD
        STI R0,ENTRY
        LD  R0,MASK
        STI R0,KBSR_ADD
        
        RTI
            
CODE_ADD    .FILL   x2000
ENTRY       .FILL   x0180
MASK        .FILL   x4000        
KBSR_ADD    .FILL   xFE00 

OS_SP       .FILL   x3000
USER_PSR    .FILL   x8002
USER_PC     .FILL   X3000
        
        .END

;TRAP ORDER
        .ORIG   x2000
        
LOOP1   LDI R2,KBSR
        BRzp    LOOP1
        LDI R0,KBDR
        
        ADD R3,R3,#0
        BRz T0
        ADD R3,R3,#-1
        LD  R4,DOT_n
        ADD R4,R4,R0
        BRz EXIT
        STI R0,ADDR0
        AND R1,R1,#0
        ADD R1,R1,R3
EXIT    RTI
                        ;THE FIRST 20 LETTERS
T0      LD  R4,DIV
        ADD R4,R4,R0
        BRnz    NUM
        
        STI R0,ADDR0
        RTI
        
NUM     ADD R4,R4,#9
        NOT R4,R4
        ADD R1,R1,R4
        LD  R4,LIM
        ADD R4,R4,R1
        BRp    BACK 
        LD  R1,LIM_n
BACK    RTI                        
       
        STI R0,ADDR0
        RTI

LIM     .FILL   #18
LIM_n   .FILL   #-18
DIV     .FILL   #-57   
DOT_n   .FILL   #-46
KBSR	.FILL	xFE00
KBDR	.FILL	xFE02
ADDR0   .FILL   x3200   
        .END


;USER PROGRAM
        .ORIG   x3000
        LD  R3,LEN
        
CHECK   ADD R3,R3,#0
        BRp CHECK
        
        ADD R1,R1,#-15
        ADD R1,R1,#-2
        
LOOP    ADD R1,R1,#1
        BRnz    F0
        AND R1,R1,#0
F0      AND R2,R2,#0
        ADD R2,R2,R1
F1      BRz     F2
        LD  R0,DOT
        OUT
        ADD R2,R2,#1
        BRnzp   F1
        
F2      LDI R0,ADDR
        OUT
        OUT
        OUT

        AND R2,R2,#0
        ADD R2,R2,R1
        ADD R2,R2,#15
        ADD R2,R2,#2
F3      BRz NEXT
        LD  R0,DOT
        OUT
        ADD R2,R2,#-1
        BRnzp   F3

NEXT    LD  R0,ENTER
        OUT
        JSR DELAY
        BRnzp   LOOP
        
DELAY   LD R2,COUNT
REP     ADD R2,R2,#-1
        BRp REP
        RET


LEN     .FILL   #20
ADDR    .FILL   x3200
DOT     .FILL   #46        
ENTER   .FILL   #10
COUNT   .FILL   #30000
        
        .END
```
***
无他
