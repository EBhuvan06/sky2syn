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
    
## Intro to Iverilog
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






