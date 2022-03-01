# Low Power and High Speed Voltage Level Shifter Based on Cross Coupled Pull Up Network
## Contents
* Abstract
* Tools Used
* Introduction
* Reference Circuit and Waveforms
* Proposed 28nm based Design
* Simulation Results
* Netlist
* Author
* Acknowledgements
* References


### Abstract
A low power voltage level shifter (LS) design is presented in this paper. A regulated cross coupled (RCC) pull-up network is utilized in this design in order achieve high speed and low power consumption. This LS has the
ability to convert the input signals having voltage levels
lower than the threshold voltage of a MOS device to higher
nominal supply voltage levels. This design is proposed to be
implemented using 28nm technology node.

## Tools Used
### Synopsys Custom Compiler Tool Details
The Synopsys Custom Compiler™ design environment is a modern solution for full-custom analog, custom digital, and mixed-signal IC design. As the heart of the Synopsys Custom Design Platform, Custom Compiler provides design entry, simulation management and analysis, and custom layout editing features. It delivers industry-leading productivity, performance, and ease-of-use while remaining easy to adopt for users of legacy tools.


### Introduction
Generally, systems operating with two or more different
supply voltages between sub blocks will require voltage level
shifting of the signals. This would be achieved using a voltage
level shifter (LS). The voltage level shifters must have the
ability to convert low logic levels including subthreshold
voltage levels to a higher and acceptable voltage levels for the
preceding block. Due to this requirement of large number of
level shifters in a system, the power consumption and
propagation delay and also the silicon area are the major issues
in level shifter designs. Hence, there is a necessity to modify
the level shifters for the optimization of the above mentioned
parameters.

### Reference Circuit and Waveforms
![Screenshot_206-modified](https://user-images.githubusercontent.com/85724019/156216657-e94930ad-544a-466c-b825-8c0acedd3bea.png)

This design is a modified DCVS structure, which includes a
regulated cross-coupled (RCC) pair to achieve pull-up. This
technique enhances the strength of the pull-up network and also
reduces the charging or discharging time of the critical internal
nodes, which in turn increases the switching speed and reduces
the dynamic power dissipation.

![Screenshot_210](https://user-images.githubusercontent.com/85724019/156216727-7e928062-0f64-4ce6-aa66-1f039f6dfceb.png)



### Proposed 28nm based Design
This design is implemented using 28nm technology node. As per the reference circuit, the VDDH is 1.8V and VDDL is 0.6V.
![Screenshot_209](https://user-images.githubusercontent.com/85724019/156206647-a280bab6-af85-411a-9419-6afd5b232249.png)


### Simulation Results
![Screenshot_207](https://user-images.githubusercontent.com/85724019/156206713-068105cf-0eba-4232-b531-0c32323cecd2.png)

The proposed Level shifter shifts the signals from the deep
subthreshold level to the high and nominal supply voltages.
The entire design was implemented in Synopsys custom design tool using the 28nm technology node with 1.8V as supply. The results show that the proposed circuit can
shift up the input signals as low as 80 mV to about 1.8 V
and while having lowest area and power-delay product. In this simulation result it is observed that the input voltage is 400mV and it has been upshifted to approximately 1.8V which is close to supply voltage.
The average power consumption of this design is found to be 86.2 nW whereas the design based on 180nm technology node was 123.1nW. Hence there is an improvement in power cosumption.
### Netlist
```
*Custom Compiler Version S-2021.09
*Tue Mar  1 15:53:37 2022

.global gnd!
********************************************************************************
* Library          : Level_Shifter
* Cell             : Inverter_LS
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
.subckt inverter_ls vdd vin vout gnd_1
xm1 vout vin vdd vdd p105 w=0.1u l=0.03u nf=1 m=1
xm0 vout vin gnd_1 gnd_1 n105 w=0.1u l=0.03u nf=1 m=1
.ends inverter_ls

********************************************************************************
* Library          : Level_Shifter
* Cell             : LS
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
xi8 net34 in net33 gnd! inverter_ls
v12 net34 gnd! dc=0.6
v11 net79 gnd! dc=1.8
xm10 out net17 net79 net79 p105 w=0.1u l=0.03u nf=1 m=1
xm5 net29 net29 net21 net21 p105 w=0.1u l=0.03u nf=1 m=1
xm4 net25 net25 net17 net17 p105 w=0.1u l=0.03u nf=1 m=1
xm2 net17 net21 net69 net69 p105 w=0.1u l=0.03u nf=1 m=1
xm3 net21 net17 net14 net14 p105 w=0.1u l=0.03u nf=1 m=1
xm1 net14 net21 net79 net79 p105 w=0.1u l=0.03u nf=1 m=1
xm0 net69 net17 net79 net79 p105 w=0.1u l=0.03u nf=1 m=1
v22 in gnd! dc=0 pulse ( 400m 0 0 50p 50p 40n 80n )
xm7 net29 net33 gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm6 net25 in gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm9 out net25 gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
```

### Author
```
Naveen Kumar S, Department of Micro and Nano Electronics, Vellore Institute of Technology, Vellore, Tamil Nadu-632014
```

### Acknowledgement
* Kunal Ghosh, Co-founder, VSD Corp. Pvt. Ltd. - kunalpghosh@gmail.com
* Chinmay panda, IIT Hyderabad
* Sameer Durgoji, NIT Karnataka
* Synopsys India

### References
* S. Kabirpour and M. Jalali, "A Low-Power and High-
Speed Voltage Level Shifter Based on a Regulated Cross-
Coupled Pull-Up Network," in IEEE Transactions on
Circuits and Systems II: Express Briefs, vol. 66, no. 6, pp.
909-913, June 2019, doi: 10.1109/TCSII.2018.2872814.
* K. Usami, M. Igarashi, F. Minami, T. Ishikawa, M.
Kanzawa, M. Ichida, et al., "Automated low-power
technique exploiting multiple supply voltages applied to a
media processor," IEEE Journal of Solid-State Circuits,
vol. 33, pp. 463-472, 1998.
* S. R. Hosseini, M. Saberi, and R. Lotfi, "A High-Speed and
Power-Efficient Voltage Level Shifter for Dual-Supply
Applications," IEEE Transactions on Very Large Scale
Integration (VLSI) Systems, vol. 25, pp. 1154-1158, 2017.
