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
***
# **2022/7/3**  
今天下午花了时间看完了Chapter4的剩余部分，晚上整理了寝室，花了很多时间，说到底还是懒。 
***  
## **计算机系统概论**   

关于LC-3的指令，首先明晰两个概念：opcode(操作码)和operand(操作数)  
指令分为三种基础类型：**Operate**,**Data Movement**,**Control**。每一条LC-3的指令由16bit组成，其中[15:12]用于表明是哪条指令，但是只有15个被利用，1个用作未来的用途。  
ADD(0001)：当bit 5==0时，[2:0]作为register的编号；当bit 5==1时，[5:0]作为一个immediate value。  
AND(0101)：bit 5==1，[5:0]作为一个immediate value。[5:0]全为0时，可用于初始化register中的值。  
LD(0010):[8:0]中的值扩充到16bit然后加到程序计数器中。(有一个关于*addressing mode*的概念，这种运用LD的方式叫做PC+offset(?))  
  
***The Instruction Cycle (指令周期)***  
指令周期有6个阶段，但并不是每个阶段都是必需的。  
**Fetch**  一个相对比较复杂但是有范式的过程：PC->MAR,PC++;Memory->MDR;MDR->IR  
**Decode**  对指令解码，确定哪个指令（如ADD）被执行  
**Evaluate Address**  如LD指令中对地址的计算操作
**Fetch Oprands**  如LD指令中从MAR中取地址，再将地址对应的数据存放到MDR中的操作  
**Execute**  在ALU中完成算术或者逻辑运算  
**Store Result**  将执行结果写入到指定的位置，这一阶段不一定单独存在（如在ADD中就在Execute阶段被执行）  
[LC-3中，ADD没有3、6，LD没有5]  

BR（0000）：一个判断的作用(conditonal branch)，若上一条指令的结果符合[11:9]，无事发生，若不符合，下一条执行的指令将由[8:0]决定。  

为停止不断执行的指令，我们需要停止CLOCK，一般来说每个时钟都有一个Q latch来控制，执行HALT instruction可以向Q Latch发出一个0信号以完成对时钟的控制（这个指令被称为TRAP指令，opcode=1111）  

最后书本展示了一个例子，用累次加法实现乘法，从中注意一个点便是PC++的时间节点，这对于BR语句的控制非常重要。  
***  
今天剩下的时间去完善一下README吧，最近想写的课程总结也可以开个小头了。  
***  
# 2022/7/4  
今天下午看完了ICS的Chapter5，晚上看完了Chapter6，现在看的速度越来越快了，开始适应英语文本的阅读，但是也要注意质量。  
***  
## **计算机系统概论**  

***Chapter5***  
这一章名为LC-3，实际上的内容更注重LC-3的ISA。一开头说了ISA specifiles ：  
* Memory Organization：就是类似之前提到的$2^2$-by-3-bit Memory，只不过在LC-3内部有的是一个$2^16$-by-16-bit Memory。
* Registers：LC-3中有八个general purpose register (GPR)。  
* The Instruction Set：Instruction 由 opcode和operand组成。在LC-3中就是15+1个指令。
* Opcodes：每个ISA又有一定数量的Opcode。
* Data Types：数据保存的不同形式。  
* Addressing Mode：寻址模式，后续会讲到，在LC-3中运用三种。  
* Condition Code：3个1bit寄存器(N,Z,P)用于存放0，1——每次GPR写入或者加载或者操作时。  

然后开始介绍各类的Operate Instructions,Data Movement Instructions,Control Instructions。  

在这个过程中学到了三种Addressing Mode：
* PC-relative Mode：指令中的[8:0]与PC相加取得的地址。  
* Indirect Mode：指令中[8:0]与PC相加取得的地址中存放着地址。 
* Base+offset Mode：指令中[5:0]与指令中[8:6]寄存器中的值相加获得地址。  
这些操作分别对应的Data Movement Instruction：LD,ST  LDI,STI  LDR,STR  
  
学到了两种控制循环的方法：  
* Counter：设置一个计数器。
* Sentinel：设置一个卫兵值（这里好像不是变量）  

看了一个关于用累加实现乘法的例子。  

