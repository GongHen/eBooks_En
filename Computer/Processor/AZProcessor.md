### 《CPU自制入门》
--------
#### AZ Processor流水线设计
* IF(Instruction Fetch) :将PC的值发送到内存，读取指令;
* ID(Instruction Decode) :将读取的指令解码并决定将要进行的操作，从寄存器堆读取数据;
* EX(Execution) :使用运算器(Arithmetic and Logic Unit)执行操作;
* MEM(Memory Access) :进行内存访问; 
* WB(Write Back) :将结果写回寄存器堆。
![image](https://user-images.githubusercontent.com/59242221/167973967-67021868-3a25-49a2-91e9-7b1b1c5336bd.png)

* AZProcessor流水线构造
![image](https://user-images.githubusercontent.com/59242221/167756149-0732208e-86c4-44db-87fc-419ccca18bf0.png)

* 指令格式
![image](https://user-images.githubusercontent.com/59242221/167756507-e9b5532c-6885-46c8-9e2f-5645726e31b8.png)
* CPU顶层模块连接
![image](https://user-images.githubusercontent.com/59242221/168000508-35c11dfe-98dc-499c-a775-608632bcc731.png)

#### 2.电路板制作
* 制作流程

![image](https://user-images.githubusercontent.com/59242221/168007930-01a11db6-f1d5-48ac-8bd1-69ecf86aa858.png)
* 元件选型

![image](https://user-images.githubusercontent.com/59242221/168009489-177f6905-dea3-40be-97d2-fd773e723e6d.png)
