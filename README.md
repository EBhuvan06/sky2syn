# sky2syn
Skywater to Synopsys
<details>
<summary>Week_0</summary>
    
## Document
We are going to understand the given below process 
```
soft copy of the Hardware using RTL
              |
              | 
   ___________|_________________
   |                           |
   |                           |
 Processor               Peripherals/IPs
   |                           |
   |                           |
 Gate Level              ______|_____
  Netlist                |          |
                      Macros       Analog IPs
```


Using the small part(blue block) which has basic gates, transistors, IPs etc. This create GDSII sent to factory which is Tape-in we get the chips out which is called Tape-out by this we are going to get the chip for that we are going to provide the peripherals for the chip which is taped-out once we get the chip we can interface with different equipments which can work under 100Mhz to 130Mhz like Arduino boards, TV pannels, AC applications etc..

## Yosys
```
$ git clone https://github.com/YosysHQ/yosys.git
$ cd yosys 
$ sudo apt install make (If make is not installed please install it) 
$ sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
$ make 
$ sudo make install


bhuvan@HP-Pavilion-Plus-Laptop-14-ew0xxx:~/yosys$ yosys

 /----------------------------------------------------------------------------\
 |  yosys -- Yosys Open SYnthesis Suite                                       |
 |  Copyright (C) 2012 - 2025  Claire Xenia Wolf <claire@yosyshq.com>         |
 |  Distributed under an ISC-like license, type "license" to see terms        |
 \----------------------------------------------------------------------------/
 Yosys 0.57+153 (git sha1 6b3a7e244, g++ 11.4.0-1ubuntu1~22.04.2 -fPIC -O3)

yosys> license 

 /----------------------------------------------------------------------------\
 |                                                                            |
 |  yosys -- Yosys Open SYnthesis Suite                                       |
 |                                                                            |
 |  Copyright (C) 2012 - 2025  Claire Xenia Wolf <claire@yosyshq.com>         |
 |                                                                            |
 |  Permission to use, copy, modify, and/or distribute this software for any  |
 |  purpose with or without fee is hereby granted, provided that the above    |
 |  copyright notice and this permission notice appear in all copies.         |
 |                                                                            |
 |  THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES  |
 |  WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF          |
 |  MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR   |
 |  ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES    |
 |  WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN     |
 |  ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF   |
 |  OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.            |
 |                                                                            |
 \----------------------------------------------------------------------------/


yosys> 

 ```
![Yosys Installed](Week_0/yosys.png)

## Iverilog
```
$ sudo apt-get install iverilog


bhuvan@HP-Pavilion-Plus-Laptop-14-ew0xxx:~$ iverilog
iverilog: no source files.

Usage: iverilog [-EiSuvV] [-B base] [-c cmdfile|-f cmdfile]
                [-g1995|-g2001|-g2005|-g2005-sv|-g2009|-g2012] [-g<feature>]
                [-D macro[=defn]] [-I includedir] [-L moduledir]
                [-M [mode=]depfile] [-m module]
                [-N file] [-o filename] [-p flag=value]
                [-s topmodule] [-t target] [-T min|typ|max]
                [-W class] [-y dir] [-Y suf] [-l file] source_file(s)

See the man page for details.
```


![Iverilog Installed](Week_0/iverilog.png)

## GTKWave
```
$ sudo apt update 
$ sudo apt install gtkwave


bhuvan@HP-Pavilion-Plus-Laptop-14-ew0xxx:~$ gtkwave
Gtk-Message: 21:42:49.369: Failed to load module "canberra-gtk-module"

GTKWave Analyzer v3.3.104 (w)1999-2020 BSI

GTKWAVE | Use the -h, --help command line flags to display help.
```

![GTKWave Installed](Week_0/gtkwave.png)
</details>
<details>
<summary>Week_1</summary>
<details>
<summary>Day_1</summary>
<details>
<summary>Intro to Iverilog</summary> 
    
## Simulation
  ```
Checking of design is done by simulation.
We are going to use iverilog simulator to simulate the design.
```
## Design
    
Design is the actual verilog code or set of verilog codes which has the intended functionality to meet with the required specification.

