# sky2syn
Skywater to Synopsys
  <details>
<summary>Week_0</summary>
## Document
                                    -----> Processor -----------> Gate Level Netliat
soft copy of the Hardware using RTL                       ------> Macros    
                                    ----->Peripherals/IPs 
                                                          -------> Analog IP

USing the small part(blue block) which has basic gates, transistors, IPs etc. This create GDSII sent to factory which is Tape-in we get the chips out which is called Tape-out by this we are going to get the chip for that we are going to provide the peripherals for the chip which is taped-out once we get the chip we can interface with different equipments which can work under 100Mhz to 130Mhz like Arduino boards, TV pannels, AC applications etc..

## Yosys

$ git clone https://github.com/YosysHQ/yosys.git
$ cd yosys 
$ sudo apt install make (If make is not installed please install it) 
$ sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
$ make 
$ sudo make install

 

![Yosys Installed](Week_0/yosys.png)

##Iverilog

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

![Iverilog Installed](Week_0/iverilog.png)

##GTKWave

$ sudo apt update
$ sudo apt install gtkwave


bhuvan@HP-Pavilion-Plus-Laptop-14-ew0xxx:~$ gtkwave
Gtk-Message: 21:42:49.369: Failed to load module "canberra-gtk-module"

GTKWave Analyzer v3.3.104 (w)1999-2020 BSI

GTKWAVE | Use the -h, --help command line flags to display help.

![GTKWave Installed](Week_0/gtkwave.png)






