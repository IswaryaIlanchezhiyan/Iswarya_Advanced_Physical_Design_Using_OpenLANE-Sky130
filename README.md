# Advanced Physical Design using OpenLANE/Sky130
# Table of Contents 
 - [Day1 -Inception of open-source EDA,OpenLANE and Sky130PDK ](#Inception-of-open-source-EDA,OpenLANE-and-Sky130PDK)<br>
 - [Day2 -Good floorplan vs Bad floorplan and Introduction to library cells](#Good-floorplan-vs-Bad-floorplan-and-Introduction-to-library-cells)<br>
  - [Day3 -Design Library Cell using Magic Layout & Ngspice Characterization](#Design-Library-Cell-using-Magic-Layout-&-Ngspice-Characterization)<br>
  - [Day4 -Pre-layout timing analysis and importance of good clock tree](#Pre-layout-timing-analysis-and-importance-of-good-clock-tree)<br>
  - [Day5 -Final steps for RTL2GDS using tritonRoute and openSTA](#Final-steps-for-RTL2GDS-using-tritonRoute-and-openSTA)<br>
  - [References](#References)<br>



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

**OpenLANE Regression**

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


 
Docker Installation:

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

OpenLANE Installation:

```

$ git clone https://github.com/The-OpenROAD-Project/OpenLane --recurse-submodules 
$ cd OpenLane
$ sudo make
$ sudo make test

```

Invoking OpenLANE:

```

$ sudo make mount
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis

```

![openlane install](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/a0f8dcb4-2fea-4134-a6d3-90e531aecd10)

To view the synthesis report:

```

cd /OpenLane/designs/picorv32a/runs/RUN_2023.09.11_10.18.48/reports/synthesis
vim 1-synthesis.AREA_0.stat.rpt

```

![synthesis report](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/2730d4ff-1429-4329-9caf-ec32f8ced042)

**Flop Ratio**

Flop Ratio = (Number of D Flipflops)/(Total Number of Cells) = (1596)/(10104) =  0.1579

 </details>

 # Day 2
 # Good floorplan vs Bad floorplan and Introduction to library cells

 <details>
  <summary>
   Chip Floor planning considerations
  </summary>

  **Utilization Factor and Aspect Ratio**

  ```

  Utilization Factor =  Area occupied the Netlist
                        __________________________
                        Total Area of the Core

```

```

 Aspect Ratio = Height
                _______
                Width

```
If the value of Aspect Ratio is 1,the chip is square shaped.

**Preplaced of Cells**

The very first step in chip design is floorplanning, in which the width and height of the chip, basically the area of the chip, is defined. A chip consists of two parts, 'core' and 'die'.During placement and routing, most of the placement tools, place/move logic cells based on floorplan specifications. Some of the important or critical cell's locations has to be pre-defined before actual placement and routing stages. The critical cells are mostly the cells related to clocks, viz. clock buffers, clock mux, etc. and also few other cells such as RAM's, ROM,s etc. Since, these cells are placed in to core before placement and routing stage, they are called 'preplaced cells'. 

**De-coupling Capacitors**

A decoupling capacitor is a capacitor, which is used decouple the critical cells from main power supply, in order to protect the cells from the disturbance occuring in the power distribution lines and source. The purpose of using decoupling capacitors is to deliver current to the gates during switching.

**Power Planning**

One of the most important stages in physical design is power planning. It will be utilized to supply power to macros and standard cells while staying under the IR-Drop limit. The resistance of the metal wires that make up the power distribution network causes a steady-state IR Drop. Steady-state IR Drop minimizes the voltage differential between local power and ground, lowering the speed and noise immunity of local cells and macros.

![powerplanning](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/b0c7884b-258b-43d3-b798-5b758f64346e)

Rings: Its Carries VDD and VSS around the chip

Stripes: Its Carries VDD and VSS from Rings across the chip

Rails: It connects VDD and VSS to the standard cell VDD and VSS.

Trunk: The connection between Pad and Ring

Pad: Interface from IC  to the outside world.

Power Planning calculates  the required number of power pins,Rings and stripes count,Ring and striped widths,IR drop.


**Pin Placement and Logical Cell Placement Blockage**

Pin Placement details basically come from the TOP level design where we are having information to place pins according to the interaction with other HMs.
We need to define edge, layer and location before placing pins.After pin placement, IO Pad placement happens.

**Steps to run Floor plan using OpenLANE**

```

run_floorplan

```

![runfloorplan](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/21082ce8-16a5-45d7-8645-b053d6d305a3)


To view Floorplan in Magic Layout:

```

cd /home/iswarya/OpenLane/designs/picorv32a/runs/RUN_2023.09.17_06.20.00/results/floorplan
magic -T /home/iswarya/OpenLane/open_pdks/sky130/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read picorv32.def &

```

![runfloorplan layout](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/df27d6a4-3a9f-4be2-abb9-addb3075adf9)

 </details>

 <details>
  <summary>
    Library Binding and Placement
  </summary>

  **Netlist Binding and initial Design**

  In electronic design, a netlist is a description of the connectivity of an electronic circuit. In its simplest form, a netlist consists of a list of the electronic components in a circuit and a list of the nodes they are connected to. Generally,we have gates like and,or etc. and flipflops in our design.But in reality,they have a physical dimension like square,rectangular etc.

  The cells in the design have various parameters like width,height,time information.delay and certains conditions for execution all the parameters are stored in Library.

  **Optimized Placement**

  Now ,we have to place the cells in the floorplan.If the input to the cells are far away from each other ,Repeaters (Buffers) are placed inbetween Input pin and Cells for passing correct information and for reducing delay.

![optimize placement](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/4597080d-fda0-4325-94e5-e7c17f8f5c05)

**Need for Library Characterization**

Knowing the logical function of a cell is not sufficient to build functional electrical circuits. More aspects need to be considered; for example, the speed of a single cell will influence the speed of the full circuit, just as the power used by a single cell can influence the total power. Further, the speed as well as the power might be influenced by the output load. Standard-cell characterization aims at collecting this sort of information.

Library characterization is a process of simulating a standard cell using analog simulators to extract input load, speed, and power data in a way that the downstream tools can process it all. This can be done via a specific analog simulator whose output is used to generate the characterization data, or by using a library characterization tool.

**Congestion aware placement using Replace**

**Legalization** - During legalization, the tool moves the cells to legal locations on the placement grid and eliminate any overlap between cells. These small changes to cell location cause the lengths of the wire connections to change, possibly causing new timing violations. Such violations can often be fixed by incremental optimization, for example: by resizing the driving cells.


**Global Placement** - There is no legalization.

**Detailed Placement** -  There is legalization.


**Steps to run Placement using OpenLANE**

```

run_placement

```

![run placement](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/90b904c8-e739-4144-81bb-880bcdab6258)

To view Placement in Magic Layout:

```

cd /home/iswarya/OpenLane/designs/picorv32a/runs/RUN_2023.09.17_06.20.00/results/placement
magic -T /home/iswarya/OpenLane/open_pdks/sky130/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read picorv32.def &

```

![runplacement layout](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/ca5fa906-6f3b-485c-9c84-cba810f58659)


 </details>

 <details>
  <summary>
   Cell Design and Characterization Flows
  </summary>

  **Cell Design Flow**

It has three steps:
+ Inputs for Cell Design Flow
+ Design Steps
+ Outputs

**Inputs** - are from Process Design Kits(PDKs): DRV &LVS rules,spice models,library & user defined specifications.

**Design Steps** - Circuit Design, Layout Design, Characterization

**Outputs** - CDL(Circuit Description Language),GDSII,LEF,Extracted Spice Netlist(.cir)

**Typical Characterization Flow**

+ Read in the models and tech files
+ Read extracted spice netlist
+ Recognise behaviour of the cell
+ Read the subcircuits
+ Attach power sources
+ Apply stimulus to characterization setup
+ Provide necessary output capacitance loads
+ Provide necessary simulation commands

GUNA is a open software used for characterization.All the above steps are fed into GUNA which generates timing,noise,power.libs,function.
</details>

<details>
 <summary>
  General Timing Characterization Parameters
 </summary>

 **Timing Threshold Definitions**

 ![timingthreshold](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/c606b58c-2aa9-40e8-aada-8d9c992abf23)

 **Propagation Delay** 
 
 Propagation delay is the time required for a signal to propagate through a gate or net.Hence if it is cell, you can call it as “Gate or Cell Delay” or if it is net you can call it as “Net Delay”.Propagation delay of a gate or cell is the time it takes for a signal at the input pin to affect the output signal at output pin.For any gate propagation delay is measured between 50% of input transition to the corresponding 50% of output transition.

 **Transistion Delay**

 Transition delay or slew is defined as the time taken by signal to rise from 10 %( 20%) to the 90 %( 80%) of its maximum value. This is known as “rise time”.Similarly “fall time” can be defined as the time taken by a signal to fall from 90 %( 80%) to the 10 %( 20%) of its maximum value.Transition is the time it takes for the pin to change state.

 ```

Propagation delay = time(out_thr) - time(in_thr)

Rise transition time = time(slew_high_rise_thr) - time (slew_low_rise_thr)

Low transition time = time(slew_high_fall_thr) - time (slew_low_fall_thr)

```
</details>

# Day 3
# Design Library Cell using Magic Layout & Ngspice Characterization

<details>
 <summary>
  CMOS Inverter Ngspice Simulations
 </summary>

 **IO Placer Revision**

 OpenLANE allows users to make changes to environment variables on the fly. For instance, if we wish to change the pin placement from equidistant to some other style of placement we may do the following in the openLANE flow:

 ```

set ::env(FP_IO_MODE) 2

```

**SPICE Deck creation for CMOS Inverter**

SPICE Deck includes the following steps:

+ Component Connectivity
+ Component Values
+ Nodes Identification
+ Naming Nodes
+ Model Description
+ Netlist Description

**SPICE Deck Simulation for CMOS Inverter**

![spice waveform](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/ee68b02e-d674-4f57-a350-64ab244acd20)

**Switching Threshold Vm**

The switching threshold, VM, is defined as the point where Vin = Vout. Its value can be obtained graphically from the intersection of the VTC with the line given by Vin = Vout. In this region, both PMOS and NMOS are always saturated, since VDS = VGS.

![threshold](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/b293ad12-2646-4321-8c92-eac07038cd99)

**Static and Dynamic Simulation of CMOS Inverter**

![static cmos](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/944f03a7-7afc-465c-b2bf-eaf5e9dc29f5)

</details>
<details>
 <summary>
   Inception of Layout A CMOS fabrication process
 </summary>


 # 16-mask CMOS Process

**Selecting a substrate** - Secting the body/substrate material.

 ![step1](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/00f3e5a4-4e3a-47aa-968f-6d9196911e85)

**Creating active regions for Transistors** -  Isolation between active region pockets by SiO2 and Si3N4 deposition followed by photolithography and etching.

![step2](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/3b0b3fb0-d7c4-4b76-a61c-aeaca06b8bf9)

**N-well and P-well formation** - Ion implanation by Boron for P-well and by Phosphorous for N-well formation.

![step3](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/d1a9d532-e55d-403c-8e54-2222f7733624)

**Formation of Gate** - NMOS and PMOS gates formed by photolithography techniques.

![step4](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/c26d6b4a-3e4a-4965-94f4-13063c3cab54)

**Lightly Doped Drain Formation** - LDD formed to prevent hot electron effect.

![step5](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/1a79bbbf-e6fd-467e-a6a1-c9786106bd82)

**Source and Drain Formation** - Screen oxide added to avoid channelling during implants followed by Aresenic implantation and annealing.

![step6](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/8279c48b-2444-497c-ad1f-a9e0cda41f5f)

**Local Interconnect Formation** - Removal of screen oxide by HF etching. Deposition of Ti for low resistant contacts.

![step7](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/300e152d-6954-4c56-8ac2-8251c4e27cf3)

**Higher Level Metal Formation** - CMP for planarization followed by TiN and Tungsten deposition. Top SiN layer for chip protection.

![step8](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/6b8a27f9-7fd9-4da1-9fea-90d4dc7297c3)

</details>

<details>
 <summary>
   Sky130 Tech File Labs
 </summary>

 **Lab steps to git clone vsdstdcelldesign**

The Magic layout of a CMOS inverter will be used so as to intergate the inverter with the picorv32a design. To do this, inverter magic file is sourced from vsdstdcelldesign by cloning it within the OpenLane directory as follows:

```

git clone https://github.com/nickson-jose/vsdstdcelldesign

```

The sky130_inv.mag file can then be invoked in Magic very easily:

```

cd /home/iswarya/OpenLane/vsdstdcelldesign
magic -T /home/iswarya/OpenLane/open_pdks/sky130/sky130A/libs.tech/magic/sky130A.tech sky130_inv.mag & 

```

![vsdstdcell magic](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/e91525ed-ffc6-4f69-bd7a-5a0f42f2fdd1)


**Lab steps to create std cell layout and extract spice netlist**

In tkcon 2.3 Main

```

extract all
ext2spice cthresh 0 rethresh 0
ext2spice

```

![extractall](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/3b18ee5e-fcfd-44c3-bfbc-aec569c0d00f)

```

cd /home/iswarya/OpenLane/vsdstdcelldesign
gvim sky130_inv.spice

```
Edit the Model File:

```

* SPICE3 file created from sky130_inv.ext - technology: sky130A

.include ./libs/pshort.lib
.include ./libs/nshort.lib

.option scale=0.01u

//.subckt sky130_inv A Y VPWR VGND
M1000 Y A VGND VGND nshort_model.0 w=35 l=23
+  ad=1.44n pd=0.152m as=1.37n ps=0.148m
M1001 Y A VPWR VPWR pshort_model.0 w=37 l=23
+  ad=1.44n pd=0.152m as=1.52n ps=0.156m

VDD VPWR 0 3.3V
VSS VGND 0 0V
Va A VGND PULSE(0V 3.3V 0 0.1ns 0.1ns 2ns 4ns)

C0 VPWR Y 0.117f
C1 Y A 0.0754f
C2 VPWR A 0.0774f
C3 Y VGND 0.279f
C4 A VGND 0.45f
C5 VPWR VGND 0.781f
//.ends

.tran 1n 20n
.control
run
.endc
.end



```

To simulate the spice netlist type the following command in the terminal:

```

ngspice sky130_inv.spice

```

To view the Plot Waveform:

```

plot y vs time a

```

![cmos waveform](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/be32632c-59fc-4123-a4c4-9bc57b6d71be)

Characterization of the inverter standard cell depends on Four timing parameters:

Rise Transition: Time taken for the output to rise from 20% to 80% of max value

Fall Transition: Time taken for the output to fall from 80% to 20% of max value

Cell Rise delay: difference in time(50% output rise) to time(50% input fall)

Cell Fall delay: difference in time(50% output fall) to time(50% input rise)

```

Rise Transition : 2.25421 - 2.18636 = 0.006785 ns / 67.85ps
Fall Transition : 4.09605 - 4.05554 = 0.04051ns/40.51ps
Cell Rise Delay : 2.21701 - 2.14989 = 0.06689ns/66.89ps
Cell Fall Delay : 4.07816 - 4.05011 = 0.02805ns/28.05ps

```

**Introduction to Magic tool options and DRC rules**

```

wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
tar xfz drc_tests.tgz
cd drc_tests
magic -d XR met3.mag

```

![magicmet3](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/c89b5f3c-a8b6-48e8-b9f9-295e37d67a4c)

Periphery Rules link - https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html#m3

To figure out the errors use the command **drc why** in tkcon 2.3 main.

Magic uses a lot of derived layers. To see these layers we can make a large box area and use following commands to see metal cut

```

cif see VIA2

```

Load the poly file by **load poly.mag** on tkcon 2.3 main

![load poly mag](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/4e0c78aa-cb0a-4486-a2a8-0d44136bc997)

Edit sky130A.tech

```

gvim sky130A.tech

```
Modify this part of code:

```

spacing npres *nsd 480 touching_illegal \
	"poly.resistor spacing to N-tap < %d (poly.9)"

```

Modify like this:

```

spacing npres allpolynonres 480 touching_illegal \
	"poly.resistor spacing to N-tap < %d (poly.9)"

```

Also,modify this part of code:

```

spacing xhrpoly,uhrpoly,xpc alldiff 480 touching_illegal \
	"xhrpoly/uhrpoly resistor spacing to diffusion < %d (poly.9)"

```

Modify like this:

```

  spacing xhrpoly,uhrpoly,xpc allpolynonres 480 touching_illegal \
       "xhrpoly/uhrpoly resistor spacing to diffusion < %d (poly.9)"

```


In tkcon 2.3 main try this command **drc check**.

**Modified Layout**

![modified layout](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/3d5b60a6-1824-4992-9cae-cffac5bff2b0)

 </details>

 # Day 4
 # Pre-layout timing analysis and importance of good clock tree

<details>
 <summary>
   Timing Modelling using Delay Tables
 </summary>

 **Steps to convert grid info to track info**

 ```

cd home/iswarya/OpenLane/open_pdks/sky130/sky130A/libs.tech/openlane/sky130_fd_sc_hd
gvim tracks.info

```

![gridinfo](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/b1ce1102-ac16-4367-b3d1-0a0418ceff01)

In tkcon 2.3 main add this command

```

 grid 0.46um 0.34um 0.23um 0.17um

```

![modified grid](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/a87e81fc-04af-4931-8054-0a6358b6905c)

**Steps to convert magic layout to std cell LEF**

Select Edit --> Text change the Text String by double clicking 'S' on I/O Ports and select the enable and unselect default

In tkcon 2.3 main define the purpose of each port

```

port A class input
port A use signal

port Y class output
port Y use signal

port VPWR class inout
port VPWR use power

port VGND class inout
port VGND use ground

```
Generate the lef file using below command:

```

lef write sky130_vsdinv

```

In terminal

```
cd home/iswarya//OpenLane/vsdstdcelldesign
gvim sky130_vsdinv.lef

```

![lef file](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/807f4a41-df79-4b02-9d79-3eff647508b0)

**Introduction to timing libs and steps to include new cell in synthesis**

Copy sky130_ishu.lef,sky130_fd_sc_hd__fast.lib, sky130_fd_sc_hd__slow.lib and sky130_fd_sc_hd__typical.lib
files from vsdstdcelldesign folder and paste it in **home/iswarya/OpenLane/designs/picorv32a/src**.

Then edit config.json file

```

{
    "DESIGN_NAME": "picorv32",
    "VERILOG_FILES": "dir::src/picorv32a.v",
    "CLOCK_PORT": "clk",
    "CLOCK_NET": "clk",
    "GLB_RESIZER_TIMING_OPTIMIZATIONS": true,
    "RUN_HEURISTIC_DIODE_INSERTION": true,
    "DIODE_ON_PORTS": "in",
    "GPL_CELL_PADDING": 2,
    "DPL_CELL_PADDING": 2,
    "CLOCK_PERIOD": 24,
    "FP_CORE_UTIL": 35,
    "PL_RANDOM_GLB_PLACEMENT": 1,
    "PL_TARGET_DENSITY": 0.5,
    "FP_SIZING": "relative",
    "LIB_SYNTH":"dir::src/sky130_fd_sc_hd__typical.lib",
    "LIB_FASTEST":"dir::src/sky130_fd_sc_hd__fast.lib",
    "LIB_SLOWEST":"dir::src/sky130_fd_sc_hd__slow.lib",
    "LIB_TYPICAL":"dir::src/sky130_fd_sc_hd__typical.lib",
    "TEST_EXTERNAL_GLOB":"dir::/src/*",
    "SYNTH_DRIVING_CELL":"sky130_vsdinv",
    "MAX_FANOUT_CONSTRAINT": 4,
    "pdk::sky130*": {
        "MAX_FANOUT_CONSTRAINT": 6,
        "scl::sky130_fd_sc_ms": {
            "FP_CORE_UTIL": 30
        }
    }
}

```

In terminal

```

cd home/iswarya/OpenLane/designs/picorv32a/runs/RUN_2023.09.17_06.20.00/logs/synthesis

```

![logsynthessi](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/5bc4e2b1-38b2-49d6-80b3-3d883c696313)

**Introduction to Delay Tables**

 We encounter several types of delays in ASIC design. They are as follows:

+ Gate delay or Intrinsic delay
+ Net delay or Interconnect delay or Wire delay or Extrinsic delay or Flight time
+ Transition or Slew
+ Propagation delay
+ Contamination delay

Wire delays or extrinsic delays are calculated using output drive strength, input capacitance and wire load models. Other delays are intrinsic properties of each and every gate.

Transistors within a gate take a finite time to switch. This means that a change on the input of a gate takes a finite time to cause a change on the output. 

Gate delay =function of (input transition (slew) time, Cnet+Cpin).

or

Gate delay =function of (input transition (slew) time, Cload).

![delay tables](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/b83578a9-7976-4f18-b815-dc5ff527ac51)

 **Steps to configure synthesis settings to fix slack and include vsdinv**

 In OpenLANE Container

 ```

set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
run_synthesis

```

```

  % echo $::env(SYNTH_STRATEGY)
  % set ::env(SYNTH_STRATEGY) "DELAY 0"
  % echo $::env(SYNTH_BUFFERING)
  % echo $::env(SYNTH_SIZING)
  % set ::env(SYNTH_SIZING) 1
  % echo $::env(SYNTH_DRIVING_CELL)

```

 ```

run_floorplan
run_placement

```

In Terminal

```

magic -T /home/iswarya/OpenLane/vsdstdcelldesign/libs/sky130A.tech lef read /home/iswarya/OpenLane/designs/picorv32a/runs/RUN_2023.09.18_15.52.03/tmp/merged.nom.lef def read /home/iswarya/OpenLane/designs/picorv32a/runs/RUN_2023.09.18_15.52.03/results/placement/picorv32.def &

```
 
 </details>

<details>
 <summary>
   Timing Analysis with ideal clocks using OpenSTA
 </summary>

**Setup Timing Analysis**

Setup time is the minimum amount of time the data signal should be held steady before the clock edge so that the data can be reliably sampled. Think of the setup time constraint as a race between the data signal and the clock.

![setup time analysis](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/ed57e250-bca9-4267-a271-1d461a33ff55)

**Clock Jitter**

Jitter is the timing variations of a set of signal edges from their ideal values. Jitters in clock signals are typically caused by noise or other disturbances in the system. Contributing factors include thermal noise, power supply variations, loading conditions, device noise, and interference coupled from nearby circuits.

 Clock jitter is the deviation of a clock edge from its ideal position in time. Simply speaking, it is the inability of a clock source to produce a clock with clean edges. As the clock edge can arrive within a range, the difference between two successive clock edges will determine the instantaneous period for that cycle. So, clock jitter is of importance while talking about timing analysis. There are many causes of jitter including PLL loop noise, power supply ripples, thermal noise, crosstalk between signals etc.

 ![clock jitter](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/25f286e1-e8e3-4f46-83e7-e28e6f4fbf73)

 **Post-Synthesis Timing Analysis using OpenSTA**

 Timing analysis is carried out outside the openLANE flow using OpenSTA tool. Invoke OpenSTA outside the openLANE flow as follows:

 ```

sta pre_sta.conf

```

Copied my_base.sdc file from OpenLane/vsdstdcelldesign/extras into :

```

cd home/iswarya/OpenLane/designs/picorv32a/src/
gvim my_base.sdc

```
![sdcfile](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/a3c1112b-028f-4fc7-a808-4142a28ba981)

</details>
<details>
 <summary>
  Clock tree synthesis TritonCTS and signal Integrity 
 </summary>

 **Clock tree routing and buffering using H-Tree algorithm**

 Clocks are used to synchronize data communication. Before clock tree synthesis, clock path behaves as ideal, where there is equal delay from clock source to sink.
 
The concept of clock tree synthesis (CTS) is the automatic insertion of buffers/inverters along the clock paths of the ASIC design to balance the clock delay to all clock inputs. Basically, clock gets evenly distributed throughout the design across all the sequential elements.

There are number of algorithms to build the clock tree:

+ H Tree
+ Clock Mesh
+ Spine
+ Fish bone

In recent times, in order to compete the clock tree balancing we use H tree algorithm. Let’s go into the details of H Tree algorithm.

**Algorithm steps for the H-Tree**

+ Find out all the flops present.
+ Find out the center of all the flops.
+ Trace clock port to center point.
+ Now divide the core into two parts, trace both the parts and reach to each center.
+ Then from this center, again divide the area into two and again trace till center at both the end.
+ Repeat this algorithm till the time we reach the flop clock pin.

**Crosstalk**

Crosstalk is the unwanted coupling of signals between adjacent wires or devices in a VLSI layout. It can occur due to capacitive, inductive, or resistive effects. Crosstalk can cause signal distortion, delay, or switching errors, especially in high-speed or low-voltage circuits.

Every electrical signal, whether electrical, magnetic, or moving, is connected to a fluctuating field. When these fields intersect, their signals interfere with one another. Crosstalk is caused by electromagnetic interference. If two wires close to each other carry different signals, the currents in them will generate magnetic fields that will induce a lesser signal in the adjoining wire.

Electrical impedance in the return path provides shared impedance coupling between the signals in electrical circuits that share a common signal return channel, resulting in crosstalk.

![crosstalk](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/104dfa53-a078-4de6-b261-e06a6a277b98)

**Clock Net Shielding**

Shielding is required to protect the critical net from the outer environment. Shielding is an effective and very common technique to reduce crosstalk noise as well as delay uncertainty at the cost of the increased routing area. . In the lower technology nodes, Due to capacitive and inductive coupling effects, inserting a shield line is necessary to keep the signal integrity efficiently. 

![clock net shielding](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/ce2b06f1-4aa8-4628-bc3d-41250cbf84b8)

**Lab steps to run CTS using TritonCTS and verify CTS runs**

```

run_cts

```

![run_cts](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/495fb3b9-5111-4e58-9622-5cdd00db7efb)

```

cd home/iswarya/OpenLane/designs/picorv32a/runs/RUN_2023.09.17_13.34.30/logs/synthesis
gvim 2-sta.log

```

![2-stalog](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/fcd09bfc-1ca1-4252-bbf1-d691acf9ac65)

Worst Slack for Setup ---> 13.45

Worst Slack for Hold ---> 0.16

Both the values are positive so there are no timing violations.

</details>
<details>
 <summary>
   Timing analysis with real clocks using openSTA
 </summary>

 **Setup Timing Analysis using Real Clocks**

Setup time is the minimum amount of time before the clock edge that the data input must be stable
 
 ![setup real](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/0053c9a1-62fa-4b34-9e6d-e572535405f8)

 **Hold Time Analysis using Real Clocks**

Hold time is the minimum amount of time after the clock edge that the data input must remain stable

![hold real](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/41406b24-d0fb-4b0e-844c-82806b9bfa5b)

**Timing analysis with real clocks**

From now post cts analysis is performed by operoad within the openlane flow

```

openroad

```

![openroad](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/5c90250b-3373-4963-b624-0c50a20d4555)

```
read_lef /home/iswarya/OpenLane/designs/picorv32a/runs/RUN_2023.09.17_13.34.30/tmp/merged.nom.lef
read_def /home/iswarya/OpenLane/designs/picorv32a/runs/RUN_2023.09.17_13.34.30/results/cts/picorv32.def 
write_db pico_cts.db
read_db pico_cts.db
read_verilog /home/iswarya/OpenLane/designs/picorv32a/runs/RUN_2023.09.17_13.34.30/results/synthesis/picorv32.v
link_design picorv32
read_liberty $::env(LIB_SYNTH_COMPLETE)
read_sdc /home/iswarya/OpenLane/designs/picorv32a/src/my_base.sdc
set_propagated_clock (all_clocks)
report_checks -path_delay min_max -format full_clock_expanded -digits 4

```

**Setup Slack**

![setup slack](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/93199da9-10f1-4889-8cb0-c79d3f9d8445)

**Hold Slack**

![hold slack](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/961772e5-1de7-4e9e-92d9-bb1061e8778b)


</details>

# Day 5
#  Final steps for RTL2GDS using tritonRoute and openSTA

<details>
 <summary>
   Routing and design rule check (DRC)
 </summary>

 **Introduction to Maze Routing and Lee's algorithm**

 Routing is the task of finding a set of connections that will wire together with the terminals of different modules on a printed circuit board or VLSI chip. In the simplest case, these connections are made on a single routing layer of metal. Each connection or net connects a source terminal to a destination terminal.

The Maze Routing algorithm represents the routing layer as a grid, where each gridpoint can contain connections to adjacent gridpoints. It searches for a shortest-path connection between the source and destination nodes of a connection by performing a search and labeling each gridpoint with its distance from the source. This expansion phase will eventually reach the destination node if a connection is possible. A second traceback phase then forms the connection by following any path with decreasing labels. This algorithm is guaranteed to find the shortest path between a source and destination for a given connection. However, when multiple connections are made one connection may block other connections.

Lee’s Algorithm performs a breadth-first search traversal of the grid, starting from the source cell and expanding outward in all possible directions. Each cell is marked with a distance value indicating the number of grid cells traversed to reach that point. This process continues until the destination cell is reached or all possible paths have been explored.

During the traversal, Lee’s Algorithm keeps track of the parent cell for each visited cell, forming a tree-like structure. This information enables efficient backtracking from the destination cell to the source cell, effectively identifying the shortest path. By considering the distances and parent cells, the routing solution obtained through Lee’s Algorithm ensures minimal wirelength and reduced congestion.

![maze](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/2f2dbcc2-37f1-4711-aa17-f68b07017a90)


**Benefits of Lee’s Algorithm**

Lee’s Algorithm brings several advantages to VLSI routing:

+ The algorithm guarantees finding the shortest path between source and destination points efficiently, making it suitable for large-scale integrated circuits.
+ By minimizing the distance between interconnected components, Lee’s Algorithm helps reduce wirelength, leading to improved signal propagation and reduced delays.
+ The algorithm’s adaptability allows designers to incorporate additional constraints, such as avoiding specific areas or optimizing for power consumption, into the routing process.

**Design Rule Check(DRC)**

Design Rule Checking (DRC) verifies as to whether a specific design meets the constraints imposed by the process technology to be used for its manufacturing. DRC checking is an essential part of the physical design flow and ensures the design meets manufacturing requirements and will not result in a chip failure. The process technology rules are provided by process engineers and/or fabrication facility.

**Types of Design Rule Checking**

Each process technology will have its own set of rules. The number of DRC rules and complexity of rules increases as the manufacturing technology shrinks at advanced nodes.

Here are some basic and common types of DRC rules

+ Minimum width
+ Minimum spacing 
+ Minimum area
+ Wide metal jog
+ Misaligned via wire
+ Special notch spacing
+ End of line spacing

</details>

<details>
 <summary>
   Power Distribution Network and routing
 </summary>

 The general ASIC flow, Power Distribution Network generation is not a part of floorplan run in OpenLANE. PDN must be generated after CTS and post-CTS STA analyses:

we can check whether PDN has been created or no by check the current def environment variable:  echo $::env(CURRENT_DEF)

```

gen_pdn
echo $::env(CURRENT_DEF)

```

![PDN](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/2fa3e52c-a832-4187-901d-5809a7e8e1e4)

Log File Generation:

```

cd home/iswarya//OpenLane/designs/picorv32a/runs/RUN_2023.09.17_14.20.42/logs/floorplan
gvim 6-pdn.log

```

![pdnlogfile](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/3a56de9c-fdf1-48ad-9711-b81fc233e117)


 **Routing using Triton Route**

 Detailed routing is a dead-or-alive critical element in design automation tooling for advanced node enablement. However, very few works address detailed routing in the recent open literature, particularly in the context of modern industrial designs and a complete, end-to-end flow. The ISPD-2018 Initial Detailed Routing Contest addressed this gap for modern industrial designs, using a realistic design rules set. In this work, we present TritonRoute, a detailed router capable of delivering a DRC-clean routing solution. The key contributions of TritonRoute include an in-memory router database, along with an end-to-end detailed routing scheme that is capable of comprehending connectivity and design rule constraints, with every key detail revealed by a code release under a permissive open source license. We evaluate our router using the official ISPD-2018 benchmark suite and show that TritonRoute achieves an unprecedented solution quality – improved wirelength and via count, and an extremely low level of design rule violations (DRCs). Compared to the known best detailed routing solutions from all published academic detailed routers, TritonRoute improves wirelength by up to 0.8% (avg. 0.4%), via count by up to 16.1% (avg. 9.3%), and DRCs by up to 100% (avg. 92.0%).

 ![triton route](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/c61462b2-b78e-402f-99d2-cd2ca586a5d4)

 </details>
 <details>
  <summary>
     TritonRoute Features
  </summary>

  **Preprocessed Route Guide**

  ![preprocessed route](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/32afb4e3-3946-4cab-8569-26b2e18a0b7e)

  **Requirements**
  + should have unit width.
  + should be in preferred direction.

**Splitting**

A guide with width (orthogonal to the preferred direction) greater than unit width is split into multiple unit-width guides.

**Merging**

Touching guides (touching edge orthogonal to the preferred routing direction) are merged.

**Bridging**

Touching guides (touching edge parallel to the preferred routing direction) are bridged with additional upper (default) or lower layer guides. After bridging, inter-guide connectivity does not rely on routing topologies with non-preferred direction routing.

**Inter-guide Connectivity**

All unconnected terminals of a net can be traced through connected route guides. Two guides are connected if (i) they are on the same metal layer with touching edges, or (ii) they are on neighboring metal layers with a nonzero vertically overlapped area. Each unconnected terminal (i.e., pin of a standard-cell instance or an IO port) should have its pin shape overlapped by a route guide.

**Intra-Layer Parallel Routing**

Since route guides on the same metal layer are aligned and have unit width, routing realization can be executed in parallel as long as two route guides do not overlap (subject to design rules). We partition each metal layer into nonoverlapping, unit-width panels such that each panel runs parallel to the preferred routing direction. Each route guide is assigned to (exactly) one panel. Routing realization of all route guides within a panel is subject to the limits of shared routing resources, i.e., track availability and various design rules. By contrast, routing realizations in different panels are almost independent, except for design rule constraints, i.e., minimum spacing. Thus, intra-layer routing can be performed in parallel, with respect to panels. In our implementation, for one metal layer, we route all even-index panels in parallel, and then route all odd-index panels in parallel so that design rules violations along panel boundaries can be optimized.

**Inter-Layer Sequential Routing**

We assign routing segments and vias layer by layer, in a sequential manner, from the bottom metal layer to the top layer. Only after we have assigned all routing segments and vias for all panels on layer l, do we proceed to the next (upper) metal layer l+1. 

In our implementation, vias between a lower layer and an upper layer are assigned when we perform the upper-layer panel routing. We handle both intra-guide and inter-guide connectivity in our MILP-based panel routing. Note that in this flow, we do not consider pre-routed power-ground (PG) mesh. Also, since we do not perform iterated inter-panel and interlayer improvements, we currently do not consider routing detours to help achieve DRC convergence.

![inter intra](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/a28c8de5-7061-4175-94be-a0b938fce468)

# Handling Connectivity

**Access Point**

An access point (AP) is an on-grid point on the metal layer of the route guide, and is used to connect to lower-layer segments, upper-layer segments, pins or IO ports. An access point may also contain certain detailed routing segments and vias as needed.

 If access points are used for inter-guide connectivity to lower-layer or upper-layer guides, we generate all on-grid access points within the guides' overlapped area. If access points are used for pins or IO ports, we generate all on-grid access points along the preferred routing direction up to 15 tracks apart. We note that only access points with unique routing patterns in the preferred direction are generated. We discard all access points using non-preferred routing except for pin access. We do not generate off-grid access points in our implementation. However, our flow supports the co-existence of on-grid and off-grid access points, including off-grid routing patterns.

**Access Point Cluster**

An access point cluster (APC) is the union of all access points derived from the same lower-layer segment, upper-layer guide, a pin or an IO port.

**Routing Toping Algorithm**

![algorithm](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/5419d784-1b79-4995-95cd-be6c5fcc2ce4)

**TritonRoute run for routing**

```

run_routing

```

Log File

```

cd home/iswarya//OpenLane/designs/picorv32a/runs/RUN_2023.09.17_14.20.42/logs/routing
gvim  14-resizer_design.log

```

![logfilerouting](https://github.com/IswaryaIlanchezhiyan/Iswarya_Advanced_Physical_Design_Using_OpenLANE-Sky130/assets/140998760/4058f15b-dd5c-42de-a4f1-2e7618be4ca1)


 </details>

 <details>
  <summary>
    VLSI OpenLANE Interactive flow
  </summary>

  ```


cd OpenLane/ 
make mount 

./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis
run_floorplan
run_placement
run_cts
run_routing
run_magic
run_magic_spice_export
run_magic_drc
run_lvs
run_magic_antenna_check

```

 </details>

# References

1. https://www.vsdiat.com
2. https://github.com/Devipriya1921/Physical_Design_Using_OpenLANE_Sky130
3. https://github.com/nickson-jose/vsdstdcelldesign/
4. https://github.com/The-OpenROAD-Project/OpenLane
   

 
 