## Test Bench
```
TB(Test Bench) is used to check whether it obey required specifications or not.
We have to apply stimulus(test_verilog) to the design and have to observe output and check whether it matches with specifications or not.
```
## How Simulation Works

First simulator checks for the changes on the input. Upon change to the input the output is evaluated. If no change to input no change in output.
``` 
 ----------            --------            ----------
|          | Primary  |        |  Primary |          |
|Stimulus  |--------->| Design |--------->|Stimulus  |
| Generator|--------->|        |--------->| Obeserver|
|          |  inputs  |        | outputs  |          |
 ----------            --------            ----------

we have to instantiate Design in TB then we have availability to apply stimulus(test_cases)
Design may have 1 or more primary inputs & outputs
```
## Iverilog Basic Flow
```
   Design--------
                 |
                 |----->Iverilog Simulator---->.vcd file----->gtkwave---->Output Wave form
                 |                              
   Test Bench----

1 We give design and tb to iverilog simulator for checking specifications.
2 iverilog simulator only checks changes in input if there are changes in input we gona dump the chnages in output.
3 .vdc file(Value_Change_Dump format) is a output file which is used to check the changes in the output.
4 gtkwave is used to map the output changes in form of a wave.
```
  </details>
  <details>
<summary>How to use Iverilog and GTKWave</summary>

  ## Getting all files related to Iverilog
  First open terminal and clone git
  ```
$ sudo -i
# go to the directory where you want to paste the librays and verilog codes using git
~# git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
```
We got all verilog files and librarys required to perform iverilog simulation

