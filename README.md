# Schematic and Layout design of a CMOS inverter using 180nm tech.
## I. CMOS Inverter Design using 180nm technology.
**_The motive of this project is to understand the basics of a cmos inverter designing and get a hands on the opensource design tools._** 
**The design tools used:**  
**esim**-To designing the schamitic.  
**ngspice**-  
**Magic**- For layout designing.  
**NetGen**- For Layout vs schamitic(LVS).  
**OpenTimer**- For Static timing analysis.   
_I have downloaded all the above tools by the following tutorial :  
And a very excillent site to learn these tools is the : opencircuit.com.  
### 1.Drawing schamitic using esim
![shows the schamatic of an inverter drawn using esim](https://github.com/Avs-Bharguav/VLSI-MINI-PROJECTS/blob/main/my_project/inverter_project_images/inv/Screenshot%20from%202023-04-04%2009-50-40.png)  
I have used the 180nm mos devices from the esim library and a pulsed input source.After making the schamitic go to option convert Kicad to ngspice and choose transiant analysis as shown.![](https://github.com/Avs-Bharguav/VLSI-MINI-PROJECTS/blob/main/my_project/inverter_project_images/inv/Screenshot%20from%202023-05-16%2013-36-59.png)   
Next in source details for pulsed source use this values:initial value-0 pulsed value-1.8v delay time-0 rise time-0 fall time-0 pulse width-1p  pulse period-2p. You can play with these values to get a proper graph. And put dc source of 1.8v.After which give the mos device model file in the device modeling option as shown.![](https://github.com/Avs-Bharguav/VLSI-MINI-PROJECTS/blob/main/my_project/inverter_project_images/inv/Screenshot%20from%202023-05-16%2014-18-46.png)  
Then press convert and simulate.It will give two graphs one from ngspice and other python plot.  
### Output  
### 1. Input vs Output
![Input vs output plot](https://github.com/Avs-Bharguav/VLSI-MINI-PROJECTS/blob/main/my_project/inverter_project_images/inv/ino.png)  
![](https://github.com/Avs-Bharguav/VLSI-MINI-PROJECTS/blob/main/my_project/inverter_project_images/inv/in%20vs%20out.png)   
![](https://github.com/Avs-Bharguav/VLSI-MINI-PROJECTS/blob/main/my_project/inverter_project_images/inv/image.png)  
### 2. Id Vs Vin
![Id Vs Vin](https://github.com/Avs-Bharguav/VLSI-MINI-PROJECTS/blob/main/my_project/inverter_project_images/inv/id.png)  
### 2.Layout designing using Magic.  
First you need to download the 180nm tech.. I have uploaded in the reprosetory by name "sample6m.tech". Go to tech. manager and load it. Then keeping in mind all the design rules you can draw the layout.  
![tech. manager](https://github.com/Avs-Bharguav/VLSI-MINI-PROJECTS/blob/main/my_project/inverter_project_images/magic/Screenshot%20from%202023-03-05%2015-26-53.png)  
![layout](https://github.com/Avs-Bharguav/VLSI-MINI-PROJECTS/blob/main/my_project/inverter_project_images/magic/Screenshot%20from%202023-03-27%2021-53-47.png)  
After that you extract all the node capacitances and resistances(*inv_layout.ext* ) and also the spice netlist of the layout(*inv_layout.spice*). Using ngspice we test the layout operational. If the layout is not proper then the output will have not reach its peak due to excess capacitances.  
     
**node capacitance** file - inv_layout.ext           
```  
timestamp 1678899716
version 8.3
tech sample_6m
style lambda=0.09(generic)
scale 1000 1 9
resistclasses 8000 8000 900000 900000 7400 80 80 80 80 80 40
node "gnd!" 59 200.04 -12 1 ppc 29 22 50 40 0 0 0 0 0 0 154 68 0 0 0 0 0 0 0 0 0 0
node "out" 23 137.692 -4 17 ndiff 29 22 48 28 0 0 0 0 0 0 135 66 0 0 0 0 0 0 0 0 0 0
node "in" 115 11.8854 -11 24 pc 0 0 0 0 0 0 0 0 82 76 40 28 0 0 0 0 0 0 0 0 0 0
node "vdd!" 1220 214.662 -17 29 nw 50 40 48 28 744 110 0 0 0 0 160 74 0 0 0 0 0 0 0 0 0 0
cap "gnd!" "in" 38.4783
cap "out" "vdd!" 40.5952
cap "gnd!" "vdd!" 13.497
cap "in" "vdd!" 23.093
cap "out" "gnd!" 41.6849
cap "out" "in" 23.087
device mosfet nmos -6 17 -5 18 2 4 "gnd!" "in" 4 0 "gnd!" 4 0 "out" 4 0
device mosfet pmos -6 34 -5 35 2 8 "vdd!" "in" 4 0 "vdd!" 8 0 "out" 8 0
subcap "vdd!" -44.4299   
``` 
   
**magic spice netlist**  file-inv_layout.spice
```
* SPICE3 file created from inv_layout.ext - technology: sample_6m

.option scale=0.09u

M1000 out in vdd vdd cmosp w=8 l=2
+  ad=48 pd=28 as=48 ps=28
M1001 out in gnd gnd cmosn w=4 l=2
+  ad=29 pd=22 as=29 ps=22
```
**For testing you can use the following ngspice code:**  file- magiclayout_spicetest.cir (ngspice takes .cir file)  

```
*magic layout test

.include NMOS-180nm.lib
.include PMOS-180nm.lib
.include inv_layout.spice



v1 vdd gnd 1.8
v2 in gnd pulse(0 1.8 0 50p 50p 1n 2n)

.control

tran 10p 8n
plot v(in) v(out)

 
.endc
.end
```  
*Note: the spice netlist, the .lib files all must be in the same directory where you are running ngspice.And in the spice files during specifying the connections of nmos and pmos the device names must be used as provided in its .lib/model file here cmosn/cmosp.*  
  
### Output
![ngspice out](https://github.com/Avs-Bharguav/VLSI-MINI-PROJECTS/blob/main/my_project/inverter_project_images/magic/Screenshot%20from%202023-03-27%2021-53-28.png)  
   
 After designing the layout we need to do layout vs schamatic for which we use netgen. Comp.out is the file result from Netgen. Here you should run both the netlist files generated from the schamitic and the layout. The result should show: **Circuits match uniquly** .  
 ![](https://github.com/Avs-Bharguav/VLSI-MINI-PROJECTS/blob/main/my_project/inverter_project_images/LVS_NETGEN/Screenshot%20from%202023-04-04%2012-27-09.png)  
 



## II. Characterisation of NMOS and PMOS.  




