#SimpleTon CPU
- This is a simple CPU design.
- It utilizes a central register that acts as a midpoint for all data called %CORE or %C for short.
- Made with logism.
- Here you will find full explanation on how this works.
---
The following is an image of the CPU design with designated sections:
![SimpleTon CPU](https://github.com/longchickenlegs/SimpleTon/blob/master/README_pictures/Capture_Annotated.png)
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


- The big squares and numbers are sections of the CPU. This will be used for explaning the CPU structure.

---
###Registers
The CPU has the following registers:
- The %R register set (%R0 to %R3) which serve as short term memory for the CPU. %R3 is also connected to a 2 HEX digit display.
- The %CORE register as mentioned above.
- The %MC or %MemoryCounter register which serves as a stack pointer for the memory.
- The %V register set (%V1 and %V2) which serve as the registers that the ALU (arithmetic logic unit) would execute the operations on.
---
###Explanation

---
