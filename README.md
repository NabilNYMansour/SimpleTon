# SimpleTon CPU
- This is a simple CPU design.
- It utilizes a central register that acts as a midpoint for all data called %CORE or %C for short.
- Made with logism.
- Here you will find full explanation on how this works.
---
The following is an image of the CPU design with designated sections:
![SimpleTon CPU](https://github.com/longchickenlegs/SimpleTon/blob/master/Capture_Annotated.png)
Key:
- (1) EwtC: Enable write to %C.
- (2) Value: The value to be placed in %C.
- (3) ptCfR: Place to %C from a selected %R.
- (4) pfCtR: Place from %C to a selected %R.
- (5) RSelect: The select bit for the %R register set.
- (6) pfCtMC: Place from %C to %MemoryCounter.
- (7) ptCfMC: Place to %C from %MemoryCounter.
- (8) ptCfV: Place to %C from ALU output.
- (9) pfCtV: Place from %C to a selected ALU register.
- (10) VSelect: The select bit for %V register set.
- (11) Oper: The operation to be executed by the ALU.
- (12) ptCfIn: Place to %C from input value.
- (13) pfCtML: Place from %C to a Memory location (as pointed by %MC).


- The big squares and numbers are sections of the CPU. This will be used for explaining the CPU structure.

---
### Registers
The CPU has the following registers:
- The %R register set (%R0 to %R3) which serve as short term memory for the CPU. %R3 is also connected to a 2 HEX digit display.
- The %CORE register as mentioned above.
- The %MC or %MemoryCounter register which serves as a stack pointer for the memory.
- The %V register set (%V1 and %V2) which serve as the registers that the ALU (arithmetic logic unit) would execute the operations on.
---
### Explanation
The CPU is divided into sections:
#### Section 1: The register set.
Consists of 4 Registers (%R0 to %R3) that can send and take information using a double sided multiplexer (DSMUX). There is also a decoder that enables a certain register for
writing.
#### Section 2: The Input set.
Consists of the input value that is to be inserted to %CORE. It also has  MUX and an encoder such that the MUX would give %CORE the intended value based on the “ptCf” enabled. Those enables are encoded by the encoder so that they play as select bits for the MUX. To be more specific the “ptCf” enables are (12), (3), (7), (8). It's noted that there is an enable for Value that turns on when %CORE enable is on.
#### Section 3: The Core.
Consists of the CORE register that all values must pass through as it acs as the connector of all the other sections It has an enable that, in reality, is simply equal to the following: (1) EwtC = (12) OR (3) OR (7) OR (8). There is a 4-input OR gate to represent that.
#### Section 4: The ALU.
Consists of an ALU chip with an enable and two registers. There is a MUX that decides which ALU register should get its value from %CORE and a decoder that allows the enable of the selected ALU register to be ON. 

**The operations are as follows for the ALU:**
00 for +
01 for -
10 for AND
11 for OR

#### Section 5: The Memory Counter.
Consists of a register used to represent the current position of the pointer in memory, or in other words, serves as the select bit for the RAM or ROM chips. It has a MUX used to give the %MC the value of %C or the counter's current value. The (6) enable (pfCtMC) acts as a select bit for the MUX. The OR gate exists because the %MC needs to be updated when either a value from %C needs to ne added OR a step is made.
**note:** When placing a value from %CORE to %MC, the (6) enable needs to be ON again (In the next clock cycle) as to sync the value of %MC with the counter register (place %MC's value in the counter).
#### Section 6: The Memory Command set.
This section has the memory (RAM or ROM) where the code will need to be. It takes the value of %MC as its select bit. Also, there is a CommandLine sender that simply has decoder since the code within the memory is only **16 bits**.
The CommandLine sender takes inputs **A B C O(2b) V r(2B) VALUE(8b)** from the memory and outputs the values in the specific order shown below:
|** A **|** B **|** C **| With the decoder
| 0 | 0 | 0 | => (13)
| 0 | 0 | 1 | => (12)
| 0 | 1 | 0 | => (7)
| 0 | 1 | 1 | => (3)
| 1 | 0 | 0 | => (8)
| 1 | 0 | 1 | => (6)
| 1 | 1 | 0 | => (4)
| 1 | 1 | 1 | => (9)
So the output would be as follows:
**13, 12, 7, 3, 8, 6, 4, 9, OPER, VSELECT, RSELECT, VALUE**
Such that it corrosponds to the machine code:
**[ABC]OOVRRxxxxxxxx**
where **O** is Operation, **V** is VSelect, **R** is RSelect, and **x** is a Value bit.

---
### Sample Code
The following is a sample code for the following operation:
**5 + 22**
- Load 5 into Core
- Load Core into V1
- Load 22 into Core
- Load Core into V2
- Perform Addition operation and place value in Core
- Load Core into R3
- Write to current Memory location.

Such that it has the following hex equivalent:
- 2005
- e000
- 2016
- e400
- 8000
- c300
- 0000
**note:** Since 0000 is the code for writing to memory location (this isn't the best design of a CPU) Core must be cleared at the end of the program by using the following code:
- 2000
Which basically means Load 0 into Core.
---
This is my first attempt on making a CPU from the ground up so I hope u like it :)
