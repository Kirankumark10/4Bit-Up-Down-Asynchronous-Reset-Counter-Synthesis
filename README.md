# 4Bit-Up-Down-Asynchronous-Reset-Counter-Synthesis

## Aim:

Synthesize 4Bit-Up-Down-Asynchronous-Reset-Counter design using Constraints and analyse reports, Timing, area and Power.

## Tool Required:

Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim)

Synthesis: Genus

### Step 1: Getting Started

Synthesis requires three files as follows,

◦ Liberty Files (.lib)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd)

◦ SDC (Synopsis Design Constraint) File (.sdc)

 ### Step 2 : Creating an SDC File

•	In your terminal type “gedit input_constraints.sdc” to create an SDC File if you do not have one.

•	The SDC File must contain the following commands;

create_clock -name clk -period 2 -waveform {0 1} [get_ports "clk"]

set_clock_transition -rise 0.1 [get_clocks "clk"]

set_clock_transition -fall 0.1 [get_clocks "clk"]

set_clock_uncertainty 0.01 [get_ports "clk"]

set_input_delay -max 0.8 [get_ports "rst"] -clock [get_clocks "clk"]

set_output_delay -max 0.8 [get_ports "count"] -clock [get_clocks "clk"]

i→ Creates a Clock named “clk” with Time Period 2ns and On Time from t=0 to t=1.

ii, iii → Sets Clock Rise and Fall time to 100ps.

iv → Sets Clock Uncertainty to 10ps.

v, vi → Sets the maximum limit for I/O port delay to 1ps.

### Step 3 : Performing Synthesis

The Liberty files are present in the library path,

• The Available technology nodes are 180nm ,90nm and 45nm.

• In the terminal, initialise the tools with the following commands if a new terminal is being
used.

◦ csh

◦ source /cadence/install/cshrc

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist.
### Code:
```
`timescale 1ns / 1ns

module counter_test;

reg clk,rst,m;

wire [3:0] count;

initial

begin

clk=0;

rst=0;#5;

rst=1;

end

initial

begin

m=1;

#160 m=0;

end

counter counter1 (clk,m,rst, count);

always #5 clk=~clk;
 
initial $monitor("Time=%t rst=%b clk=%b count=%b" , $time,rst,clk,count);

initial
#320 $finish;

endmodule

```

#### Synthesis RTL Schematic :
![Screenshot (136)](https://github.com/user-attachments/assets/de97eeb0-1626-4375-89f1-d057d6ea82f1)

#### Area report:
![Screenshot (137)](https://github.com/user-attachments/assets/5c083390-1839-4a7d-b0c0-a94b554ee1c4)

#### Power Report:
![Screenshot (138)](https://github.com/user-attachments/assets/dc6511ff-a677-45bd-88d3-df677f5b0b02)

#### Timing Report: 
![Screenshot (139)](https://github.com/user-attachments/assets/b1d167a4-c223-4a43-8e49-aa87e29f20d7)

#### Result: 

The generic netlist has been created, and area, power, and timing reports have been tabulated and generated using Genus.





