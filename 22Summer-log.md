# **2022/6/30**
今天是信电短学期线下课程的最后一天，花费了大概四个小时去预习了《计算机系统概论》的Chapter1、2。  
开始尝试使用Markdown的语法来完成这个学习日志的记录，本来是想在98开个一路帖的，但是感觉在Github上显得更加高大上一点。：）  
接下来的每天我都会花一点时间将所学写个小总结放到这个仓库中，也算是对于自己的一种激励吧。  
  
***  
## **计算机系统概论**   

没有花时间去读Preface，本来看到英文就头疼。  

***Chapter1***  
主要就是介绍了一些观念上的东西，比如计算机其实是一套软硬结合的完备系统，稍微介绍了一下计算机的思想，黑盒模型之类的。  
整一章最为重要的便是这个七层的模型： 

**Problems  
Algorithms  
Language  
ISA(instruction set architecture)  
Microarchitecture  
Circuits  
Device**  

这个模型自上而下，解释了我们如何层层递进去解决一个问题——利用计算机。  

***Chapter2***  
这章的内容相对比第一张明显变多了，不过仍然有很多概念是已经学过的，大部分都是大计基的内容，关于一些数据类型以及运算。  

**Integer Data Type**  
分为 unsigned integers以及signed integers，具体的差别就在于最前的一位用于表示数还是用于表示符号。  
两种类型的不同，从而引申出 1's complement （1补数（反码）） 以及 2's complement （2补数（补码））。  
二进制数和十进制数之间的转换，以及二进制数之间的算术加法，值得一提的是，在ALU中负数的存储方式是以2补数的形式存在（其实正数也是），利用2补数相加可以更方便地完成数的加减法。  
逻辑运算，依旧是 AND OR NOT XOR 这几个家常便饭的运算，然后又提到了 DeMorgan's Laws。这一部分新学到的是关于 Bit Vector（位向量）的内容，我们可以对原始数据和位向量的逻辑运算来完成对数据的处理（详见书上的例题）。  
  
**Floating Point Data Type**  
表示方式便是浮点数的表示方式，具体体现在1（S）+8（exponent）+23（fraction）=32bit。具体的浮点数的计算机表示和实数的转换需要掌握。  
浮点数的表示有特殊情况，当 exponent 为 11111111 时，根据 S 的情况具体为正无穷大和负无穷大。  
当 exponent 为 00000000 时，这时用于表示较小的 Subnormal numbers。计算公式详见书本。  
  
**ASCII Code**  
一种编码，后续会学在 LC-3 上的应用。  
  
**十六进制**  
大同小异的内容，和二进制几乎没有什么差别。  
  
***    

明天希望能完成vscode上c编程环境的配置，然后明天花时间看一点计概的书本内容（Chapter3），然后完成短学期的调研报告，再做几个C加强的lab，完善一下Github的主页。

***  
# **2022/7/1**  
今天没有太多的时间让我去自学 ICS 了，简单讲讲今天干了什么吧。    

早上跟着 vscode 的官方文件配置了一下vscode的c/c++环境，但是现在还是有几个问题没有解决：  
1、c的程序可以运行但是c++的程序无法运行  
2、output始终没有输出结果，全部的输出和输入现在都是在terminal上进行，但我还是不知道两者具体有什么区别  
  
下午花了些时间去完成短学期的实践课报告，纯浪费时间，希望以后这种作业可以少一点。晚上总算是搞定了C加强的作业，也是浪费时间，整个课程设计得像一坨shit，不想在吐槽，这个时间花完了就好了，啥也没学到。  
  
明天的话，上午希望能花时间解决今天在vscode上出现的问题，下午可以多学一点ICS，明天能把Chapter3和Chapter4都解决是最好的，这样后天就能进入LC-3的学习啦。  
其他好像就没什么一定要做的事情了，关于c语言的进阶学习，到时候放在CS61A和大学物理等课程之后吧，这些都可以慢慢来，暑假还长，短期内还是要把ICS的书看掉，然后学习一下各类工具的使用方式，初步熟悉一下Python的语法。
   
***Chapter3***  
这一章的内容是讲*Digital logical structure*  

### 3.1  
内容讲了三极管，以MOS管和CMOS管为介绍对象，然后讲述了一下P型和N型在不同电压下的通断情况  具体表现为  
|三极管类型|0|1|
|---|---|---|
|P|1|0|
|N|0|1|
  