## Knowing how gtkwave and iverilog works
After cloning the git go to sky130RTLDesignAndSynthesisWorkshop -----> verilog_files directory
```
$sudo -i
#change the directory where sky130RTLDesignAndSynthesisWorkshop file exists
~# cd sky130RTLDesignAndSynthesisWorkshop/ verilog_files/
# in verilog_files we have all design related files and test benches for the respective design file
# now invoking the iverilog
~# iverilog design_file.v tb_design_file.v
# in this we are providing design and testbench of respective design file for simulation
~# ./a.out # for geting .vcd file for checking output
~# gtkwave tb_design_file.vcd # this gives the output wave form

```
## Terminal Overview
```
bhuvan@HP-Pavilion-Plus-Laptop-14-ew0xxx:~$ sudo -i
[sudo] password for bhuvan: 
root@HP-Pavilion-Plus-Laptop-14-ew0xxx:~# cd /home/bhuvan/
root@HP-Pavilion-Plus-Laptop-14-ew0xxx:/home/bhuvan# ls
Bhuvan     Downloads  Public                               sky2syn    Videos
Desktop    Music      README.md                            snap       yosys
Documents  Pictures   sky130RTLDesignAndSynthesisWorkshop  Templates
root@HP-Pavilion-Plus-Laptop-14-ew0xxx:/home/bhuvan# cd sky130RTLDesignAndSynthesisWorkshop/verilog_files/
root@HP-Pavilion-Plus-Laptop-14-ew0xxx:/home/bhuvan/sky130RTLDesignAndSynthesisWorkshop/verilog_files# ls
a.out                    partial_case_assign.v
bad_case_net.v           pattern_detect_fsm_bad_style.v
bad_case.v               pattern_detect_fsm.v
bad_counter.v            rca.v
bad_latch_2.v            ripple_counter.v
bad_latch_net.v          tb_bad_case.v
bad_latch.v              tb_bad_counter.v
bad_mux_net.v            tb_bad_latch2.v
bad_mux.v                tb_bad_latch.v
bad_shift_reg2.v         tb_bad_mux.v
bad_shift_reg.v          tb_bad_shift_reg2.v
blocking_caveat_net.v    tb_bad_shift_reg.v
blocking_caveat.v        tb_blocking_caveat.v
comp_case.v              tb_comp_case.v
counter_opt2.v           tb_counter_opt.v
counter_opt.v            tb_demux_case.v
demux_case.v             tb_demux_generate.v
demux_generate.v         tb_dff_asyncres_syncres.v
dff_ares.net.v           tb_dff_asyncres.v
dff_asyncres_net.v       tb_dff_async_set.v
dff_asyncres_syncres.v   tb_dff_const1.v
dff_asyncres.v           tb_dff_const2.v
dff_async_set.v          tb_dff_const3.v
dff_const1.v             tb_dff_const4.v
dff_const2.v             tb_dff_const5.v
dff_const3.v             tb_dff_syncres.v
dff_const4.v             tb_good_counter.v
dff_const5.v             tb_good_latch.v
dff_net.v                tb_good_mux.v
dff_syncres.v            tb_good_mux.vcd
fa.v                     tb_good_shift_reg.v
good_counter.v           tb_incomp_case.v
good_latch.v             tb_incomp_if2.v
good_mux_netlist.v       tb_incomp_if.v
good_mux.v               tb_multiple_modules.v
good_shift_reg.v         tb_mux_generate.v
incomp_case.v            tb_opt_check2.v
incomp_if2.v             tb_opt_check3.v
incomp_if.v              tb_opt_check.v
mul2_net.v               tb_partial_case_assign.v
mult_2.v                 tb_pattern_detect_fsm.v
mult_8.v                 tb_rca.v
multiple_module_opt2.v   tb_ripple_counter.v
multiple_module_opt.v    tb_ternary_operator_mux.v
multiple_modules_flat.v  tb_upcntr.v
multiple_modules_hier.v  tb_up_dn_cntr.v
multiple_modules.v       tb_up_dn_cntr_with_load.v
mux_generate.v           tb_up_dn_cntr_with_load_with_start_stop.v
mux_spice.v              ternary_operator_mux_net.v
net.v                    ternary_operator_mux.v
opt_check2.v             upcntr.v
opt_check3.v             up_dn_cntr.v
opt_check4.v             up_dn_cntr_with_load.v
opt_check.v              up_dn_cntr_with_load_with_start_stop.v
root@HP-Pavilion-Plus-Laptop-14-ew0xxx:/home/bhuvan/sky130RTLDesignAndSynthesisWorkshop/verilog_files# iverilog good_mux.v tb_good_mux.v 
root@HP-Pavilion-Plus-Laptop-14-ew0xxx:/home/bhuvan/sky130RTLDesignAndSynthesisWorkshop/verilog_files# ./a.out 
VCD info: dumpfile tb_good_mux.vcd opened for output.
root@HP-Pavilion-Plus-Laptop-14-ew0xxx:/home/bhuvan/sky130RTLDesignAndSynthesisWorkshop/verilog_files# gtkwave tb_good_mux.vcd 
Gtk-Message: 23:59:17.901: Failed to load module "canberra-gtk-module"

GTKWave Analyzer v3.3.104 (w)1999-2020 BSI


(gtkwave:10340): dconf-WARNING **: 23:59:17.916: failed to commit changes to dconf: Failed to execute child process ?dbus-launch? (No such file or directory)
[0] start time.
[300000] end time.

(gtkwave:10340): dconf-WARNING **: 23:59:18.099: failed to commit changes to dconf: Failed to execute child process ?dbus-launch? (No such file or directory)

(gtkwave:10340): dconf-WARNING **: 23:59:18.099: failed to commit changes to dconf: Failed to execute child process ?dbus-launch? (No such file or directory)
```

![Expected 1](Week_1/Expected_output_1.png)


![Expected](Week_1/Expected%20_output_2.png)

</details>

<details>
<summary>Checking the Desing and Test Bench</summary>

## Checking the code
To check the design code and testbench code first open terminal and go to the directory where the related files are present and run the below commands
```
$ sudo -i
~# cd /home/bhuvan/sky130RTLDesignAndSynthesisWorkshop/verilog_files/
~# gvim -O good_mux.v tb_good_mux.v
```
This gives the verilog design code and testbench code

![code](Week_1/Codes.png)

</details>

<details>
<summary>What is yosys</summary>

## yosys
Now we are going to use yosys which is the synthesizer used to convert RTL to netlist

