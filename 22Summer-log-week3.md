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
