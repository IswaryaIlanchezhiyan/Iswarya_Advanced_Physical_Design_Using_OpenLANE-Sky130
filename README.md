# OpenLANE/Sky130
# Table of Contents 
 - [Day1 -Inception of open-source EDA,OpenLANE and Sky130PDK ](#Inception-of-open-source-EDA,OpenLANE-and-Sky130PDK)<br>

 # Day 1
 # Inception of open-source EDA,OpenLANE and Sky130PDK
 <details>
   <summary>
       Introduction to QFN-48 Package,chips,pads,core,die and IPs
   </summary>

   **Arduino** 
   
Arduino is an open-source platform that helps circuit developers build electronic projects. It consists of both hardware and software. Arduino hardware is a programmable circuit board called a microcontroller. Arduino software is an IDE (integrated development environment) through which developers write and upload the code to the microcontroller. We can feed a program with a set of instructions to the Arduino board that can carry out simple to complex tasks.

  **Block Diagram of Arduino Board**

   ![Arduino](https://github.com/IswaryaIlanchezhiyan/Iswarya_sky130/assets/140998760/d421c2f2-2714-405f-9158-200d5a4a7bad)

   The chip in the Arduino board looks like

   ![Arduino board](https://github.com/IswaryaIlanchezhiyan/Iswarya_sky130/assets/140998760/edf64881-76a4-43e1-aa7b-220e920fb395)

   Wire bounds are used to connect QFN-48 Package pins to the boundaries of the chip.

   Components inside the chip
   
   ![arduino chip](https://github.com/IswaryaIlanchezhiyan/Iswarya_sky130/assets/140998760/e3618f3c-d071-40ee-abe0-95c22a16438f)

   **Pads** - are something through which we can send signals inside the chip.

   **Core** - is the place where all the digital logic's are placed in the chip.

   **Foundry** - is a place where the chips are manufactured.

   **IP** -  An intellectual property core (IP core) is a functional block of logic or data used to make a field-programmable gate array (FPGA) or application-specific integrated circuit for a product.Foundry IPs are used for communication inside the chip.

   **Macros** - Macro Cells are the Memory cells. These IPs have been designed by some other Analog design team, which can be used in the floor plan stage of the design.

</details>

<details>
 <summary>
   Introduction to RISC-V
 </summary>

**RISC-V**

 RISC-V (“risk-five”) is an instruction set architecture (ISA) rooted in reduced instruction set computer (RISC) principles. RISC-V is unique, even revolutionary, because it is a common, free, open-source ISA to which software can be ported, hardware can be developed, and processors can be built to support it.

**ISA**

An Instruction Set Architecture (ISA) is part of the abstract model of a computer that defines how the CPU is controlled by the software. The ISA acts as an interface between the hardware and the software, specifying both what the processor is capable of doing as well as how it gets done.The ISA provides the only way through which a user is able to interact with the hardware.

ISA also known as **Abstract Interface** and **Architecture of Computer**.

 **Diagrammatic Representation**

![Diagrammatic Representation](https://github.com/IswaryaIlanchezhiyan/Iswarya-RISC-V/assets/140998760/04cf63c8-a085-45c8-9879-791dbaae9c32)

**System Software**

System Software is the interface between Hardware and User Applications.System Software includes
+ Operating Systems
+ Compiler
+ Assembler

**Operating Systems**

It converts apps into their respective assembly language program and then into binary code for the hardware to understand it.
It also 
+ handle IO operations
+ allocate memory
+ low level system functions


**Compiler**

It is a special program that translates a programming language's source code into Instruction sets(.exe file).

Instruction sets depends on the hardware that we are going to use.

**Assembler**

It converts Instruction sets into binary code(logic 1 & logic 0).

**Instruction Sets**

Initially, we get specifications from ISA and write a HDL (Hardware Description Language) code which get synthesized into a gate level design .Gate Level Design is then converted into respective layout(Hardware).

**Instruction Set Architecture** has
+ Pseudo Instructions
+ Base Integer Instructions(RV64I)
+ Multiply Extension(RV64M)
+ Single & Double precision floating point extension (RV64F & RV64D)
+ Application Binary Interface
+ Memory Allocation & Stack Pointer

</details>
 