然后又回到那张LC-3的Data Path图，明确了各条指令在机器中是如何运作之后，这张图中的一部分连接关系就显得比较明朗了——虽然还是记不住：（  
* The Global Bus:这个应该就是负责数据传递的总线，Bus中，Data Path是可以转变的。
* Memory：还是老样子，和MDR、MAR在一起运作。
* ALU & Register File：RF的两个数据输出是直接或者间接连接到ALU上的，其中SR2OUT还要经过一个MUX。  
* PC & PCMUX：微妙的连接关系，PCMUX的三个输入分别是：自增的PC、控制指令、未知，通过MUX来决定PC的下一个值究竟是什么。  
* MARMUX：控制给到MAR的地址。  

以LDR指令为例分析了指令周期的几个过程。 

***Chapter6***  
虽然是以Programming为题目，但是就是两大块内容：
1、结构化的编程风格  
2、Debug的范式  

首先看到了如何用LC-3的指令实现*Sequential,Conditional,Iterative*这三个结构，然后就是看了之前那个例子如何从自然语言一步步分解成一个可编程的问题。  
Debug相关，有几个基本方法：
* Set Value
* Execute Sequences：可以单步执行，也可以通过Set Breakpoint实现。  
* Display Values  
然后讲了四个例子，来表明在debug过程中会遇到的问题，和相应要去解决的方法。值得注意和总结的有：  
* 语句本身有没有错误  
* BR语句判断值取决于前一条语句产生的condition codes。
* 在debug过程中要注意用Corner Case，以此为依据完成Set Value。
***  
总体来说今天的内容是比较多的，现在看书的速度加快了，希望自己能按照上课的节奏完成预习，现在就是希望自己能够在8点左右起床，想去吃个早饭什么的，每天学习的时间还是不够多，没有空闲去熟悉VScode之类的工具的操作了，像是在虚拟机上运用Linux之类的估计要等这段时间过去吧。  
现在我努力将这份recording写的简单一点，主要是讲究我究竟学了什么，而不是学的具体内容，主要还是一个简单的归纳总结。  
***
# 2022/7/5  
今天就是学习了一下计概，其他啥都没干，烦。  
***  
## **计算机系统概论**  
***Chapter7***  
这一章的内容是关于*Assembly Language*。其实就是讲了之前的机器语言转化为汇编语言的结构要怎么写。  

一条Instruction由1+2+1组成:  
* Opcodes & Operands:这两个部分是必需的！  
* Labels：包含1到20长度的含大小写字母和数字，以字母开头。注意不能使用*保留字*。  
* Comments：注释。  
  
还有一些是Pseudo-Ops(Assembler Directives)，这种指令在编译的过程中帮助Assember，在执行过程中“消失”。目前学了这几种：
* .ORIG:指明在Memory中放置程序的位置。
* .FILL:预留出空间来初始化值。  
* .BLKW:预留出一系列的空间（？）
* .STRINGZ:预留出n+1的空间用于存放字符串的ASCII码（16），最后一位存放0('\0')表示结束。  
* .END:告诉编译器这里是程序的末尾。  

在编译的过程中，是Two-Pass Process：
The First-Pass：Creating the Symbol Table.  
The Second-Pass：Generating the machine language program.  

最后的这个小节的内容，不是很懂。大概的意思是，每一个执行的程序都被称为executable image，而这个image往往是由很多个object file转变而来的。这就导致了在编译过程中创建的Symbol Table可能存在问题（一个object file中的symbol可能在另一个中被解释）。  
这就导致了.EXTERNAL的使用，保证Symbol不出错，从而实现多个object file的*link*(具体的内容，其实Figure8.6解释得很清晰)。  

***Chapter8***  
这章得内容是Data Structures（Abstract Data Type）。  

在具体讲述数据结构之前，首先介绍了*subroutine(function)*的概念。讲述了Call/Return Mechanism,就是利用call指令和return指令完成对一个代码模块的调用。  
* JSR(R):调用subroutine的指令，JSR采用PC-relative寻址模式，JSRR采用BaseR寻址模式（提供更广的寻址范围）。  
* JMP：可用于返回某个语句(?)。  

在调用之前，由于可能用到某些寄存器，通常会把这些寄存器中的数据先保存到Memory中，防止数据的丢失，在执行完成后再把这些值重新保存到寄存器中。  

库函数，在一个库中（比如Math库）有一些可供调用的函数。这边的内容就是Chapter7末尾的一个形象例子，便于理解。  

