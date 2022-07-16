# **2022/7/10**  
今天打了棒球，其余时间都在写CS61A了。  
# CS61A  
Lab01感想：  
* ```  
  >>> True and 13
  13
  >>> False or 0
  0
  ```
* `and` and `or` always return the last thing they evaluate, whether they short circuit or not.
* Debug相关知识  

Hog感想：
* 有些东西就是不知道为啥会出问题，但又没学会怎么用ok去debug。
***  
明天正式开始上计概了，加油哦噢噢噢！  
***
# **2022/7/11**  
今天做完了CS61A的Hog，做完了才发现很多知识点都没上过，无语。  
ICS的课程质量堪忧，有点不想上，以后就是，早上ICS，中午CS61A，ICS实验课，ICS homework,晚上CS61A的学习模式。  
加油！  
***
# **2022/7/12**  
稍微上了一点CS61A的课。  
## CS61A  
# Lecture4  
* Fibonacci Sequence starts at 0  
* A function's domain is the set of all inputs it might possibly take as arguments.  
* A function's range is the set of output values it might possibly return.  
* A pure function's behavior is the relationship it creates between input and output.
* **high-order function**: a function that takes a function as an argument value or returns a function as a return value.
* ```
  assert expression , 'string'
  ```
  when expression is True, nothing happens; when expression if False, print the string.
* Functions defined within other functions bodies are bound to names in a *local* frame
* functions can be manipulated as values in our programming language.
* express general methods of computation; remove repetition from programs; separate concers among functions.  
***  
昨天没写，这份是13号，写的，忘记了。  
***  
# **2022/7/13**  
早起，不错。  
## CS61A  
看完了相关的reading，还把discuss做完了。  
***  
## ICS  
今天用机器语言写出了这个程序，很麻烦，要是用汇编语言都能快很多，究极折磨，贴一下代码吧。  
```
0011 0000 0000 0000         ;.ORIG X3000
0010 000 01111 1111         ;LD R0,#255      ;将数据加载到R0
0101 001 001 1 00000        ;AND R1,R1,#0    ;初始化R1，用于存放掩码
0101 010 010 1 00000        ;AND R2,R2,#0    ;初始化R2，用于存放结果
0101 011 011 1 00000        ;AND R3,R3,#0    ;初始化R3，用于存放掩码与数据的与运算结果
0101 100 100 1 00000        ;AND R4,R4,#0    ;初始化R4，用于存放掩码的相反数的补码
0101 101 101 1 00000        ;AND R5,R5,#0    ;初始化R5，用于计数器

0001 001 001 1 01111        ;ADD R1,R1,#15
0001 101 101 1 10011        ;ADD R5,R5,#-13  ;计数器初始值

0101 011 000 0 00 001       ;AND R3,R0,R1    ;获得掩码与数据的与运算结果
1001 100 001 1 11111        ;NOT R4,R1       
0001 100 100 1 00001        ;ADD R4,R4,#1    ;获得掩码的反码的补码
0001 011 011 0 00 100       ;ADD R3,R3,R4    ;计算结果

0000 010 000001000          ;JUDGE   BRZ RESULT;判断结果是否为0
0001 101 101 1 00001        ;ADD R5,R5,#1    ;R5自增
0000 010 000000111          ;BRZ FINAL;判断R5是否为0
0001 001 001 0 00 001       ;ADD R1,R1,R1    ;掩码前移

0101 011 000 0 00 001       ;AND R3,R0,R1    ;获得掩码与数据的与运算结果
1001 100 001 1 11111        ;NOT R4,R1       
0001 100 100 1 00001        ;ADD R4,R4,#1    ;获得掩码的反码的补码
0001 011 011 0 00 100       ;ADD R3,R3,R4    ;计算结果
0000 111 111110111          ;BRNZP JUDGE     ;返回判断语句

0001 010 010 1 00001        ;RESULT  ADD R2,R2,#1
1111 0000 00100101          ;FINAL   HALT
                            ;.END
```  
只能说是看着容易写着难。  
***
听课方面，还是得听，但是看别的网课感觉更有效率，纠结，好好上课吧，真的努力不差这几天的。
***
# **2022/7/14** 
## CS61A
完成了Lecture5的内容，完成了hw02.
## Lecture5  
* 关于嵌套定义函数和environment diagram的知识
* local name
* **lambda expression**的用法
* lambda's return must be a single expression.
* lambda expression versus def statements:
  * both create a function with the same domain, range, and behavior.
  * both functions have as their parent the frame in which they were defined.
  * both bind that function to the name square.
  * only the def statement gives the function an **intrinsic name**.

Homework感想：  
基础题目都会做了，但是关于丘奇数的拓展题很难，对函数的理解非常不透彻，以后找机会补一下。
***
# ICS  
首次Lab验收通过了，上课内容开始听了。  
***
现在的学习很规律。  
***
# 2022/7/15
## CS61A
完成了Lecture6的学习，完成了Lab02.  
## Lecture6  
* return statement completes the evaluation of a call and provide its value.  
* only one return statement is ever executed while executing the body of a function.
* 不能用call expression来代替if statement
* control expression:
  * `<left> and <right>`
  * `<left> or <right>`
* conditional expression
  * `<consequence> if <predicate> else <alternative>`
  * if the predicate true, value equals the value of consequence,else the alternative.

Lab感想：对函数的嵌套等定义还是很模糊，做起题目来并非得心应手。
***  
明天继续加油。
***
# 2022/7/16  
第二周结束，有点小偷懒，但还是学的不错的。  
## CS61A  
## Lecture6  
* return statement completes the evaluation of a call and provide its value.  
* only one return statement is ever executed while executing the body of a function.
* 不能用call expression来代替if statement
* control expression:
  * `<left> and <right>`
  * `<left> or <right>`
* conditional expression
  * `<consequence> if <predicate> else <alternative>`
  * if the predicate true, value equals the value of consequence,else the alternative.  

Lab感想：对函数的嵌套等定义还是很模糊，做起题目来并非得心应手。
***
# Lecture7
* an example to introduce why we need high-order function
# Lecture8
* Function Curring
* Decorater
* Mid review、
***  
做完了ics的作业，明天写Lab02，顺便和他们一起玩会PUBG，加油！
