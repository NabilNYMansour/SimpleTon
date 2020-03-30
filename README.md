#SimpleTon CPU
- This is a simple CPU design.
- It utilizes a central register that acts as a midpoint for all data called %CORE or %C for short.
- Made with logism.
- Here you will find full explanation on how this works.
---
The following is an image of the CPU design with designated sections:
![SimpleTon CPU](https://github.com/longchickenlegs/SimpleTon/blob/master/README_pictures/Capture_Annotated.png)

---
The CPU has the following registers:
- The %R register set (%R0 to %R3) which serve as short term memory for the CPU. %R3 is also connected to a 2 HEX digit display.
- The %CORE register as mentioned above.
- The %MC or %MemoryCounter register which serves as a stack pointer for the memory.
- The %V register set (%V1 and %V2) which serve as the registers that the ALU (arithmetic logic unit) would execute the operations on.
---