**Stack（栈）**  
学习了栈的概念，知道了push和pop的操作，了解了underflow和overflow，知道了如何用汇编语言实现带检测的push和pop操作。  
要注意的是：存在一个指针，始终指向Top（栈顶）；已经在栈中的Value是不会移动地址的的（因为pop等操作是通过这个指针完成的）。  
***  
今天学的比较懒散，明天加油，希望能能早起。最近想找个实验室，最好能有人带着我，让我知道能学些什么，来发表论文，胆大当爸爸。  
其实有在想，每天浪费的时间有点多，早上可以研究一下整个网课的上课方式。  
***
# 2022/7/6  
今天除了看完计概的内容以外，还开始上CS61A的课程了。  
***  
## **计算机系统概论**  
***Chapter8***  
学完了剩下的数据结构。
* **Recursion**：主要从求阶乘和求斐波那契数列的第N项两个例子讲述了如何递归的概念，在用LC-3汇编语言实现递归的过程中要注意Stack的应用，不然就会丢失已有的数据和返回的位置。  
最主要的例子还是Maze，在Maze的code中，了解到了掩码的应用和对最高位的操作以实现一个比较的功能。  
* **Queue**：和Stack有类似之处，但是区别在于有FRONT和REAR两个指针来确定队尾和队首，值得注意的是：FRONT指向第一个数据前一个地址，REAR指向最后一个数据的地址；Queue有着环形的结构，一个queue最多可以储存n-1个数据，当FRONT和REAR相同时，这个queue is empty；Queue同样也存在Underflow和Overflow，分别在queue empty和full的情况下出现；对queue的操作被称为*remove*和*insert*。  
* **Character Strings**：就是字符串，看了两个例子：字符串储存员工信息；字符串表示整数。 

***Chapter16***  
这章是根据上课的大纲，被我提前拿来预习的。主要就是讲Pointer & Array。  
* Pointers:讲了指针的概念；两个运算符&和*；空指针;最后通过一个例子（Language C）表明指针的运用。  
* Array：数组的概念；数组用汇编语言的操作；数组作为函数传递的值；字符串数组；数组与指针的关系；数组的应用，主要是学了一个Insertion Sort的算法；Array in Language C的越界会导致的BUG；变长度数组；多维数组。  
***   
## **CS61A**  
听完了Lecture1的内容，就是介绍一下课程，稍微展示了一下Python的应用，一些关于Expression的内容。  
***  
从总结来看，今天学的内容不是很多，主要大多是一些已经学过的内容，所以看起来比较轻松。  
现在开始看一点CS61A的内容，感觉还是不错的（因为单学ICS其实有点小浪费时间，而且无聊）。不过CS61A的Lab之类的东西确实还是要找时间做的，早上的时间就不要这么浪费了吧。  
请不要焦虑。  
***
# 2022/7/7  
今天早上终于花时间配置完了Vscode中的C/C++和Python编程环境，总算是完成一件拖拖拉拉的事情。学了计概，但是没有时间做CS61A的Lab0了。  
## **计算机系统概论**  
***Chapter19***  
也是数据结构的内容，不过是Dynamic Data Structure。  
* Structure：结构体，讲的就是一些已经学过的东西；typedef，可用于定义一个新的数据类型名称，方便程序的编写和指针的定义；结构体数组；结构体数组和指针的关系。  
* Dynamic Memory Allocation：讲的是如何用malloc和free函数在Heap中开辟出一块动态存储空间，具体的应用后续可以展现；值得注意的是，malloc返回的是一个 generic pointer (void *)指向被分配的空间，所以要利用type cast来实现对指针的赋值；还有remalloc函数可用于grow/shrink已经分配的空间；这些函数都在stlib.h头文件中；都可应用于dynamic array。  
* Linked Lists：链表的概念；Add/Delete a Node,分为五种情况，Middle/Empty List/at Tail/at Head/(Not)Exits;链表操作的Language C实现；数组与链表的异同。  

***Chapter9***  
讲的是在LC-3中实现I/O，算是从数据结构的部分回归主线，内容有点多，而且学的不是很明白。  

首先是几个小概念：  
* Privilege：权限，一般的计算机使用过程中会分为Supervisor Mode和User Mode，分别对应有无权限。  
* Priority：优先级。  
值得注意的是，这两个概念可以说是坐标轴的横轴和纵轴，以此来理解一个program在执行中的位置。  
* Processor Statu Register(PSR)：状态寄存器，bit[15]-Priv,bit[10:8]-Priority,bit[2:0]-cond code。  