## yosys setup
```
     ------------
    |Read_verilog|
     ------------   
       /                                 -------------
     /                                  |Write_verilog|
 --------                                -------------
|        |                                 /
| Design |------                         /  
|        |      |      -------        -------
 --------       |     |       |      |       |
                |---->| Yosys |----->|netlist|
 --------       |     |       |      |  file |
|        |      |      -------        -------
|  .lib  |------
|        |
 --------
    \  
      \
  ------------
 |Read_liberty|
  ------------
```

Read_verilog command to read the design and read_liberty command to read .lib file and write_verilog to write the netlist file. Once we execute the comand write_verilog we get the netlist output. Both netlist and design are same but Netlist is repreasentation of Design in the form cells present in the .lib.

## Verify the synthesis

The out put of the Iverilog basic flow which has Design code otput(RTL simulation) should be same as the netlist code output(synthesized output).
```
   NETLIST-------
                 |
                 |----->Iverilog Simulator---->.vcd file----->gtkwave---->Output Wave form
                 |                              
   Test Bench----
```
So the set of primary inputs or outputs will remain same between the RTL design and synthesized netlist which means the same test bench can be used for both the Dsign and Netlist codes. 

## Logic synthesis
RTL Design:
Behavioral representation of the required specification
```
module sample_code (                                         --------- 
input clk,rst, output result, done);                        |         |
always @ (posedge clk, posedge rst)                  ------>| D       |
if(rst)                                                     |         |------->Q
------                                               ------>|> clk    |
else                                                        |         |
------                                               ------>|  Reset  |               
endmodule                                                    ---------    
----------------------------------
       RTL Code                                          Digital Logic Circuit                         
```
Basically we dont want RTL code we wnat Logical circuit we map these two in the form of Synthesis. 
```
In synthesis the RTL code is translated into Gate level.                                    RTL    Frount End lib
The design is converted into gates and the connections are made between gates.               |___________| 
This is given a output file which is called netlist file.                                          |
                                                                                               synthesis
                                                                                                   | 
                                                                                                NETLIST
```
## What is .lib
```
.lib
This Collection of logical modules.
Includes basic logic gates like And, Or, Not, etc...
This has Different flavors of same gate
  2 input And gate which has
    Slow version
    Medium version
    Fast version
  3 input And gate also
    Slow version
    Medium version
    Fast version
4 input And gate
........so on
```
## Why use of different versions or flavours of gates
Combinational delay in logic path determines the maximum speed of operation of digital logic circuit
```
         ---------                    --------
        |         |                  |         |
        |         |----> combib ---->|         |      ___     ___     ___     ___
        |  D-FF A |                  |  D-FF B |    _|   |___|   |___|   |___|   |___ 
        |         |                  |         |    <--Tclk-->
        |         |                  |         |             propogation delay of comb  
 ------>|> clk    |               -->|> clk    |     TCLK > TCQ A + TCOMBI + TSETUP_B
    |    ---------               |    ---------        propogation delay of flop A                                    
    |____________________________|

```
The time taken for the clock to go from A to B is 1 clk cycle. We can't give the clock at same time for both FF because there might be chances of loss of data so we have to add a small delay which is called SETUP delay ot FF B by combining all of this the delay should be minimum for higher frequency  fclk_max = 1/clk_min. so for better performance dilay should be as less as possible. So we need cells that work fast to make TCOMBI Small. This where different types of versions of gates comes in to implementation.

## Need of slow cells

```
         ---------                    --------
        |         |                  |         |
        |         |----> combib ---->|         |      ___     ___     ___     ___
        |  D-FF A |                  |  D-FF B |    _|   |___|   |___|   |___|   |___ 
        |         |                  |         |       1       2       3       4  
        |         |                  |         |      THOLD_B < TCQ_A + TCOMBI           
 ------>|> clk    |               -->|> clk    |     
    |    ---------               |    ---------                                          
    |____________________________|
```
When A FF is launched at 1 then B should not capture the launched signal at 1 the b should be captured at 2 as there is possibility of loss of data. The combination of the delay of FF A and Combi should be greater than the Hold of B which helps in the condition which we disscused before for this the slow cells comes into image which helps to provide dely required. Simply to ensure that there are no hold voilations at B FF we cells that work slow. Hence we need cells that work fast to meet the required performance and cells that work slow to meet HOLD. This collection of fast and slow cells is present in .lib 

