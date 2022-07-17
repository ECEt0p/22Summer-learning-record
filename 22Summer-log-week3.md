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