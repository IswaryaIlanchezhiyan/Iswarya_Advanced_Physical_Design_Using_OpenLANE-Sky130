# OpenLANE/Sky130
# Table of Contents 
 - [Day0 -Installation ](#Installation)<br>
 - [Day1 -Inception of open-source EDA,OpenLANE and Sky130PDK ](#Inception-of-open-source-EDA,OpenLANE-and-Sky130PDK)<br>

 # Day 0
 # Installation

 <details>
 <summary>
   OpenLANE
 </summary>
 I installed OpenLANE using the following commands:

 ```

$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt install -y build-essential python3 python3-venv python3-pip make git
$ sudo apt install apt-transport-https ca-certificates curl software-properties-common
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
$ echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
$ sudo apt update
$ sudo apt install docker-ce docker-ce-cli containerd.io
$ sudo docker run hello-world
$ sudo groupadd docker
$ sudo usermod -aG docker $USER
$ sudo reboot

```

After Reboot

```

$ docker run hello-world

```

Below is the screenshot of successful launch

![Screenshot from 2023-09-05 18-00-04](https://github.com/IswaryaIlanchezhiyan/Iswarya_asic_course/assets/140998760/c5b4808f-c46e-476c-affb-0edd9353880d)

</details>

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

<details>
 <summary>
   SoC Design and OpenLANE
 </summary>
 
**Introduction to all components of open-source digital ASIC design**

ASIC Enablers
+ RTL IPs
+ EDA Tools
+ PDK Data

**RTL IPs** 
RTL IP Integration enables IP packaging, integration, documentation and reuse based on the IPXACT format. Starting from a RTL block, IP core or SoC, the tool helps generate the related IPXACT description.

**EDA Tools**
Electronic Design Automation, or EDA, is a market segment consisting of software, hardware, and services with the collective goal of assisting in the definition, planning, design, implementation, verification, and subsequent manufacturing of semiconductor devices, or chips.

**PDK**
A Process Design Kit (PDK) is a library of basic photonic components generated by the foundry to give open access to their generic process for fabrication.

![ASIC enabler](https://github.com/IswaryaIlanchezhiyan/Iswarya_sky130/assets/140998760/89b2d0e3-b60f-4287-8ccd-57e2f1380b33)

**Simplified RTL2GDS flow**

![rtl2gdsflow](https://github.com/IswaryaIlanchezhiyan/Iswarya_sky130/assets/140998760/bdefd1a0-895d-4a98-98f5-e0f9303900ef)

**1.Synthesis** - converts RTL to a circuit out of components from the standard cell library.
A standard-cell library is a collection of low-level electronic logic functions such as AND, OR, INVERT, flip-flops, latches, and buffers. These cells are realized as fixed-height, variable-width full-custom cells.

![synthesis](https://github.com/IswaryaIlanchezhiyan/Iswarya_sky130/assets/140998760/46e85e6e-695b-4fa8-a97b-2b74ec62a41e)

**2.Floor/Power Planning**  

Chip Floor-planning - partition the chip die between different system building blocks and place the I/O pads

![chip planning](https://github.com/IswaryaIlanchezhiyan/Iswarya_sky130/assets/140998760/c44a7036-1c6e-4053-b075-ca043f3e7c2a)

Macro Floor-planning - dimensions,pin locations,row dimensions

![macro plan](https://github.com/IswaryaIlanchezhiyan/Iswarya_sky130/assets/140998760/83228a9f-0aa5-48f0-ab5d-e504e3a752e0)

Power Planning  - provide power to the every macros, standard cells, and all other cells are present in the design

![power plan](https://github.com/IswaryaIlanchezhiyan/Iswarya_sky130/assets/140998760/bde5f4bc-ba2f-4d6e-bf8c-9005d3563c34)

**Placement** 

Place the cells on the floorplan rows,aligned with the sites

![placement](https://github.com/IswaryaIlanchezhiyan/Iswarya_sky130/assets/140998760/b69fedde-2145-483e-9951-8f30fb5bedfb)

Placement usually done in 2 steps:

1.Global

2.Detailed

![placement 2](https://github.com/IswaryaIlanchezhiyan/Iswarya_sky130/assets/140998760/fd5c2425-ecbe-4320-8aad-dc0d0d17ef2b)

**Clock Tree Synthesis**

The concept of Clock Tree Synthesis (CTS ) is the automatic insertion of buffers/inverters along the clock paths of the ASIC design in order to balance the clock delay to all clock inputs. In order to balance clock skew and minimize insertion delay, CTS is performed.

A clock tree has different structures:

+ Fish bone+
+ H-tree
+ X-tree
+ Multi-level clock tree

**Routing**

Routing is making physical connections between signal pins using metal layers.

![routing](https://github.com/IswaryaIlanchezhiyan/Iswarya_sky130/assets/140998760/54e16de1-7e88-46de-b615-1f0222f9b14f)

**Sign Off**

Sign off includes 
+ the physical verification of the design
+  the timing verification of the design
+  the power verification of the design
+  the electrical verification of the design
  
 Once all these verifications are completed and the chip is deemed to be functioning as expected, the design can be signed off.

 **Introduction to OpenLANE and Strive chipsets**

 **OpenLane** is a RTL to GDSII infrastructure library based on several components including OpenROAD, Yosys, Magic, Netgen, CVC, SPEF-Extractor, KLayout and a number of custom scripts for design exploration and optimization.

 OpenLane abstracts the underlying open source utilities, and allows users to configure all their behavior with just a single configuration file, but also allows for completely custom, Python-based scripts.

 OpenLANE can be used to harden Macros and Chips.

 Two modes of operation:

 + Autonomous or Interactive
 + Design Space Exploration

**Introduction to OPenLANE detailed ASIC Design flow**

![openlane designflow](https://github.com/IswaryaIlanchezhiyan/Iswarya_sky130/assets/140998760/10ba224c-7974-47fb-9bcb-8b07b8125485)

**Synthesis Exploration**


+ Yosys is used for RTL synthesis
+ ABC is used for logic synthesis and technology mapping

 ABC needs a script that defines the sequence of optimization operations.OpenLane comes with several synthesis scripts,We call them “Synthesis Strategies”.Synthesis Exploration can help picking the best
strategy for a given design.

**Design Exploration**

 + OpenLane has 16 design specific configurations
 + Not all combinations may result in a DRC clean layout
 + OpenLane can sweep different parameters to help with that
 + For each run, OpenLane collects around 35 different design metrics

**OPenLANE Regression**

+ The design exploration utility is, also, used for regression testing
+ We run OpenLane on ~70 designs and compare the results to the best known ones

**Design for Test**

 + Scan Insertion
 + Automatic Test Pattern Generation (ATPG)
 + Test Patterns Compaction
 + Fault Coverage
 + Fault Simulation

**Physical Implementation**

+ Also called automated PnR (Place and Route)
+ Floor/Power Planning
+ End Decoupling Capacitors and Tap cells insertion
+ Placement: Global and Detailed
+ Post placement optimization
+ Clock Tree Synthesis (CTS)
+ Routing: Global and Detailed

**Logic Equivalence check**

 + Every time the netlist is modified (ECO), verification must be performed
   
      1.CTS modifies the netlist
   
      2.Post Placement optimizations modifies the netlist
 + LEC is used to formally confirm that the function did not change by modifying the netlist

**Dealing with Antenna Violations**

 + When a metal wire segment is fabricated, it can act as an antenna.
 + Reactive ion etching causes charge to accumulate on the wire.
 + Transistor gates can be damaged during fabrication

 + Two solutions:
   
   1.Bridging attaches a higher layer intermediary
      + Requires Router awareness (not there yet!)

   2.Add antenna diode cell to leak away charges
      + Antenna diodes are provided by the SCL

**Physical verification DRC & LVS**

 + Magic is used for Design Rules Checking and SPICE Extraction from Layout
 + Netgen is used for LVS
 + Extracted SPICE by Magic vs. Verilog netlist
</details>
<details>
 <summary>
   Open source EDA Tools
 </summary>

 
</details>
 