## Fast vs Slow

Load in Digital Logic circuit is Capacitance
```
Gate A -----> Gate B
```
IF the capacitance between the gates is large than it take time to charge and progation delay at B gate increases and if capacitor is small the cahrge time will be less so teh propogation delay is less simply Faster the charging / discharging of capacitance Lesser the cell delay
```
To charge / discharge the capacitance fast, we need transistors capable of sourcing more current means wide transistors
Wider transistors -> Low Delay -> More Area and Power as well !!
Narrow transistors -> More Delay -> Less Area and Power
Faster cells donot come free, they come at penalty of area and power
```
## selection of cells
```
Need to guide the Synthesizer to select the flavour of cells that is optimum for the implementation of logic circuit
More use of faster cells --> Bad circuit interms of Power and Area and Hold time violations 
More use of slower cells --> Sluggish circuit, may not meet the performance need
The guidance offered to the Synthesizer --> "Constraints"
```
## synthesis Illustration
```
  ------------------------------------
 | module (A, B,sel, clock, reset, Q) |                   ----------------------------------   
 | input A, B,sel, clock, reset;      |----------------->|                                  |
 | output Q;                          |                  |                                  |
  ------------------------------------                   |    |\                            |
  wire int;                                           B  |    |  \                          |
  -------------------------                        ----->|--->|I0  \                        |
 | assign int = sel ? A:B; |-----------------------------|--->|     |                       | 
  -------------------------                              |    |    Y|-----                  |
  ------------------------------------------          A  |    |     |     |     ------      |
 | always @(posedge clock or posedge reset) |      ----->|--->|I1  /      |    |      |     | 
 |  begin                                   |            |    |  /         --->|D     |     |
 |   if (reset)                             |            |    |/  |        --->|>clk q|---->|----->Q
 |   begin                                  |       Sel  |        |       |    |      |     |
 |      Q <= 1'b0;                          |      ----->|--------        |  ->|res   |     |
 |   end                                    |            |                | |   ---|--      |
 |   else if (clk)                          |      ----->|----------------  |      |        |
 |   begin                                  |      clock |                  |      |        |
 |      Q <= int;                           |      reset |                  |      |        |
 |   end                                    |      ----->|------------------       |        |
 |  end                                     |------------|-------------------------         |
  ------------------------------------------              ----------------------------------
endmodule
```
Module map to the top level. Assign block is used for making mux in the main block where output of mux is connected to the D FF. Finally the assign block is used for the D FF and Q output is connected to the main block. The circuit on the right is created from RTL using the gates in the .lib and give out as Netlist.

</details>

<details>
<summary>Introduction to synthesiser</summary>

## yosys
To convert RTL to Netlist follow the commands.
```
$ sudo -i
# change directory where the yosys has been installed
# yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
# to read the library
read_verilog module_name.v
# there should be no error
synth -top module_name
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
# this covert rtl file to gate level net list and .lib is used to specify the what type of gate to be used
show
#this show graphical version of netlist
```
![1](Week_1/1.png)
![2](Week_1/2.png)
![3](Week_1/3.png)
![4](Week_1/4.png)
![5](Week_1/5.png)
![6](Week_1/6.png)
![7](Week_1/7.png)
![8](Week_1/8.png)
![9](Week_1/9.png)
![10](Week_1/10.png)
![Graphical](Week_1/graphical_interface.png)

## Check netlist

To check net list run below commands
```
write_verilog good_mux_netlist.v 
!gvim good_mux_netlist.v
# This give all the text which is not use full so run
write_verilog -noattr good_mux_netlist.v
# eliminate un wanted things
!gvim good_mux_netlist.v
```
```
yosys> write_verilog good_mux_netlist.v 

7. Executing Verilog backend.

7.1. Executing BMUXMAP pass.

7.2. Executing DEMUXMAP pass.
Dumping module `\good_mux'.

yosys> !gvim good_mux_netlist.v 

