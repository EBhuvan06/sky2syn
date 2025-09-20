# sky2syn
Skywater to Synopsys
  <details>
<summary>Week_0</summary>
    
## Document
We are going to understand the given below process 

soft copy of the Hardware using RTL
          
          ---> 1.Processor
               ---> 1.Gate Level Netlist
          
          ---> 2.Peripherals/IPs
               ---> 1.Macros
               ---> 2.Analog IPs 


Using the small part(blue block) which has basic gates, transistors, IPs etc. This create GDSII sent to factory which is Tape-in we get the chips out which is called Tape-out by this we are going to get the chip for that we are going to provide the peripherals for the chip which is taped-out once we get the chip we can interface with different equipments which can work under 100Mhz to 130Mhz like Arduino boards, TV pannels, AC applications etc..

## Yosys
$ git clone https://github.com/YosysHQ/yosys.git
$ cd yosys 
$ sudo apt install make (If make is not installed please install it)
$ sudo apt-get install build-essential clang bison flex \ 
    libreadline-dev gawk tcl-dev libffi-dev git \ 
    graphviz xdot pkg-config python3 libboost-system-dev \ 
    libboost-python-dev libboost-filesystem-dev zlib1g-dev \
$ make \
$ sudo make install 
 

![Yosys Installed](Week_0/yosys.png)

## Iverilog

$ sudo apt-get install iverilog



![Iverilog Installed](Week_0/iverilog.png)

## GTKWave

$ sudo apt update \
$ sudo apt install gtkwave 

[GTKWave Installed](Week_0/gtkwave.png)






