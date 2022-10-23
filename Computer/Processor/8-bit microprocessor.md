### Design 8-bit Microprocessor
----
#### 1. Instroduction
|Computer architecture|
|--|
|![image](https://user-images.githubusercontent.com/59242221/167363716-bd289a89-fe90-48c8-982c-b1278d484ca5.png)|

* 8-bit data bus
* 16-bit address bus
* Instructions formatted </br>

|![image](https://user-images.githubusercontent.com/59242221/167353584-12103a0a-d22e-41e7-af17-54f901696091.png)|
|--|
* Instruction set 

|Instruction|Opcode|Operands|
|-----------|------|--------|
|NOP|0x00|---|
|Add|0x01|reg,reg/imm|
|Subtract|0x02|reg,reg/imm|
|Multiply|0x03|reg,reg/imm|
|Logical AND|0x04|reg,reg/imm|
|Logical OR|0x05|reg,reg/imm|
|Logical shift right|0x06|reg|
|Logical shift left|0x07|reg|
|Complement bits|0x08|reg|
|Load|0x010|reg,reg/address|
|Store|0x11|address,reg|
|Move|0x12|address,address|
|Jump|0x0F|address,condition|
|Halt|0x1F|----|
* Jump condition codes </br>

|Condition|Bit designation|
|-----------|------|
|Always|00|
|Carry|01|
|Zero|10|
|Negative|11|
#### 2. Chip-level IO
* Clock - Square wave input from function generator
* Reset - Active low input from switch
* Address bus - 16-bit output bus
* Data bus - 8-bit bidirectional bus
* ROM enable - Active low signal which enables the EEPROM
* RAM enable - Active low signal which enables the SRAM
* Memory write - Active high signal which switches the direction of the bidirectional buffer
* Write - Active low signal which enables writing to SRAM

#### 3. Module design
* Generic 16-bit register
```
 A 16-bit register is used three times in the design: the jump register, 
 the memory address register, and the instruction register. The same module
 is instantiated in all three of these cases.
 ```
|16-bit register block diagram|
|--|
|![image](https://user-images.githubusercontent.com/59242221/167378286-d8156b03-6176-4de9-834a-90d53e353078.png)|
```
module register_16bit(clock, reset, setHigh, setLow, halfValueIn, valueOut);
  input clock;
  input reset; // Synchronous reset; active low
  input setHigh;// When this signal is high, the top half of the value is loaded from the input line (data bus)
  input setLow;
  input [7:0] halfValueIn;
  output reg [15:0] valueOut; 
  
  always @(posedge clock) begin
    if(~reset) begin 
      valueOut = 0;
    end
    else if(setHigh) begin
      valueOut[15:8] = halfValueIn;
    end
    else if(setLow) begin
      valueOut[7:0] = halfValueIn;
    end
  end
 
endmodule
```
* Program counter
```
The program counter holds the address of the next instruction byte and is used to index ROM when fetching
instructions. It increases the output count by on the rising edge of the clock when the increment signal
is high. When the set signal is asserted, it loads the value from the jump register through the input
newCount.
```
|Program counter block diagram|
|--|
|![image](https://user-images.githubusercontent.com/59242221/167391044-2ab2a5c5-17c7-430c-b9b4-d69528831b44.png)|

* General-purpose register block
```
The general-purpose register block contains 8 eight-bit registers which are used for data
manipulation. Theyare grouped into pairs, creating 4 sixteen-bit registers which can receive
the result of a multiply operation.
```
|Program counter block diagram|
|--|
|![image](https://user-images.githubusercontent.com/59242221/167391622-abee894b-f571-46c7-a236-fa50844f77ed.png)|

* Arithmetic logic unit(ALU)
```
The arithmetic logic unit implements all of the arithmetic operations specified: addition,
subtraction, multiplication, logical AND and OR, left and right logical shifts, left and
right arithmetic shifts, bitwise complement, and negation. It also contains a passthrough 
instruction so that the ALU latch can be used as atemporary register for the MOVE operation. 
Output flags are set based on the results of the operation
```
|ALU block diagram|
|--|
|![image](https://user-images.githubusercontent.com/59242221/167392207-71bed916-7253-4cfc-bcdb-4a86530c3e09.png)|

* ALU latch
```
The ALU latch uses a simple sequential design. The alu_result and flags are stored on the 
rising edgeof the clock if grab is high. Combinational logic is used to determine which half 
of the stored value is putout to the data bus. If neither store signal is high, the output is
high-z. The flags_out output is always enabled.
```
|ALU block diagram|
|--|
|![image](https://user-images.githubusercontent.com/59242221/167393143-9d6edbcf-c744-4634-8377-0be7d49ea9cd.png)|

* Datapath
```
The datapath module combines the program counter, jump register, general-purpose registers,
ALU, ALU latch, memory address register, and instruction register into a single unit 
connected by a data bus. The databus is a bidirectional module port, so data can be brought 
in and out of the chip.
```
|Datapath block diagram|
|--|
|![image](https://user-images.githubusercontent.com/59242221/167380565-744265a8-8c3f-4324-8703-a191331afa18.png)|

* Control module
```
The control module consists of two separate modules: a state machine which reads the output of
the instruction register and determines what to do on the next clock cycle, and a signal 
translation module whichmaps the control state into controls signals for all of the other modules.
```
|Block diagram of control module|
|--|
|![image](https://user-images.githubusercontent.com/59242221/167382729-cebaf59a-4345-44f5-bea3-98d36888e9ce.png)|
* Address multiplexer

* Memory IO
```
The memory IO module performs memory mapping to locate the ROM and RAM in address space, and
translates the read and write signals into ROM and RAM chip enable signals.
```
|Block diagram of memory IO module|
|--|
|![image](https://user-images.githubusercontent.com/59242221/167383838-8a62471b-8571-4f40-92fb-5642daf8fe02.png)|

* Complete chip

|CPU block diagram|
|--|
|![image](https://user-images.githubusercontent.com/59242221/167376618-c6937d5e-9736-487f-bc73-c063e7ea9b66.png)|

#### 3. Hardware implementation
|Block diagram of breadboard layout|
|---|
|![image](https://user-images.githubusercontent.com/59242221/167401306-ebb50780-36ee-4240-b367-6600bae9339c.png)|