8. Shell command: gvim good_mux_netlist.v
QStandardPaths: XDG_RUNTIME_DIR not set, defaulting to '/tmp/runtime-root'

yosys> QStandardPaths: XDG_RUNTIME_DIR not set, defaulting to '/tmp/runtime-root'


yosys> write_verilog -noattr good_mux_netlist.v 

9. Executing Verilog backend.

9.1. Executing BMUXMAP pass.

9.2. Executing DEMUXMAP pass.
Dumping module `\good_mux'.

yosys> !gvim good_mux_netlist.v 

10. Shell command: gvim good_mux_netlist.v
QStandardPaths: XDG_RUNTIME_DIR not set, defaulting to '/tmp/runtime-root'

yosys> QStandardPaths: XDG_RUNTIME_DIR not set, defaulting to '/tmp/runtime-root'


yosys> exit
```

![With_comments](Week_1/External_comments.png)
![Without_comments](Week_1/No_comments.png)

</details>
</details>
<details>
<summary>Day_2</summary>

## What .lib contains

P(process) V(voltage) T(temperature) plays a main role for a design to work. \
Process     -> variation due to fabrication \
voltage     -> variation due to voltage \
Temperature -> variation due to temperature \
Variation in PVT determine how the silicon is gona work like it is gona work faster or slower so we can not make a device every time with same specifications there will be minimal changes in the circuit so this small variations determine how the circuit is going to work. 
```
library ("sky130_fd_sc_hd__tt_025C_1v80") {
    define(def_sim_opt,library,string);
    define(default_arc_mode,library,string);
    define(default_constraint_arc_mode,library,string);
    define(driver_model,library,string);
    define(leakage_sim_opt,library,string);
    define(min_pulse_width_mode,library,string);
    define(simulator,library,string);
    define(switching_power_split_model,library,string);
    define(sim_opt,timing,string);
    define(violation_delay_degrade_pct,timing,string);
    technology("cmos");
    delay_model : "table_lookup";
    bus_naming_style : "%s[%d]";
    time_unit : "1ns";
    voltage_unit : "1V";
    leakage_power_unit : "1nW";
    current_unit : "1mA";
    pulling_resistance_unit : "1kohm";
    capacitive_load_unit(1.0000000000, "pf");
    revision : 1.0000000000;
    default_cell_leakage_power : 0.0000000000;
    default_fanout_load : 0.0000000000;
    default_inout_pin_cap : 0.0000000000;
    default_input_pin_cap : 0.0000000000;
    default_max_transition : 1.5000000000;
    default_output_pin_cap : 0.0000000000;
    default_arc_mode : "worst_edges";
    default_constraint_arc_mode : "worst";
    default_leakage_power_density : 0.0000000000;
    default_operating_conditions : "tt_025C_1v80";
    operating_conditions ("tt_025C_1v80") {
        voltage : 1.8000000000;
        process : 1.0000000000;
        temperature : 25.000000000;
        tree_type : "balanced_tree";
    }
    power_lut_template ("power_inputs_1") {
        variable_1 : "input_transition_time";
        index_1("1, 2, 3, 4, 5, 6, 7");
    }
```
IN this sky130_fd_sc_hd__tt_025C_1v80 \
tt stand for typical process \
025C stand for 25c temperature \
1v80 indicates 1.8v voltage. 

technology("cmos"); \
This tells what kind of technology we are going to use. In this we are using CMOS technology.

    time_unit : "1ns"; -------------------------> units of time in nano sec 
    voltage_unit : "1V";------------------------> units of voltage in volts 
    leakage_power_unit : "1nW";-----------------> units of power in nano whatt 
    current_unit : "1mA";-----------------------> units of current in milli amps
    pulling_resistance_unit : "1kohm";----------> units of resistance in kilo ohm
    capacitive_load_unit(1.0000000000, "pf");---> units of capacitance in peco farade 

   operating_conditions ("tt_025C_1v80") { ---> Tells the oeration conditions \
        voltage : 1.8000000000;---------> Voltage 1.8 \
        process : 1.0000000000;---------> process tt \
        temperature : 25.000000000;-----> temp 25 \
        tree_type : "balanced_tree"; \
   }


