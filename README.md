# **FPGA - Fabric, Design, and, Architecture**
This repository contains all the information studied and created during the [FPGA - Fabric, Design, and Architecture](https://www.vlsisystemdesign.com/fpga/) workshop. It is primarily focused on a complete FPGA flow using the maximum open-source tools.
# Table of Contents
<div class="toc">
  <ul>
    <li><a href="#header-1">Day 1 - Exploring FPGA Basics and Vivado</a></li>
	<ul>
        <li><a href="#header-1_1">FPGA (Field Programmable Gate Array)</a></li>
      </ul>
      <ul>
        <li><a href="#header-1_2">Counter Example in Vivado</a></li>
      </ul>
	<ul>
        <li><a href="#header-1_3">VIO - Virtual Input/Output</a></li>
      </ul>
  </ul>
</div>

<div class="toc">
  <ul>
    <li><a href="#header-2">Day 2 - Exploring OpenFPGA, VPR and VTR</a></li>
	<ul>
        <li><a href="#header-2_1">Introduction To OpenFPGA</a></li>
      </ul>
      <ul>
        <li><a href="#header-2_2">VPR(Versatile Place and Route)</a></li>
      </ul>
	<ul>
        <li><a href="#header-2_3">VTR(Verilog to Routing)</a></li>
      </ul>
	 <ul>
        <li><a href="#header-2_4">Example 1 : VPR on a Pre-Synthesized Circuit</a></li>
      </ul>
	 <ul>
        <li><a href="#header-2_5">Example 2 :Run the entire VTR flow automatically</a></li>
      </ul>
	 <ul>
        <li><a href="#header-2_6">Comparision of counnter design from Basys3 and VTR Flow</a></li>
      </ul>
	 </ul>
  </ul>
</div>

<div class="toc">
  <ul>
    <li><a href="#header-3">Day 3 - RISC-V Core Programming Using Vivado</a></li>
	<ul>
        <li><a href="#header-3_1">Behavioral Simulation</a></li>
      </ul>
      <ul>
        <li><a href="#header-3_2">1. Running with ILA(Integrated Logic Analyser)</a></li>
      </ul>
	<ul>
        <li><a href="#header-3_3">2. Running without ILA(Integrated Logic Analyser)</a></li>
      </ul>
  </ul>
</div>

<div class="toc">
  <ul>
    <li><a href="#header-4">Day 4 - Introduction To SOFA FPGA Fabric</a></li>
	<ul>
        <li><a href="#header-4_1">SOFA (Skywater Opensource FPGAs)</a></li>
      </ul>
	  <ul>
        <li><a href="#header-4_2">Running SOFA to design a counter</a></li>
      </ul>
  </ul>
</div>

<div class="toc">
  <ul>
    <li><a href="#header-5">Day 5 - RISCV Core on Custom SOFA Fabric</a></li>
	<ul>
        <li><a href="#header-5_1">Running SOFA to design a RISC-V Core</a></li>
      </ul>
  </ul>
</div>

<div class="toc">
  <ul>
    <li><a href="#header-6">References</a></li>
  </ul>
</div>

<div class="toc">
  <ul>
    <li><a href="#header-7">Acknowledgement</a></li>
  </ul>
</div>

# <h1 id="header-1">Day 1 - Exploring FPGA Basics and Vivado</h1> 
## <h1 id="header-1_1">FPGA (Field Programmable Gate Array)</h1> 
### Introduction to FPGA 
FPGA, or field programmable gate array, is a type of semiconductor logic device that, like PLDs, may be configured to create virtually any system or digital circuit. PLDS can support only a few hundred gates, but FPGAs can accommodate thousands of gates. An ASIC-like language called HDL (Hardware Description Language) is typically used to specify the setting of the FPGA design ( Application Specific Integrated Circuit).
![Screenshot (2178)](https://user-images.githubusercontent.com/120498080/208611881-bd44dbc3-ce2d-47d8-a469-6b193dcde3c6.png)
When compared to ASIC technologies with fixed functions, like conventional cells, FPGAs can offer a variety of benefits. ASICs typically take months to create and cost thousands of dollars to purchase the device. However, FPGAs may be made in less than a second, and they can cost anything from a few dollars to a few thousand. The FPGA's flexibility has a hefty price tag in terms of space, power, and delay. An FPGA uses 20 to 35 times more space than a conventional cell ASIC while performing at speeds that are 3 to 4 times slower. One of the newest areas of VLSI that is trending is FPGAs.
### FPGA Architecture
There are three different types of modules in the typical FPGA architecture. They are 
1. Configurable Logic Blocks (CLB)
2.  Interconnection Wires
3. Switch Matrixes
4. I/O blocks or pads 
They are the fundamental FPGA architecture consists of two-dimensional arrays of logic blocks that can be connected in any order by the user. The following is an overview of an FPGA architecture module's functions:
- The CLB (Configurable Logic Block) has inputs, outputs, and digital logic. It carries out user logic.
- Interconnects give the logic blocks direction so they can apply the user logic.
- Switch matrix offers to switch between interconnects based on the logic.
- I/O pads utilize to connect to various applications from the outside world.
![Screenshot (2176)](https://user-images.githubusercontent.com/120498080/208611382-16d884fd-bda5-4188-9fbb-b79df8038ab1.png)
The MUX (Multiplexer), D flip-flop, and LUT components of a logic block. The MUX is utilized for selection logic, the LUT performs the combinational logical operations, and the D flip-flop stores the LUT's output.
The Look Up Table-based function generator is the fundamental component of the FPGA. Following tests, the LUT can have 3, 4, 6, or even 8 inputs. We now have adaptive LUTs, which use two function generators to implement two outputs from a single LUT.
![Screenshot (2177)](https://user-images.githubusercontent.com/120498080/208611400-3a3ee907-f95e-4949-ba90-f03cf880aa2f.png)
The most well-known FPGA, the Xilinx Virtex-5, has a flip-flop and a look-up table (LUT) that are coupled by MUX. Thousands or hundreds of customizable logic blocks make up the modern FPGA. Modelsim and Xilinx ISE software are used for development and to create a bitstream file for setting the FPGA.
### Basys 3 Artix-7 FPGA Board
The Basys 3 is a basic FPGA development board using the Xilinx® Artix®-7-FPGA architecture that was created specifically for the Vivado® Design Suite. The Basys 3 is the most recent model in the well-liked Basys range of FPGA development boards for novices or students just entering into FPGA technology. The Basys 3 has all of the features that are common to all Basys boards, including fully functional hardware that is ready for use, a sizable selection of onboard I/O devices, all necessary FPGA support circuits, a free version of development tools, and a price point that is affordable for students.
![Screenshot (2175)](https://user-images.githubusercontent.com/120498080/208610017-dc1e8d76-1b4a-46a1-b593-3c33c153aefa.png)

## <h1 id="header-1_2"> Counter Example in Vivado</h1>
A counter is a device that stores (and sometimes displays) the number of times a specific event or process has occurred in digital logic and computing, frequently about a clock. The most typical kind is a sequential digital logic circuit, which has several output lines and a clock-input line. The binary or BCD number system is represented by the values on the output lines as a number. The value in the counter is increased or decreased with each pulse applied to the clock input.
- A 4-bit up counter is being used for exploring the Vivado tool and OpenFPGA. 
- Below mentioned is the RTL for the counter modules that are being used.
- ***NOTE**Linux codes to download GitHub file from link `git clone https://github.com/nandithaec/fpga_workshop_collaterals.git`*
### VERILOG Codes "counter_clk_div.v"
```verilog
module counter(clk,reset,count);
input clk,reset;
output reg [3:0] count = 4'b0000;
reg [25:0] count_reg;
reg clk_div = 1'b0;

always @ (posedge clk)
begin
if (reset)
    begin
        clk_div <= 1'b0;
        count_reg <= 26'd0;
     end
else
    begin
        count_reg <= count_reg + 1;
        if (count_reg == 26'h33) // for synthesis
    //   if (count_reg == 26'd12) // for simulation
        begin
            clk_div <= ~ clk_div;
            count_reg <= 26'd0;
        end
    end
 end
 always @ (posedge clk_div)
 begin
 if (reset)
 begin
    count <= 4'b0000;
 end
 else
 begin
    count <= count + 1;
 end
 end
endmodule
```
### VERILOG testbench "test_counter.v"
```verilog
`timescale 1ns / 1ps

module test_counter();
reg clk, reset;
wire [3:0] out; //create an instance of the design

counter dut(clk, reset, out);  
   initial begin
   //note that these statements are sequential.. execute one after the other 
   //$dumpfile ("count.vcd"); 
   //$dumpvars(0,upcounter_testbench);
	clk=0;  //at time=0
	reset=1;//at time=0
	#20; //delay 20 units
	reset=0; //after 20 units of time, reset becomes 0
   end
   always 
	#5 clk=~clk;  // toggle or negate the clk input every 5 units of time
endmodule 
```
### Behavioral Simulation of the Counter
![Screenshot (2115)](https://user-images.githubusercontent.com/120498080/208306281-42b14bad-2357-4156-9cb7-18f147949796.png)
### RTL ANALYSIS 
#### Elaborate Design of the Counter
It is going to bind a few modules and the modulate hierarchy and it will also establish certain net connectivities.
It is usually done before Synthesis
#### Schematic of the Counter
- To see how the designs are getting mapped.
![Screenshot (2043)](https://user-images.githubusercontent.com/120498080/207792466-697fca77-ced7-4c0f-b1da-4283731ff720.png)
### I/O Planning of the Counter
- It se to obsreve the differnet pins of FPGA
![Screenshot (2044)](https://user-images.githubusercontent.com/120498080/207792629-8a565a89-b586-48dc-9be4-0dd4756585db.png)
### Mapping I/O Ports to the pins of the FPGA
- As I do not have access to the FPGA board so I am using the schematic of basis 3 and mapping the pins accordingly
#### Schematic of Basys3 Board
[SCHEMATIC PDF](https://digilent.com/reference/_media/reference/programmable-logic/basys-3/basys-3_sch.pdf)
![Screenshot (2046)](https://user-images.githubusercontent.com/120498080/207820032-b6efb987-a4ae-45eb-af8a-756cf998eaf4.png)
#### Mapping in constraints.edx file 
- I set Vcc as 3.3V (I/O Std - LVCMOS33) for all input and output pins. 
- Then by setting the inputs and outputs I generated the `constraints. edx` file
- Providing the clovk frequency of 100MHz (period of 10nsec).
![Screenshot (2172)](https://user-images.githubusercontent.com/120498080/208490548-82b91717-2562-458c-b1f6-286b71ac4b67.png)
### Introduction to Slack 
- **Slack** is the difference between achieved or actual time and the desired time for a timing path.  The amount of timing path slack tells us whether the design operates at the desired speed or frequency.
![Screenshot (2174)](https://user-images.githubusercontent.com/120498080/208606261-344b03cc-e153-46ad-b017-233a816e2c72.png)
Tcq = Time Delay to reach the data from D to A
Tlogic = Time required to reach the data from A to B
- **Setup Time** The amount of time needed for the input to a flip-flop to be steady before a clock edge is known as setup time.
- **Hold Time** The hold time is the shortest period necessary for the input to a flip-flop to remain steady following a clock edge.
- **Data Arrival Time** This is the amount of time needed for data to go through the data path.(Tcq + Tlogic)
- **Data Required Time** This is the amount of time needed for the clock to go through the clock path. (T - Tsetup)
- Setup and hold slack is the difference between data required time and data arrival time.

**Setup Slack = Data Required Time - Data Arrival Time**
**Hold Slack= Data Arrival Time- Data Required Time**

- A positive setup slack indicates that the design is operating at the desired frequency and also has some additional margin.
- Zero setup slack indicates that there is no buffer available and that the design is precisely operating at the intended frequency.
- Negative setup Slack indicates that the restricted frequency and time are not met by the design. This is called a setup violation.
### SYNTHESIS & IMPLEMENTATION
- Clock frequency is 100MHz (from Constraints Wizard)
#### Report Timing Summary of the Counter
![Screenshot (2068)](https://user-images.githubusercontent.com/120498080/207813932-5b9ffb95-2197-4598-a2ae-e8f5f9a9e220.png)
#### Set of Paths of Timing Report  of the Counter
![Screenshot (2073)](https://user-images.githubusercontent.com/120498080/207833329-2a05d4fc-fcd4-4984-b865-ecf12f37cce0.png)
#### Path report if Path1 in Paths Timing Report of the Counter
![Screenshot (2074)](https://user-images.githubusercontent.com/120498080/207833693-368619f4-b532-4f29-a548-1e18c5a0f546.png)
![Screenshot (2075)](https://user-images.githubusercontent.com/120498080/207834358-a9078258-db6d-4ff8-9b60-e7fadf99afa4.png)
![Screenshot (2076)](https://user-images.githubusercontent.com/120498080/207834391-bacc2dda-c8e7-478a-a2e8-cc4ddb944bcc.png)
 #### Circut of the Counter 
- It shows the synthesized netlist of the schematic
![Screenshot (2069)](https://user-images.githubusercontent.com/120498080/207824737-cfb319d1-aaba-44fe-9699-2e830f28b627.png)
#### Power Report of the Counter
![Screenshot (2070)](https://user-images.githubusercontent.com/120498080/207825343-2fa69e41-a876-4a59-8982-9898858ec658.png)
#### Report Utilization of the Counter
- It tells about the area report.
- e.g - it shows us how many resources have been utilized in the FPGA
![Screenshot (2071)](https://user-images.githubusercontent.com/120498080/207827717-1e2d4d97-c7d2-49d3-8d4b-9eeea1413900.png)
### PROGRAM AND DEBUG
#### Generate Bitstream of the Counter
- Here I locally connected the FPGA Basis3 board to our pc, programmed the board, and test the output by adjusting the reset switch (as I was not having access to the Basys3 board so I am not doing it here)
### Alternative way is Post Implementation Timing Simulation
**NOTE**
- **Run Behavioral Simulation** It just takes the original design (the written .v file Verilog codes) and runs the testbench on it to give the output.
- **Run Post Implementation Timing Simulation** It is creating a Post Implementation Simulation netlist (e.g. - it is completing the synthesis and implementation) and then it is running the testbench in that netlist which is closest to running in an FPGA.
#### POST-IMPLEMENTATION TIMING SIMULATION
- This simulation output waveform should match the Behavioral Simulation output waveform.
![Screenshot (2114)](https://user-images.githubusercontent.com/120498080/208306396-6639e787-08aa-4695-be2d-d27e47f8ec8f.png)

## <h1 id="header-1_3"> VIO - Virtual Input/Output </h1>
- VIO is an IP that comes along with vivado (inbuild into vivado), so when this interface is virtually connected to my design (counter) then I can virtually provide the input (rest) through this VIO and observe the outputs (out and div_clk) 
- So this needs some changes in the codes: I have created an instance of the VIO 
1. "reset" will be output from VIO which is given as input to the counter.
2. "counter_out" and "div_clk" will be input to VIO which is taken from the output of counter
### VIO Block Diagram
![Screenshot (2125)](https://user-images.githubusercontent.com/120498080/208318452-00b8e63e-20ab-46c9-be3f-61ed70be2bc4.png)
### Opening VIO in vivado
- For that go to IP Catalog/VIO
- In that set  "Input Probes Cout = 2" (because I am having 2 inputs ) and "Output Probes Cout = 1" (because I am having 1 output(reset))
- In next tab "PROBE_IN Ports" and set "PROBE_IN0 = 1" (because div_clk is a 1 bit signal) and "PROBE_IN1 = 4" (because counter_out is a 1 bit signal)
- In the next tab "PROBE_OUT Ports" set "PROBE_OUT0 = 1" (because reset is a 1-bit signal
- Then confirm and generate.
#### Generated VIO
![Screenshot (2127)](https://user-images.githubusercontent.com/120498080/208319739-db6700a8-f480-4443-a113-efd717abc7a9.png)
- Then use the codes 'counter_clk_div_vio.v` and go for Simulation >>Elaboration >> Syntheses >> Implemantation >> Bitstream Generation and set clk as W5.
- Then after connecting the Basys3 FPGA board go to Open Hardware Manager and observe the outputs.





# <h1 id="header-2">Day 2 - Exploring OpenFPGA, VPR and VTR</h1> 
## <h1 id="header-2_1">Introduction To OpenFPGA</h1>
An open-source platform called OpenFPGA seeks to make it possible to quickly prototype adaptable FPGA systems. The below figure illustrates how a traditional approach would require a big team of seasoned engineers for more than a year to complete a production-ready layout and related CAD tools. In actuality, the majority of engineering efforts are put into creating manual layouts and ad-hoc CAD support.
![Screenshot (2179)](https://user-images.githubusercontent.com/120498080/208620681-ce83bf1a-385b-41d4-887c-e09430eafed5.png)
The development process for both hardware and software can be greatly sped up with OpenFPGA. Based on an XML-based description file, OpenFPGA can automatically produce Verilog netlists describing an entire FPGA fabric. Within 24 hours, production-ready layout generation can be accomplished with the help of contemporary semi-custom design technologies. With the use of contemporary verification tools, OpenFPGA can automatically construct Verilog test benches to verify the accuracy of FPGA fabric. To avoid repeating engineering while creating CAD tools for several FPGAs, OpenFPGA also offers native bitstream generating capability based on the same XML-based description file used in Verilog generation. The CAD tool is available for usage as soon as the FPGA architecture is complete.

OpenFPGA opens up a wide design area for developing customizable FPGAs because it can support any architecture that VPR can describe. This includes the majority of architectural modifications present in contemporary FPGAs. In addition, OpenFPGA has improved syntax that enables users to alter transistor-level parameters in simple circuits. This makes it easier for developers to best tailor the P.P.A. (Power, Performance, and Area). A small number of young engineers or researchers now have access to adaptable FPGAs for prototype and study thanks to all these advantages.

The following components make up OpenFPGA's tool functionality: FPGA-Verilog, FPGA-SDC, FPGA-Bitstream, and FPGA-SPICE. The remainder of this section will center on the specific reasons for each of them, as seen in the image below.
![Screenshot (2180)](https://user-images.githubusercontent.com/120498080/208624329-5e0816e9-06fd-4602-856a-9b022c637f7c.png)

- [Opne FPGA and VTR Installation Guide](https://drive.google.com/file/d/1BbyCDvzvidx22hTT6BOYbCEFAXNhKalH/view?usp=sharing)


## <h1 id="header-2_2">VPR(Versatile Place and Route) </h1>
The last part of VTR is versatile place and route (VPR). A BLIF circuit serves as its input, and it packs, puts, and routes the circuit on an input FPGA design.'

During packing, adjacent and connected logic components of the circuit are grouped into Logic Blocks that match the FPGA's hardware. These logic blocks and hard blocks are assigned to the FPGA's available hardware resources during placement. Finally, signal connections between blocks are formed during routing. Many other universities and businesses have contributed to the development of VPR, which is principally being done by the University of Toronto.
- [VPR Reference](https://docs.verilogtorouting.org/en/latest/vpr/)
#### VPR Flow
![Screenshot (2078)](https://user-images.githubusercontent.com/120498080/208228994-29779770-a2ac-4f8e-882c-0333beaf97a9.png)


## <h1 id="header-2_3">VTR(Verilog to Routing)</h1>
The Verilog to Routing (VTR) project offers free and open-source CAD tools for studying FPGA architecture.
In contrast to closed-source tools, open-source CAD tools allow for the investigation of novel FPGA architectures and CAD algorithms.
A Verilog description of a digital circuit and information about the intended FPGA architecture are input into the VTR design flow. Next, it performs:
- ODIN II -  Elaboration & Synthesis 
- ABC - Logic Optimization & Technology Mapping 
- VPR - Packing, Placement, Routing & Timing Analysis 

to generate FPGA area and speed data. The data necessary for bitstream synthesis to target actual FPGA devices can also be produced via VTR.
The benchmark designs included in VTR are ideal for evaluating FPGA architectures and are adaptable and can accommodate a variety of hypothetical, commercial-like, and practical FPGA architectures.
- [VTR Reference](https://docs.verilogtorouting.org/en/latest/quickstart/)
#### VTR Flow
![Screenshot (2077)](https://user-images.githubusercontent.com/120498080/208229019-3d36e223-5d2e-4410-927c-3ecb3ff7f7ec.png)


## <h1 id="header-2_4">Example 1 : VPR on a Pre-Synthesized Circuit</h1>
### Input to this VPR is:
1. Technology mapped netlist of a Design (in form of **`tseng.blif`** file)
2. FPGA Architecture description file (in form of **`Earch.xml`** format)
- **NOTE** This EArch.xml is already available (nearly 40 different FPGA Architectures available) available (For  our FPGA achitecture it can be written using XML language) 
- **NOTE** This tseng.blif is generated from Tech Mapped Netlist and it contains information about the technology Tech Mapped circuits (for eg if we are targeting a 40nm circuit) which will be implemented in the target FPGA and used as an input file to VPR flow.
### VPR tool will go through the following steps. 
#### 1. VPR Packing 
- It is going to combine all the primitive netlist blocks(e.g. - all the LUTs,FF,etc which are the part of the design) 
- These are going to be packed in CLB(Complex Logic Blocks).
- The output of this is a `.net` file
#### 2. VPR Placement 
- The CLBs will get placed in the FPGA Grid.
- The output of this is a `.place` file, which is going to contain the locations of where these CLBs are placed. 
#### 3. VPR Route
- It is going to connect all of these CLBs to the FPGA grid.
- The output of this is a `.route` file, which is going to contain all the route information.
#### 4. VPR Analysis
- It analyzes in terms of Area, Timing, and Power.
- It is also going to output a Post-Implementation Netlist( it will give information about resource usage, number of block pipes and wires used, timing in terms of critical path delay and timing path and also power usage by each of these blocks)

- Location of blif file in server : 
> /home/kunalg123/Desktop/vtr-verilog-to-routing/vtr_flow/benchmarks/blif/tseng.blif
  
- Location of Earch.xml file in server :
>/home/kunalg123/Desktop/vtr-verilog-to-routing/vtr_flow/arch/timing/Earch.xml

#### Example `.xml` file explanation :
![Screenshot (2080)](https://user-images.githubusercontent.com/120498080/207940470-314389f2-05d8-4886-84b3-074b9638554b.png)

- ***NOTE** Command to open the above blif and Earch.xml location `cd $VTR_ROOT` (after that use `cd` and `ls` to go into a particular location and open the file)* 
***NOTE**
-  *Steps to make a new working directory in Linux
#### *Move to our home directory
> cd ~
#### *Make a working directory
> mkdir -p vtr_work/quickstart/vpr_tseng
#### *Move into the working directory
> cd ~/vtr_work/quickstart/vpr_tseng*

#### Working Location :
>is22mtech14002@fpga-workshop-02:~/vtr_work/quickstart/vpr_tseng$
### Running VTR
#### Command to run VPR
- Use these commands in the working location to run VPR.
```
$VTR_ROOT/vpr/vpr $VTR_ROOT/vtr_flow/arch/timing/EArch.xml $VTR_ROOT/vtr_flow/benchmarks/blif/tseng.blif --route_chan_width 100 --disp on
```
```
$VTR_ROOT/vpr/vpr\                             // invoking vpr which is at VTR_ROOT (where vtr has been installed in the cloud)                                       
$VTR_ROOT/vtr_flow/arch/timing/EArch.xml\      // First input is FPGA Architecture Description File (EArch.xml)
$VTR_ROOT/vtr_flow/benchmarks/blif/tseng.blf\
-- route_chan_width 100 \                      // use a benchmark file that is already being converter into blf format
-- disp on                                     // to open GUI
```

#### GUI - Graphical User Interface
![Screenshot (2081)](https://user-images.githubusercontent.com/120498080/207940492-b3c8ddb5-da7d-4026-86e0-b2f7bba9bce7.png)
#### Structure of FPGA Architecture
![Screenshot (2088)](https://user-images.githubusercontent.com/120498080/208081790-279b1699-d010-4a70-a94f-295040f1519a.png)
#### Congestion Architecture 
- It shows which area is how much Congested.
![Screenshot (2089)](https://user-images.githubusercontent.com/120498080/208081834-0f92663a-bc7e-4757-86eb-24f96f55c9a5.png)
- There are also different views available of this FPGA Architecture which can be accessed through GUI

- Finally, the output of this VPR step is 
1. **tseng.net** It's a packed netlist format, it's an xml file that describes post packed circuit. So it represents the user netlist in terms of complex logic blocks of this particular architecture. 
2. **tseng.place** It's the output of the Placement step. It is going to list the netlist and tells about the different block number and their placement in the Architecture.
3. **tseng.route** It's the output of the Routing step which going to contain information about the net and the nodes which are going to connect.
4. **tseng.log** It's basically what it printed out in the terminal.
- All the files are generated in the same working directory `/home/kunalg123/Desktop/vtr-verilog-to-routing/`
- It will also generate `report_timing.setup.rpt` , `report_timing.hold.rpt`, `packing_pin_util.rpt`, etc files. in the same working directory.

- ***NOTE** Command to search .rpt file in working directory `ls *.rpt`*
### Running VTR with added clock
To run VTR with the clock I needed to define `tseng.sdc` and invoke it in the VTR command
#### `tseng.sdc` file
- To get the correct timing report I need to  set the clock and for that, I need to set the constraints file (`tseng.sdc file`)
```
create_clock -period 10 -name pclk     
set_input_delay -clock pclk -max 0 [get_ports {*}]  
set_output_delay -clock pclk -max 0 [get_ports {*}]  
```
```
create_clock -period 10 -name pclk                    //Created a clock with the period of 10nsec with name plck (I can find it from the timing report)
set_input_delay -clock pclk -max 0 [get_ports {*}]    //Set input delay to zero
set_output_delay -clock pclk -max 0 [get_ports ("}]   //Set output delay to zero
```
### Steps to add this clock to the Design
- First, go back to the same working directory and append the sdc option.
```
$VTR_ROOT/vpr/vpr $VTR_ROOT/vtr_flow/arch/timing/EArch.xml $VTR_ROOT/vtr_flow/benchmarks/blif/tseng.blif --route_chan_width 100 --sdc_file /home/is22mtech14002/LAB1/tseng.sdc  
```
[Reference for VPR Command Line Options](https://docs.verilogtorouting.org/en/latest/vpr/command_line_usage/)
- Finally, it will generate several reports:
1. `report_timing.setup.rpt`
2. `report_timing.hold.rpt`
3. `report_unconstrained_timing.hold.rpt`
4. `report_unconstrained_timing.setup.rpt`
5. `packing_pin_util.rpt`
#### Setup Slack Path
![Screenshot (2087)](https://user-images.githubusercontent.com/120498080/208078972-dc84eab8-f2e4-45bd-b51f-cafacb8b42fc.png)
- Finally, I got a Setup Slack Path of 8.507nsec



## <h1 id="header-2_5">Example 2 :Run the entire VTR flow automatically</h1>
- In the VTR flow we will start with HDL going through Odin II then ABC then finally the VPR flow (as done in example 1)
- There are two ways of running VTR :
1. **Manually Running the VTR Flow**
- We have to invoke Odin II manually
- Then we have to do the technology mapping with ABC
- Then manually implement the circuit using VPR
2. **Automatically Running the VTR Flow**
- In Automatically Running the VTR Flow instead of invoking Odin II and ABC I used some existing files and VPR with the help of these files.
### Automatically Running VTR
- To Automatically Run the VTR Flow
I will be invoking the python script present at 
>$VTR_ROOT/vtr_flow/scripts/run_vtr_flow.py
- **NOTE** This `run_vtr_flow.py file` is already available for this Open FPGA (for our simplicity) if we are Automatically Running the VTR Flow.
- **NOTE** This `EArch.xml` is already available (nearly 40 different FPGA Architectures available) available (For  our FPGA architecture it can be written using xml language) 
#### Codes to run VTR tool
```
$VTR_ROOT/vtr_flow/scripts/run_vtr_flow.py     /home/is22mtech14002/Desktop/fpga_workshop_collaterals/Day2/counter_files/counter.v   $VTR_ROOT/vtr_flow/arch/timing/EArch.xml   -temp_dir .  --route_chan_width 100
```
- Then run the commands in the working directory to generate `.blif` file 
```
 $VTR_ROOT/vtr_flow/scripts/run_vtr_flow.py \         //Invoicing Python script .py
    $VTR_ROOT/doc/src/quickstart/counter.v \          //Inputs the counter.v file
    $VTR_ROOT/vtr_flow/arch/timing/EArch.xml \        //Architecture onto which we want to map the counter.v file
    -temp_dir . \                                     //Local Working Directory
    --route_chan_width 100                            // Routing Channel width for the Architecture
```
#### Codes of the counter.v file
```verilog
module up_counter    (
out,  // Output of the counter
enable  ,  // enable for counter
clk     ,  // clock Input
reset      // reset Input
);

output [3:0] out;  //we can alternately write this as output reg [7:0] out;
input enable, clk, reset; //------------Internal Variables--------
reg [3:0] out; 

always @(posedge clk)
  if (reset) begin //reset ==1
    out = 4'b0 ;
  end 
  else if (enable) begin //reset =0
    out = out + 1;
  end
endmodule 
```
- Commands to invoke GUI analysis step
```
$VTR_ROOT/vpr/vpr $VTR_ROOT/vtr_flow/arch/timing/EArch.xml  /home/is22mtech14002/vtr_work/quickstart/vpr_tseng/counter.pre-vpr.blif  --route_chan_width 100 --analysis --disp on
```
--analysis      // to run GUI from analysis step onwards
- Commands to invoke GUI with the entire VPR flow
```
$VTR_ROOT/vpr/vpr $VTR_ROOT/vtr_flow/arch/timing/EArch.xml  /home/is22mtech14002/vtr_work/quickstart/vpr_tseng/counter.pre-vpr.blif  --route_chan_width 100 --disp on
```

### GUI (Graphical User Interface) of the Design
![Screenshot (2090)](https://user-images.githubusercontent.com/120498080/208226847-1cfb86ed-e9fa-42fd-9afc-f4fdce2b5814.png)
- So now it will complete the entire VPR flow

### Generation of the Post-Implementation Netlist of the Design
- Now I need to generate a Post-Implementation Netlist from VPR
[Generation of the Post-Implementation Netlist](https://docs.verilogtorouting.org/en/latest/tutorials/timing_simulation/)

```
$VTR_ROOT/vpr/vpr $VTR_ROOT/vtr_flow/arch/timing/EArch.xml  /home/is22mtech14002/vtr_work/quickstart/vpr_tseng/counter.pre-vpr.blif  --route_chan_width 100 --gen_post_synthesis_netlist on
```
```
$VTR_ROOT/vpr/vpr $VTR_ROOT/vtr_flow/arch/timing/EArch.xml                   //Run VPR with the Architecture file (.xml file)
/home/is22mtech14002/vtr_work/quickstart/vpr_tseng/counter.pre-vpr.blif      //Run the .blif file that has been created from the VPR
--route_chan_width 100 
--gen_post_synthesis_netlist on                                              //to generate post-synthesis netlist
```
- So now VPR will generate the  Post-Implementation Netlist (`up_counter_post_synthesis.v` file) and also the delay file (`up_counter_post_synthesis.sdf`) file

- ***NOTE** Linux Command to check `up_counter_post_synthesis.sdf` and `up_counter_post_synthesis.v` file has been generated `ls *.v *.sdf`

#### Location the files
> /home/kunalg123/Desktop/vtr-verilog-to-routing/vtr_flow/primitives.v
> /home/is22mtech14002/vtr_work/quickstart/vpr_tseng/up_counter_post_synthesis.blif
> /home/is22mtech14002/vtr_work/quickstart/vpr_tseng/up_counter_post_synthesis.sdf
> /home/is22mtech14002/vtr_work/quickstart/vpr_tseng/up_counter_post_synthesis.v

- **NOTE** This `privitive.v` file is specific for a particular FPGA board and it is available in FPGA fabric (sometimes it has constraints which I need to fix, like clock written as clk which should match with our up_counter_post_synthesis.v file)

### Post-Implementation Simulation in Vivado of the Design
- Now create a project in VIVADO and add `primitives.v` and `up_counter_post_synthesis.v` as design sources and `upcounter_testbench.v` as simulation sources and run the simulation.
- **NOTE** In the generated `up_counter_post_synthesis.v` file have values assigned to cout and sumout as don't care **`cout(1'bX)`** and **sumout(1'bX)** which shows an error in vivado simulator so it needs to not assign any values as **`cout()`** and **sumout()**
#### Vivado error of generated `up_counter_post_synthesis.v`
![image (2)](https://user-images.githubusercontent.com/120498080/208493016-a17c34db-0aef-457e-97f1-59d9c65bedcb.png)
- **NOTE** But due to some errors it was giving don't care in the output if I where using generated `up_counter_post_synthesis.v` and provided `upcounter_testbench.v` and `primitives.v`in git repo.
#### Comparison report of generated `up_counter_post_synthesis.v` and provided `up_counter_post_synthesis.v`
![Screenshot (2160)](https://user-images.githubusercontent.com/120498080/208436679-41fded33-2069-4c97-b24e-e9f8251c50fb.png)
- But this mismatch can't be the reason for getting don't cares in the output.
- According to me there must be some disconnection in the nodes of the generated Verilog codes in generated `up_counter_post_synthesis.v`
#### Behavioural Simulation of the generated `up_counter_post_synthesis.v`
![Screenshot (2161)](https://user-images.githubusercontent.com/120498080/208437905-24ecd678-6165-471e-be24-4176a42de94d.png)
- So I used the provided `up_counter_post_synthesis.v` file and proceed further.
#### Behavioural Simulation of the provided `up_counter_post_synthesis.v`
![Screenshot (2162)](https://user-images.githubusercontent.com/120498080/208438709-58782213-34a0-41ea-b25b-f5e37b6bc3ae.png)
- **NOTE** It does not matter what FPGA we choose initially in the VIVADO tool because we are not going to run an FPGA simulation, the up_counter_post_synthesis.v file is specific to an open FPGA Architecture and Xilinx's particular architecture, but we are going to use the Xilinx tools only particularly for simulation purposes and for synthesis and simulation, and so on. 


### Area Analysis in VTR of the Design
- The `vpr_stdout.log file` generate in the Dump file location contain information about the Utilization Report(Area Report) of our Design. 
#### Output of Area Analysis
![Screenshot (2164)](https://user-images.githubusercontent.com/120498080/208465505-b6a85e2c-f537-4312-b723-1f2cb4a585bb.png)

### Timing Analysis in VTR of the Design
- To do timing analysis using VTR I created a `counter.sdc` file whose clock name `up_counter_clk` should be the same as the clock name in `counter.pre-vpr.blif` file
- In `counter.pre-vpr.blif` replace up_counter^clk with up_counter_clk
```
create_clock -period 10 up_counter_clk
set_input_delay -clock up_counter_clk -max 0 [get_ports {*}]
set_output_delay -clock up_counter_clk -max 0 [get_ports {*}]
```
- Then run the timing analysis which will create the report in the working directory.

#### Commands to run Timing Analysis in VTR
```
$VTR_ROOT/vpr/vpr $VTR_ROOT/vtr_flow/arch/timing/EArch.xml  /home/is22mtech14002/vtr_work/quickstart/vpr_tseng/counter.pre-vpr.blif  --route_chan_width 100 --sdc_file /home/is22mtech14002/Desktop/counter.sdc
```
#### Output of Timing Analysis
![Screenshot (2170)](https://user-images.githubusercontent.com/120498080/208470305-4ea394b9-4e1a-488d-8fc3-38f4edadc666.png)
![Screenshot (2171)](https://user-images.githubusercontent.com/120498080/208470776-2309ae2e-4500-46e2-92b3-a69c49b76873.png)


### Power Analysis in VTR of the Design
- Then I do Power Analysis in VTR and I used the following commands.
[Reference for Power Analysis](docs.verilogtorouting.org/en/latest/vtr/power_estimation/#running-vtr-with-power-estimation) 

```
$VTR_ROOT/vtr_flow/scripts/run_vtr_flow.py     /home/is22mtech14002/Desktop/fpga_workshop_collaterals/Day2/counter_files/counter.v   $VTR_ROOT/vtr_flow/arch/timing/EArch.xml  -power -cmos_tech /home/kunalg123/Desktop/vtr-verilog-to-routing/vtr_flow/tech/PTM_45nm/45nm.xml -temp_dir .  --route_chan_width 100
```
```
-power                                                                                         // to have the power estimation 
-cmos_tech /home/kunalg123/Desktop/vtr-verilog-to-routing/vtr_flow/tech/PTM_45nm/45nm.xml    //passes cmos technology file available while downloading VTR
```
- This will generate the 'counter.power` file in the working directory.

#### Output of Power Analysis
![Screenshot (2167)](https://user-images.githubusercontent.com/120498080/208471755-803825a8-1e10-43eb-aec6-db124452e25d.png)

## <h1 id="header-2_6">Comparision of counnter design from Basys3 and VTR Flow</h1>
### Timing Comparision
- I have used a clock frequency of 100MHz (Period = 10nsec)

| Parameters | Counter from Basys3 | Counter from VTR Flow |
|:----------:|:-------------------:|:---------------------:|
| Technology | 28nm                |  40nm                 |
|Worst Setup Slack|5.989nsec|9.0976nsec|
|Worst Hold Slack|0.117nsec|0.293nsec|

### Area Comparision

| Parameters | Counter from Basys3 | Counter from VTR Flow |
|:----------:|:-------------------:|:---------------------:|
| LUTs | 23|18|
|I/Os|6|7|
|FF|31|4|

### Power Comparision

| Parameters | Counter from Basys3 | Counter from VTR Flow |
|:----------:|:-------------------:|:---------------------:|
| Power | 84mWatt|0.3212mWatt|













# <h1 id="header-3">Day 3 - RISC-V Core Programming Using Vivado</h1> 

Here I used the verilog code of the RISC-V processor core called RVMyth (mythcore_test_no_ILA.v)(ILA - Integrated Logic Analyser, I used no_ILA one because I am not using practical FPGA board). It has a 5-stage pipelined processor which is going to add the first 9 numbers.
Then I created a vivado project by adding basys3(xc7a35tcpg238-1) board and I added mythcore_test_no_ILA.v as the destination source and test.v as the simulation source and then perform the vivado simulations.

## <h1 id="header-3_1">Behavioral Simulation</h1> 
![Screenshot (2091)](https://user-images.githubusercontent.com/120498080/208234103-a18b8b86-aad0-4901-ab6e-8ce94ca0bfc0.png)

## RTL ANALYSIS
## <h1 id="header-3_2">1. Running with ILA(Integrated Logic Analyser)</h1> 
After running Elaboration I set I/O Std as LVCMOS33 and clk to W5 and reset to R2 for the output port I am going to assign an ILA (Integrated Logic Analyser) to view the output (because I am not using practical FPGA board). Fo that I made some changes to the codes
> Replace `module core(input clk, input reset, output [7,0]out);` with `module core(input clk, input reset);` so I do not need to map the outputs to any LEDs
- Then again run the Elaboration (Do not do the behavioral simulation at this point, otherwise it will show a mismatch in the number of ports because I have eliminated the output port here, as the testbench contain the output port) 
-  So I have gone with **Elaboration >> Syntheses >> Implementation >> Bitstream**
#### Running ILA in Vivado
- I added ILA to probe the signals
- For that go to IP Catalog/ILA(Integrated Logic Analyser)
- In that set Number of Probes = 2 (because I wanted to check reset and output)
- In the next tab "Probe Ports" set PROBE0|Probe With = 1 (because reset is a 1-bit signal) and PROBE1|Probe With = 8 (because the output is a 8-bit signal)
- Then confirm and generate.
#### Generated ILA(Integrated Logic Analyser)
![Screenshot (2095)](https://user-images.githubusercontent.com/120498080/208235941-000dff30-d315-4349-a0e7-7d723e07d7f4.png)
- Then copy this and paste it into our codes
```verilog
ila_0 your_instance_name (
	.clk(clk), // input wire clk
	.probe0(reset), // input wire [0:0]  probe0  
	.probe1(out) // input wire [7:0]  probe1
);
```
![Screenshot (2096)](https://user-images.githubusercontent.com/120498080/208236104-2e9b6322-6692-4e5a-bd05-a27c1626549c.png)
 - Finally, run the synthesis and set the clock as 100MHz Constrains Wizard.
#### Constrains File
 ![Screenshot (2104)](https://user-images.githubusercontent.com/120498080/208252230-e09a8c3d-4792-425a-8819-77c2ce7e410e.png)
### SYNTHESIS and IMPLEMENTATION 

#### Utilization Report
![Screenshot (2098)](https://user-images.githubusercontent.com/120498080/208238191-99e41f5a-e8b7-4aa1-b864-2b8db9084174.png)
#### Schematic of the Architecture 
![Screenshot (2099)](https://user-images.githubusercontent.com/120498080/208238125-ec9e3bc0-bf5e-4c63-9663-ebb93110e4b6.png)
#### Floarplanning of Implemented Design 
![Screenshot (2103)](https://user-images.githubusercontent.com/120498080/208252100-e2d57600-2e73-423b-bac6-509bf56b1a5a.png)
#### Report Timing Summary
![Screenshot (2100)](https://user-images.githubusercontent.com/120498080/208252113-b7869a24-82aa-44db-930b-d151173d6d1e.png)
#### Power Report
![Screenshot (2105)](https://user-images.githubusercontent.com/120498080/208252633-0f729d19-de3a-46f3-b922-ef13db969ae1.png)
- Then I proceed for Bitstream Generation if I have the FPGA Basys3 Board. 
## <h1 id="header-3_3">2. Running without ILA(Integrated Logic Analyser)</h1> 
I create a project in vivado and I added `mythcore_test_no_ILA.v` as the destination source and `test.v` as the simulation source and then perform **Simulation>>Elaboration >> Syntheses >> Implementation>> Bitstream**. and set constraints as shown below. For pin selection, I referred to [Schematic of Basys3 Board](https://digilent.com/reference/_media/reference/programmable-logic/basys-3/basys-3_sch.pdf)
#### Constrains File
![Screenshot (2108)](https://user-images.githubusercontent.com/120498080/208255165-9b0db85a-5aba-4444-856b-27b6209a2e3e.png)
- Finally, go running and run the Post Implementation Timing Simulation and it will give the same output as before.
#### Post Implementation Timing Simulation
- This simulation output waveform should match the Behavioral Simulation output waveform.
![Screenshot (2107)](https://user-images.githubusercontent.com/120498080/208255251-dbd75711-772e-4476-9f44-7c2eff15a031.png)
**NOTE**
- **Run Behavioral Simulation** It just takes the original design (the written .v file/verilog codes) and runs the testbench on it to give the output.
- **Run Post Implementation Timing Simulation** It is creating a Post Implementation Simulation netlist (e.g. - it is completing the synthesis and implementation) and then it is running the testbench in that netlist which is closest to running in an FPGA.



# <h1 id="header-4">Day 4 - Introduction To SOFA FPGA Fabric</h1>
## <h1 id="header-4_1">SOFA (Skywater Opensource FPGAs)</h1>
SOFA (Skywater Opensource FPGAs) is a collection of opensource FPGAs IPs using the open-source [Skywater 130nm PDK](https://github.com/google/skywater-pdk) and [OpenFPGA](https://github.com/lnis-uofu/OpenFPGA) framework.
Skywater Opensource FPGA (SOFA) is a completely open-source embedded FPGA IP library, including the description of the architecture and layouts that are ready for production. As shown in the illustration below, the Synopsys IC Compiler II, OpenFPGA, and Skywater 130nm PDK are used to develop SOFA IPs. The design flow runs for a total of 24 hours for each IP.

The Caravel SoC interface is supported by all SOFA FPGAs. With its high-density architecture and low-cost design strategy, we hope to empower embedded applications.
![Screenshot (2181)](https://user-images.githubusercontent.com/120498080/208638108-72987dfa-1941-43ea-9316-afdd7e658e89.png)
- [SOFA Main Reference](https://github.com/lnis-uofu/SOFA)
### The following eFPGA (Embedded FPGA) IPs are supported by this repository:
- Architecture description file: Using the VTR project and the OpenFPGA project, users can examine architecture specifics and test architecture evaluation.
- Fabrication-ready GDSII layouts: Users can integrate them into their chip designs.
- Post-layout Verilog Netlists: Users can run HDL simulations on the eFPGA IPs to validate their applications.
- Benchmark suites: An example benchmarking suite with which users can run quick examples on the eFPGA IPs
- Documentation: Datasheets for each eFPGA IPs down to circuit-level details

### Resource Utilization of HD eFPGA
![Screenshot (2109)](https://user-images.githubusercontent.com/120498080/208286236-582cb3e7-4223-475e-b94b-88bf657fd7cf.png)

## <h1 id="header-4_2">Running SOFA to design a counter</h1>
First I started with a **design of a counter in SOFA** and then I will use a design of a RISC-V processor called RVMyth in SOFA
### Installing and Running SOFA
- Go to the directory in which SOFA is installed and use `git clone https://github.com/lnis-uofu/SOFA.git` (where all the files are pre-available from SOFA) 
- Our working directory in `Desktop/Day4_counter/SOFA/`
- Then open `Desktop/Day4_counter/SOFA/FPGA1212_QLSOFA_HD_PNR/FPGA1212_QLSOFA_HD_task/config/task_simulation.conf` which contains all the path information about .yml .openfgpa .xml counter.v etc files, and set the correct locations.
- Now open `Desktop/Day4_counter/SOFA/FPGA1212_QLSOFA_HD_PNR/FPGA1212_QLSOFA_HD_task/generate_testbench.openfpga` which is a Shell Script going to call of invoking VPR tool.
- Then the architecture file is available under the `Desktop/Day4_counter/SOFA/FPGA1212_QLSOFA_HD_PNR/FPGA1212_QLSOFA_HD_task/arch/vpr_arch.xml` which tool is going to use and it gives an overview of how many LUTs, FF, etc are used.
- Then `vim ~/.bashrc` and give the correct location where VTR_ROOT, OPENFPGA and VIVADO is installed.
```
export VTR_ROOT=/home/kunalg123/Desktop/vtr-verilog-to-routing
export OPENFPGA_PATH=/home/kunalg123/Desktop/OpenFPGA
alias vivado=/tools/Xilinx/Vivado/2019.2/bin/vivado
```
- Now go to `Desktop/Day4_counter/SOFA/FPGA1212_QLSOFA_HD_PNR`
- Then run 'make runOpenFPGA'
### Running OpenFPGA
![Screenshot (2145)](https://user-images.githubusercontent.com/120498080/208414894-c5232a8a-a70a-4cf0-9631-07f71cfa21cb.png)
- So after completion, it is going to dump all the outputs as .blif .rpt .log under the location: 
- **File Dumping Location** `/Desktop/Day4_counter/SOFA/FPGA1212_QLSOFA_HD_PNR/FPGA1212_QLSOFA_HD_task/latest/vpr_arch/counter/MIN_ROUTE_CHAN_WIDTH`
- This `openfpgashell.log` file gives the detail about the set of commands it has run, the outputs, and the area reports.
- **NOTE** If we face some error in running 'make runOpenFPGA' then we can study the error in this  `openfpgashell.log` files
#### openfpgashell.log files
![Screenshot (2146)](https://user-images.githubusercontent.com/120498080/208415211-63b7b434-ff54-4f6a-97e6-a28cb4bec00e.png)


- ***NOTE** Command to open a text editor in Linux - After going into that folder using `vim <file_name.extension>*
- ***NOTE** Command to close and save a text editor in Linux - Press Esc then type `:wq` and press Enter*
- ***NOTE** Command to close and not save a text editor in Linux - Press Esc then type `:q!` and press Enter*
- ***NOTE** Command to go back to one folder in Linux is `cd ../` and press Enter*

### Area Analysis using SOFA
- The `vpr_stdout.log file` generate in the Dump file location contain information about the Utilization Report(Area Report) of our Design. 
#### Output of Area Analysis
![Screenshot (2150)](https://user-images.githubusercontent.com/120498080/208416320-d1d55b2e-169f-4515-bbcf-3ea855e54d59.png)

### Timing Analysis using SOFA
- To do timing analysis using SOFA makes a `counter.sdc` file with details about the clock periods and delays as shown below
```
create_clock -period 20 clk
set_input_delay -clock clk -max 0 [get_ports {*}]
set_output_delay -clock clk -max 0 [get_ports {*}]
```
- Then make Add `--sdc_file /home/is22mtech14002/Desktop/DAY3_COUNTER/SOFA/FPGA1212_QLSOFA_HD_PNR/FPGA1212_QLSOFA_HD_task/BENCHMARK/counter/counter.sdc` on `Desktop/Day4_counter/SOFA/FPGA1212_QLSOFA_HD_PNR/FPGA1212_QLSOFA_HD_task/generate_testbench.openfpga` and run the `make runOpenFPGA` again then it will generate a `report_timing.setup.rtp` file in Dumping Location.
#### Changes made in generate_testbench.openfpga
![Screenshot (2147)](https://user-images.githubusercontent.com/120498080/208415716-796ebf09-bc37-4e0d-ad2c-333d6080c2b7.png)
#### Output of Timing Analysis
![Screenshot (2151)](https://user-images.githubusercontent.com/120498080/208416545-74759913-baec-41d7-9c13-93b5179c6d3d.png)
![Screenshot (2152)](https://user-images.githubusercontent.com/120498080/208416586-a6b9d4c2-4eff-4b79-8c39-1e8d64039890.png)
### Generation of Post Implementation Netlist and Running Post Implementation Netlist using SOFA
- To Generation of Post Implementation Netlis add `--gen_post_synthesis_netlist on` on `Desktop/Day4_counter/SOFA/FPGA1212_QLSOFA_HD_PNR/FPGA1212_QLSOFA_HD_task/generate_testbench.openfpga` and run the `make runOpenFPGA` again then it will generate a `counter_post_synthesis.v` file in Dumping Location.
#### Changes made in generate_testbench.openfpga
![Screenshot (2148)](https://user-images.githubusercontent.com/120498080/208416641-009fd10d-2f02-4629-8e19-e21dba169279.png)
- Now after the creation of this `counter_post_synthesis.v` file use `primitives.v` and `counter_tb.v` files and check the outputs in an FPGA simulator like vivado (while project creation we can choose any board we want because we are using OpenFPGA)
#### Behavioural Simulation
![Screenshot (2130)](https://user-images.githubusercontent.com/120498080/208416788-93e7bc8f-7cef-4c4d-863f-a8607bfb43e0.png)
### Power Analysis using SOFA
- To perform the Power analysis using SOFA we need to make some changes in the `task_simulation.conf` file, the `generate_testbench.openfpga` file, and the 'vpr_arch.xml` file ( changed vpr_arch.xml is already available in GitHub repo) 
#### Changes in task_simulation.conf file
![Screenshot (2132)](https://user-images.githubusercontent.com/120498080/208365493-0fc4f058-0f3b-451b-8701-82aef2c5821c.png)
#### Changes in task_simulation.conf file
- Add `--power --activity_file /home/is22mtech14002/Desktop/DAY3_COUNTER/SOFA/FPGA1212_QLSOFA_HD_PNR/FPGA1212_QLSOFA_HD_task/latest/vpr_arch/counter/MIN_ROUTE_CHAN_WIDTH/counter_ace_out.act  --tech_properties /home/kunalg123/Desktop/vtr-verilog-to-routing/vtr_flow/tech/PTM_45nm/45nm.xml` where .act will is generated from the previous run of Open FPGA and 45nm.xml file is already available when we download VTR.
![Screenshot (2135)](https://user-images.githubusercontent.com/120498080/208366229-40f5e6fc-665b-4f84-9f64-818893cd8410.png)
- Then again run 'make runOpenFPGA' which will create a `counter.power file` in the dump File location which will contain information about the power breakdown of the circuit.
- But in our design, we were getting errors in the generation of the outputs.
#### Generated error message in `openfpgashell.log`
![Screenshot (2163)](https://user-images.githubusercontent.com/120498080/208490994-30a72b2d-6d2f-4ddb-9378-caa58eaba133.png)




# <h1 id="header-5">Day 5 - RISCV Core on Custom SOFA Fabric</h1>
Here **we are going to implement the RISC-V processor core which is the RVMyth Core on SOFA** 
## <h1 id="header-5_1">Running SOFA to design a RISC-V Core</h1>
### Installing and Running SOFA
- Go to the directory in which we need to install SOFA and use `git clone https://github.com/lnis-uofu/SOFA.git` (where all the files are pre-available from SOFA) 
- Our working directory in `Desktop/Day5_RVMyth/SOFA/`
- Then open `Desktop/Day5_RVMyth/SOFA/FPGA1212_QLSOFA_HD_PNR/FPGA1212_QLSOFA_HD_task/config/task_simulation.conf` which contains all the path information about .yml .openfgpa .xml counter.v etc files, and set the correct locations. (changed task_simulation.conf is already available in GitHub repo Day5) 
#### Changes in task_simulation.conf file
![Screenshot (2137)](https://user-images.githubusercontent.com/120498080/208372853-8838a1cf-96c2-413d-9ec7-afd8e018e2a8.png)
- Now open `Desktop/Day5_RVMyth/SOFA/FPGA1212_QLSOFA_HD_PNR/FPGA1212_QLSOFA_HD_task/generate_testbench.openfpga` which is a Shell Script going to call of invoking VPR tool. (changed generate_testbench.openfpga is already available in GitHub repo Day5)
#### Changes in generate_testbench.openfpga file
![Screenshot (2138)](https://user-images.githubusercontent.com/120498080/208373059-5edb2f96-1edb-49fb-a776-9724f81f922b.png)

- Then the architecture file is available under the `Desktop/Day5_RVMyth/SOFA/FPGA1212_QLSOFA_HD_PNR/FPGA1212_QLSOFA_HD_task/arch/vpr_arch.xml` which tool is going to use and it gives an overview of how many LUTs, FF, etc are used. (changed vpr_arch.xml is already available in GitHub repo Day5)
- Then `vim ~/.bashrc` and give the correct location where VTR_ROOT, OPENFPGA and VIVADO is installed.
```
export VTR_ROOT=/home/kunalg123/Desktop/vtr-verilog-to-routing
export OPENFPGA_PATH=/home/kunalg123/Desktop/OpenFPGA
alias vivado=/tools/Xilinx/Vivado/2019.2/bin/vivado
```
- Now go to `Desktop/Day5_RVMyth/SOFA/FPGA1212_QLSOFA_HD_PNR`
- Then run `make runOpenFPGA`
### Running OpenFPGA
![Screenshot (2140)](https://user-images.githubusercontent.com/120498080/208392216-219c16e1-e13a-4af3-8cd5-ca9f99cb59ed.png)
- So after completion, it is going to dump all the outputs as .blif .rpt .log under the location: 
- **File Dumping Location** `/Desktop/Day5_RVMyth/SOFA/FPGA1212_QLSOFA_HD_PNR/FPGA1212_QLSOFA_HD_task/latest/vpr_arch/core/MIN_ROUTE_CHAN_WIDTH`
- This `openfpgashell.log` file gives the detail about the set of commands it has run , the outputs, and the area reports.
- **NOTE** If we face some error in running 'make runOpenFPGA' then we can study the error in this  `openfpgashell.log` files
#### openfpgashell.log files
![Screenshot (2141)](https://user-images.githubusercontent.com/120498080/208392339-a2f44f10-23c8-4176-95f7-39a6595abcdb.png)
### Area Analysis using SOFA
- The `vpr_stdout.log file` generate in the Dump file location contain information about the Utilization Report(Area Report) of our Design. 
#### Output of Area Analysis
![Screenshot (2142)](https://user-images.githubusercontent.com/120498080/208397931-0b97b5b1-0dfe-4a7b-b805-0c10f0c0082f.png)
### Timing Analysis using SOFA
- To do timing analysis using SOFA makes a `mythcore.sdc` file with details about the clock periods and delays as shown below (here we have used a slow clock with a period of 200nsec because it's for a design of a processor and it needs to meet the timings)
```
create_clock -period 200 clk
set_input_delay -clock clk -max 0 [get_ports {*}]
set_output_delay -clock clk -max 0 [get_ports {*}]
```
- Then add `--sdc_file /home/is22mtech14002/Desktop/Day5_RVMyth/SOFA/FPGA1212_QLSOFA_HD_PNR/FPGA1212_QLSOFA_HD_task/BENCHMARK/rvmyth/mythcore.sdc` on `Desktop/Day5_RVMyth/SOFA/FPGA1212_QLSOFA_HD_PNR/FPGA1212_QLSOFA_HD_task/generate_testbench.openfpga` and run the `make runOpenFPGA` again then it will generate a `report_timing.setup.rtp` file in Dumping Location.
#### Changes made in generate_testbench.openfpga
![Screenshot (2153)](https://user-images.githubusercontent.com/120498080/208424757-053d226e-d9ab-4e2d-8f5f-0df86d6f93c9.png)
#### Output of Timing Analysis
![Screenshot (2155)](https://user-images.githubusercontent.com/120498080/208424985-fc9baf48-bd49-4cf2-9e90-98b4763bd03e.png)
![Screenshot (2157)](https://user-images.githubusercontent.com/120498080/208425013-caa33a9c-1954-4110-89a7-cb6e2f1cad9d.png)
### Generation of Post Implementation Netlist and Running Post Implementation Netlist using SOFA
- To Generation of Post Implementation Netlis add `--gen_post_synthesis_netlist on` on `Desktop/Day3_counter/SOFA/FPGA1212_QLSOFA_HD_PNR/FPGA1212_QLSOFA_HD_task/generate_testbench.openfpga` and run the `make runOpenFPGA` again then it will generate a `core_post_synthesis.v` file in Dumping Location.
#### Changes made in generate_testbench.openfpga
![Screenshot (2158)](https://user-images.githubusercontent.com/120498080/208426103-a925cd43-58b7-466a-80e7-e5ffae9d7526.png)
- Now after the creation of this `core_post_synthesis.v` file use `primitives.v` and `test.v` files and check the outputs in an FPGA simulator like vivado (while project creation we can choose any board we want because we are using OpenFPGA)
#### Behavioural Simulation
![Screenshot (2159)](https://user-images.githubusercontent.com/120498080/208431880-73730c32-2cc1-4195-9730-e937f860a197.png)

# <h1 id="header-6">References</h1>
- [VLSI System Design](https://www.vlsisystemdesign.com/ip/)
- https://docs.verilogtorouting.org/en/latest/vtr/cad_flow/
- https://docs.verilogtorouting.org/en/latest/arch/reference/#arch-grid-layout
- https://www.xilinx.com/products/boards-and-kits/1-54wqge.html
- https://www.elprocus.com/fpga-architecture-and-applications/
- https://openfpga.readthedocs.io/en/master/
- https://skywater-openfpga.readthedocs.io/_/downloads/en/latest/pdf/
- [Workshop GitHub Material]( https://github.com/nandithaec/fpga_workshop_collaterals)
# <h1 id="header-7">Acknowledgement</h1>
Finally, I would like to express my sincere gratitude to [Mr. Kunal Ghosh](https://github.com/kunalg123) {Co-founder of VLSI System Design (VSD) Corp. Pvt. Ltd.} and [Dr. Nanditha Rao](https://www.iiitb.ac.in/faculty/nanditha-rao) {Assistant Professor at International Institute of Information Technology – Bangalore} for tremendous assistance in planning and presenting this workshop on FPGA Fabric Design and Architecture. The workshop was excellent and well designed, this workshop taught me a lot of new things about the design of counter and RISC-V processor in FPGA Basys 3 board and  Open Source FPGA using VTR and VPR flow and about the SOFA FPGA fabric IP.   
