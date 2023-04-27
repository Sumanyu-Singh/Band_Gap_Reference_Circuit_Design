# BGR_Circuit_Design
A bandgap voltage reference is a temperature independent voltage reference circuit widely used in integrated circuits. It produces a fixed (constant) voltage regardless of power supply variations, temperature changes, or circuit loading from a device.

## Contents
------------
* [Problem Statement](#problem-statement)
* [Design of CTAT Reference Voltage](#design-of-ctat-reference-voltage)
  * [Schematic and Netlist](#schematic-and-netlist)
  * [Simulation Analysis](#simulation-analysis)
* [Design of PTAT Reference Voltage](#design-of-ptat-reference-voltage)
  * [Schematic and Netlist](#schematic-and-netlist)
  * [Simulation Analysis](#simulation-analysis)


---------
## Problem Statement
Implement a Band Gap reference Circuit, with Vref = 1.2 V, Temp. coefficient < = 200 ppm/0C (for the worst case). You can use any topology of your choice. Also, show Vout vs. VDD and minimize the effect of supply voltage variation in output voltage.

## Design of CTAT Reference Voltage
![image](https://user-images.githubusercontent.com/100671647/234956625-670ddf51-2e27-45dd-888d-d5f64c4d338c.png)
![image](https://user-images.githubusercontent.com/100671647/234956702-88ffc350-3743-4663-a1d9-f192ed0e3818.png)


## Schematic and Netlist
### Schematic
![image](https://user-images.githubusercontent.com/100671647/234956763-50a72a88-9de8-4a9a-9d61-4747501d1ed7.png)
### Netlist
`````
.model 2N2907 PNP(IS=1E-14 VAF=120
+	BF=250 IKF=0.3 XTB=1.5 BR=3
+	CJC=8E-12 CJE=30E-12 TR=100E-9 TF=400E-12
+	ITF=1 VTF=2 XTF=3 RB=10 RC=.3 RE=.2 Vceo=40 Icrating=600m
mfg=Philips) vdc VDD 0 1.8
Q§M1 0 0 CTAT 0 2N2907 IEp VDD CTAT 0.6
.model NPN NPN
.model PNP PNP
.dc temp -40 130 10

.end

`````
   
## Simulation Analysis
Below waveform shows Complementary To Absolute Temperature Plot.
![image](https://user-images.githubusercontent.com/100671647/234960474-f00f00bb-7291-492f-a045-3db7030694ce.png)

## Design of PTAT Reference Voltage 
![image](https://user-images.githubusercontent.com/100671647/234960660-d288864e-636f-4d1f-bac2-2b5d3837a2dc.png)
![image](https://user-images.githubusercontent.com/100671647/234960714-ba1cca9a-3f07-4e69-8a0e-36614a2e750d.png))

## Schematic and Netlist
### Schematic
![image](https://user-images.githubusercontent.com/100671647/234960787-4021a576-87c3-4523-b8b2-f30adff2772d.png)

### Netlist

`````
M8 VDD 1 PTAT VDD pch l=180n w=720n M6 VDD 1 1 VDD pch l=180n w=720n
M4 1 2 V2 0 nch l=180n w=180n
R2 PTAT 0 600 R1 V2 VD1 40
Q§M3 0 0 VD1 0 2N2907
Q§M1 0 0 VD 0 2N2907
Q§M2 0 0 VD1 0 2N2907
vdc VDD 0 1.8
M5 2 2 VD 0 nch l=180n w=180n
M7 VDD 1 2 VDD pch l=180n w=720n
.model NPN NPN
.model PNP PNP
.model NMOS NMOS
.model PMOS PMOS
.dc temp -40 130 10
.include ptm_level_49_180nm.txt


.model 2N2907 PNP(IS=1E-14 VAF=120
+	BF=250 IKF=0.3 XTB=1.5 BR=3
+	CJC=8E-12 CJE=30E-12 TR=100E-9 TF=400E-12
+	ITF=1 VTF=2 XTF=3 RB=10 RC=.3 RE=.2 Vceo=40 Icrating=600m
mfg=Philips)
.op
.end

`````

## Simulation Analysis
![image](https://user-images.githubusercontent.com/100671647/234961152-18e8849e-1167-4398-819d-fde34252dcb3.png)

Below waveform shows Proportional To Absolute Temperature Plot and its Slope Calculation.

![image](https://user-images.githubusercontent.com/100671647/234961236-ebd7bc53-1877-4f8c-a188-b12967ecb54e.png)

------------------------------------------------------------------------------------------------------------------------------------------------------------------