### 3.2  
讲述了如何用P型和N型的三极管去构建之前学到的各种逻辑门，要注意搭建时的规范性，不然会导致低电压过高、高电压过低的情况。  

### 3.3  
Combintional Logical Circuit 是用逻辑门实现的具体应用：  
**Decoder**,可以通过输出判断输入的内容，也可以由输入在指定的输出输出1；**Mux**，通过控制S的输入内容使得n个input的值中的一个可以作为output；adder（全加器），没什么好讲的，之前信电导做过更复杂的；**PLA**，我的理解是一种逻辑电路的设计范式，这里先想到如何通过真值表来完成逻辑表达式的书写，就能很清楚地理解PLA的设计意图———PLA有a个输入，娜美就有$2^a$个a输入与门，有b个输出，就有b个或门，或门同与门的连接方式取决于输出的真值表。  
Logical Completeness：指的是用单一逻辑门构建整个逻辑电路的能力，NAND、NOR都具有这一特性。　　

### 3.4　
Basic Storage Element　两个存储数据的电路:    
**The R-S Latch** ,就是R-S锁存器。S、R都为1时，为静止状态，储存值；S1 R0时，置0；S0 R1时，置1；S、R皆为0的状态暂时不考虑，为随机状态。  
**The Gate D Latch**，在原有锁存器的基础上添加一个D门(?)，增加了一个D输入和一个WE(write enable)输入来控制对锁存器的读写。WE为0时为静止状态，WE为1时，可改变锁存器的内容，a的值与D相同。  

### 3.5  
讲述了关于Memory的概念：  
首先是两个概念，地址空间和可寻址能力，两者就像是列表的横行与竖列(?)。  
然后就是一个$2^2$-by-3-bit Memory的模型，这个模型具有2bit的地址空间，每个地址上有3bit的存储内容，当我们想要读取其中的内容时,首先通过A[1:0]来输入地址，Decoder就会根据输入在指定位置输出1，再利用Mux完成对锁存器中数据的输出。(具体的过程可以看书上的图来理解)  
还有几个零碎的概念：每个地址上所存储的3bit数据被称为*word line*；[high:low]表示有 high-low+1 bit的数据。  

### 3.6  
Sequential Logic Circuit  时序逻辑电路  
时序逻辑电路的输出结果时受先前状态影响的，因此时序逻辑电路会多出一个用于存储状态的Storage element。  
状态：a snapshot of all the elements of teh system at the moment the snapshot is taken.(不是很好去翻译)  
**Finite State Machine**  这种机器有五个特点：  
1、状态有限。  
2、有限外部输入。  
3、有限外部输出。  
4、状态间的转化有着明晰的规则。  
5、明确由什么决定输出。  
**Synchronous Finite State Machine** 这种状态机的内部有Clock Circuit，Clock会在固定的间隔时间内完成自身的值由0变1、由1变0的过程，借助Clock的这一特性，有限同步状态机就能完成在每个clock cycle开始的时刻完成状态的转化。  
之后书本给出了一个例子，在例子中出现了 A master/slave flip-flop 简而言之就是两个Latch轮流可写来完成对状态的储存和输出，书本给出了时序图，便于理解。  

***Chapter4***  
这一章讲述*The Von Neumann Model*  
冯·诺伊曼架构的计算机由以下5个部分组成：  
1.Memory  当我们从Memory中读取内容时，我们先会把地址放到MAR(memory's address register)中，然后地址上的内容就会被放入MDR(memory's data register)中，再完成输出。  
2.Processing Unit  最简单的处理单元就是ALU(Arithemetic and Logic Unit)，他能够完成基本的算数和逻辑运算。  
word length 是PU一次能够处理的数据的长度。  
因为在PU和Memory之间经常有数据的交换，所以在两者之间设计一个register可以大大加快运行的效率。  
3.Input/Output  
4.Control Unit  CU保持追踪每一个程序和指令的运行过程，用于指向被执行的指令(保存正在被执行的指令)的被称为IR(instruction register)(also be called program counter(PC))。  

接下来简单介绍了LC-3中哪些部分对应VNM中的哪个部分。  
  
***
上午就这么过去了，昨天确实看了很多内容，今天也要加油！
