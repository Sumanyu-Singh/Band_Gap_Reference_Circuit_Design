# BGR_Circuit_Design
A bandgap voltage reference is a temperature independent voltage reference circuit widely used in integrated circuits. It produces a fixed (constant) voltage regardless of power supply variations, temperature changes, or circuit loading from a device.

## Contents
------------
* [Problem Statement](#problem-statement)
* [Design of CTAT Reference Voltage](#design-of-ctat-reference-voltage)
  * [Schematic and Netlist](#schematic-and-netlist)
  * [Simulation Analysis for CTAT](#simulation-analysis-for-ctat)
* [Design of PTAT Reference Voltage](#design-of-ptat-reference-voltage)
  * [Schematic and Netlist](#schematic-and-netlist)
  * [Simulation Analysis for PTAT](#simulation-analysis-for-ptat)
* [Design of BGR Reference Voltage](#design-of-bgr-reference-voltage)
  * [Schematic and Netlist](#schematic-and-netlist)
  * [Simulation Analysis for BGR](#simulation-analysis-for-bgr)
* [Optimized BGR Circuit](#optimized-bgr-circuit)
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
   
## Simulation Analysis for CTAT
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

## Simulation Analysis for PTAT

![image](https://user-images.githubusercontent.com/100671647/234961152-18e8849e-1167-4398-819d-fde34252dcb3.png)

Below waveform shows Proportional To Absolute Temperature Plot and its Slope Calculation.

![image](https://user-images.githubusercontent.com/100671647/234961236-ebd7bc53-1877-4f8c-a188-b12967ecb54e.png)

## Design of BGR Reference Voltage
![image](https://user-images.githubusercontent.com/100671647/234962389-18475600-d974-414d-bd88-15714d00f857.png)
![image](https://user-images.githubusercontent.com/100671647/234962418-7c62caf1-5beb-49e8-b5bd-c5dfa5fb661c.png)
![image](https://user-images.githubusercontent.com/100671647/234962440-cac3f63c-7d23-4210-8139-ad90a0f3b90d.png)

Below is the comparison between CTAT and PTAT
![image](https://user-images.githubusercontent.com/100671647/234962537-3e0e4c71-406f-426b-8068-960f98d932ad.png)

## Schematic and Netlist
### Schematic
![image](https://user-images.githubusercontent.com/100671647/234962704-d2adcbf6-45b1-440c-be5a-385dedb2460f.png)

### Netlist

`````
Q1 0 0 VD1 0 2N2907
Q3 0 0 VD1 0 2N2907
Q2 0 0 CTAT 0 2N2907
Q4 0 0 E 0 2N2907
M1 2 3 V2 0 nch l=5u w=10u
M2 E 3 3 0 nch l=5u w=20u
M3 vdd 2 2 vdd pch l=5u w=40u M4 3 2 vdd vdd pch l=5u w=40u
M5 vdd 2 Vref vdd pch l=5u w=40u R2 Vref CTAT 40k
R1 V2 VD1 40
V1 vdd 0 1.8v
.model NPN NPN
.model PNP PNP
.model NMOS NMOS
.model PMOS PMOS
.dc V1 0 5 0.1
.include ptm_level_49_180nm.txt
.model 2N2907 PNP(IS=1E-14 VAF=120
+	BF=250 IKF=0.3 XTB=1.5 BR=3
+	CJC=8E-12 CJE=30E-12 TR=100E-9 TF=400E-12
+	ITF=1 VTF=2 XTF=3 RB=10 RC=.3 RE=.2 Vceo=40 Icrating=600m
mfg=Philips)
.include ptm_level_49_180nm.txt
.end

`````
## Simulation Analysis for BGR
![image](https://user-images.githubusercontent.com/100671647/234963112-788998d9-95b0-448b-8a2b-cbeb85c40936.png)
![image](https://user-images.githubusercontent.com/100671647/234963294-39f6b9db-f542-4ecc-b0fb-1654b032101c.png)

#### Below is the plot between Vref and Vdd which shows erroneous output Vref. So, we need to modify the W/L of BGR circuit to get the correct output.

![image](https://user-images.githubusercontent.com/100671647/234963565-d2daf056-a4ef-43c4-b952-08ee3df21f21.png)

So, after adjusting the W/L values for PMOS and NMOS we get the optimised output.

## Optimized BGR Circuit
![image](https://user-images.githubusercontent.com/100671647/234963675-11a8fbfe-f08c-4b8e-9276-fb88ecf76777.png)

### Optimised Vref v/s Vdd is as below
![image](https://user-images.githubusercontent.com/100671647/234963852-642bf206-6893-411c-815b-29c1382d9bb2.png)




------------------------------------------------------------------------------------------------------------------------------------------------------------------




