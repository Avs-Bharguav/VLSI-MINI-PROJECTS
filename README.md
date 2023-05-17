# VLSI-MINI-PROJECTS
## CMOS Inverter Design using 180nm technology.
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