然后讲述Organization of Memory in LC-3：  
* 自上而下system space|SSP|supervisor stack(x0000-x2FFF),user space|USP|user stack(x3000-xFDFF),I/O page(xFE00-xFFFF)。  
* 一个program只能在两种Mode中的一种执行，两种模式切换时SP会分别进行Save&Load。  

重头戏，关于Input/Output。首先是关于I/O的基本特点：
* Memory-Mapped I/O & Special I/O instruction：分别是在Memory中映射出一块内容负责处理I/O的相关内容；一套独立的 I/O Instruction。  
* Asynchronous & Synchronous：I/O device和processor之间的信号交换存在一个同步的问题，因为processor的处理是由Clock决定的存在周期，为了解决这一问题，我们通过设置一个flag called *ready bit*。  
* Interrupt-Driven & Polling：由上一个问题引发的问题，分别对应，由I/O device来打断processor，还是由Processor来时刻查询ready bit的状态来决定是否执行指令。  

Input from Keyboard：有两个基本的Register，**KBDR** & **KBSR**：
* keyboard data register:bit[15:8]=0,bit[7:0]用于存放Data。  
* keyboard statu register：bit[15]存放ready bit，bit[14]存放Privilege。  
然后就是如何利用这两个Register来完成从keybroad输入。  

Output to the Monitor：一样有两个Register，**DDR** & **DSR**：
* display data register:bit[15:8]=0,bit[7:0]用于存放Data。  
* display statu register：bit[15]存放ready bit，bit[14]存放Privilege。  
然后就是如何利用这两个Register完成输出到monitor。  

Example：keybroad echo  
一个更加复杂的样例，当可以input时，在monitor上输出prompt。  
最后就是Data path implementation of memory-mapped I/O（依旧是有点看不懂，又有点懂）。  

LC-3's TRAP Routine：
* TRAP Mechanism：involve several element：A set of service routines；A table of starting addresses；the TRAP instruction;A linkage.
* TRAP instruction :bit[15:12]-opcode,bit[11:8]=0,bit[7:0]-trap vector。In Execute phase，TRAP 做三件事情：1、将PSR&PC push into system stack，按照需求转换SP。2、set bit[15] in PSR to 0.3、将trap vector转换到16 bits以指向Address。  
* RTI instruction：1000000000000000；将之前的PSR和PC pop，回到接下来的address，根据权限切换SP。  
一个切换大小写的样例。  
在后面还会看到完整的储存在LC-3中的用于输出输出的code，还用到了JMP/RET机制。  
Halt：利用一个x7FFF的MASK以完成对Run latch(the bit[15] of MCR(master control register))的清零，从而停止clock。  

中间讲了一块内容，就是如何使用LC-3汇编语言实现puts(),这部分的code也是前面提到的完整keybroad echo代码的一部分（用于输出prompt）。  

最后一块内容就是提到的Interrupt & Interrupt-Driven I/O：
* 展示了一个Interrupt 的流程图，讲述了以下两种机制的差异，主要体现在节省processor的时间上(?)。

*Two Parts of the Processor*:  
1、Causing the interrupt to occur :  
* the device want the service.  
* the device has the privilege.
* the urgency.  
以上的这些必要性都是通过INT signal 来判断的。注意的是，如果确定interrupt，将在current instruction 结束后开始；会出现一个INT vector。  

2、Handling the interrupt request :
* Initiate the interrupt:save the state of the interrupted program(一般只save PSR PC，LC-3默认register's content 已经save);load the state of the interrupt service routine.
* Service the interrupt.
* Return from the interrupt(使用RTI指令，将PC和PSR从supervisor stack中弹出).  

值得注意的是，不是只有I/O可以造成一个Interrupt。  

最后展示了Polling被interrupt导致的问题，并给出一个solution（没怎么看懂）。  
***  
内容还是很多的，幸亏预习了一遍，看看明天早上有没有时间去完成Lab0，主要还是要注重休息。  
也不知道C加强又会有什么乱七八糟的作业，总之加油！  
***  
# 2022/7/8  
今天没学什么东西，早上四点才睡觉，一天都用来补觉了。  
## **计算机系统概论**  
***Chapter10***  
就是讲了一个综合应用，用之前的知识实现一个三位加减乘法的计算器，没细看。  
***  
计概的预习我想就到此为止吧，再过两天就要开始接受Patt的授课了，已经将他的part全部看完了，还是很厉害的！  
还做完了intel的那个不知道啥的作业，真没意思。  
接下来可以将重点放在学习CS61A上了，明天开始吧。  
安倍晋三遇刺。  
***  
