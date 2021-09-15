# DESIGN OF DIFFERENTIAL INPUT SINGLE ENDED OUTPUT SINGLE STAGE AMPLIFER

## Table of Contents
|#|TOPIC|
|:---:|:---:|
|1|[Design Specifications](#design-specifications)| 
|2|[Design Layout](#design-layout)| 
|3|[Self Biased Current Source Circuit](#self-biaed-current-source-circuit)| 
|4|[Simulations](#simulations)| 
|5|[Results](#results)| 

# DESIGN SPECIFICATIONS
To design a differential-input single-ended output Single-Stage amplifier, using CMOS 0.13um technology. The amplifier is powered from a 1.6V power supply. The amplifier to have one current source with a capacitive load as 4pF. 

![image](https://user-images.githubusercontent.com/89927660/132460294-baf97f76-9dec-48de-afca-807ad6965e90.png)

## _Design Considerations and Approach_
1)	The operational amplifier was designed using Folded-Cascode Topology due to its capability to output a higher impedance, therefore a higher dc gain. The process technology is CMOS 0.13um which has Lmin of 400nm. 
2)	While designing the transistors, larger transistor lengths (approximately 4 times Lmin = 1.6um) were considered so that the device will not be impacted by channel width modulation (λ). It is evident that the value of λ decreases for increasing value of channel length modulation parameter. The relationship is given by: λ ∝ 1/L.
3)	Given the value of VGS and VTH, each of the transistors (NMOS and PMOS) was put into saturation region by formulating VDS value greater than or equal to the overdrive voltage. Overdrive voltage is the difference between VGS and VTH. The below conditions were satisfied for each of the transistors. For NMOS:VDS ≥ VGS – VTH and For PMOS: VSD ≥ VSG – |VTH|.
4) Upon fixing the W/L ratio to achieve the specified Differential Gain, Phase Margin and Unity Gain Bandwidth, the ratio was further fine-tuned to meet the other design specifications. Especially for power consumption, the ratio was chosen so that the current flowing through each branch is reduced. 
5) The maximum rate at which the output of an Operational Amplifier can change is limited by the finite Bias Current. Due to the additional effect of parasitic capacitances, the W/L ratio of tail transistor was designed so that the bias current has additional leverage to obtain the required average slew rate. Average Slew Rate was calculated by taking the average between positive and negative slew rate. Average Slew Rate ∝ Bias Current/Load Capacitance.
6)	Lastly in the final design, the ideal current source of 25uA was replaced by self-biased current source. The current from startup circuit design is 25.12uA. The resistance value was hand calculated to match the desired current rating. 

## _Mathematical Gain Calculation_

![Screen Shot 2021-09-08 at 2 02 36 AM](https://user-images.githubusercontent.com/89927660/132462005-768ec35c-d7b6-472e-a132-bfcae3efec6c.png)

>_The W/L Ratio of the transistors were tuned to approximately match the mathematical voltage gain._

# DESIGN LAYOUT

![image](https://user-images.githubusercontent.com/89927660/133513238-43f22d80-3b8f-4eff-9574-a0da165051e0.png)

>_Firstly, DC analysis was performed to check if all the transistors were put into saturation region. This is essential to have a constant drain current, controlled by the gate-source voltage. The MOS device is useful only if operated in the saturation region._

## _Symbol_

![image](https://user-images.githubusercontent.com/89927660/133513279-48dfc816-c529-44dd-aabd-a183e1590baf.png)

# SELF BIASED CURRENT SOURCE CIRCUIT

An ideal current source is an independent current source that has high degree of precision and stability, independent of power supply and temperature variations. For greatly reducing the power supply sensitivity, self-biasing technique is used. Startup circuit is always needed in self-biasing to avoid zero current state. Also, the start-up circuit doesn’t interfere with the normal operation of the reference once the desired operating point is reached.  

After designing the amplifier to meet the desired specifications, in the final design, an attempt to design a self-biased current source was made.  The ideal current source (25uA) was replaced with self-biased current source circuit directly on the circuit schematic without creating extra symbol/pin. The current from the startup circuit design was found to be 25.12uA.

## _Schematic Layout_

![image](https://user-images.githubusercontent.com/89927660/133513322-89bdb880-b3a1-4bb2-b2f2-b0075e2d0b8e.png)

# SIMULATIONS

## _Offset Voltage_

When real amplifiers are connected in unity gain configuration (output voltage is negative input voltage), there will be a voltage difference between the positive and negative inputs called the offset voltage of the amplifier. This Voff was obtained by performing DC analysis and annotating the node voltages. 

![image](https://user-images.githubusercontent.com/89927660/133513360-a63e55a1-a628-4228-8b95-2de6e488623b.png)

### _Result: OFFSET VOLTAGE = 9.235mV_

## _Output Voltage Swing_

Output voltage swing is the range of output voltages that allow linear operation of output signals. The output swing was simulated using two voltage-controlled voltage sources (VCVS) with voltage gain 0.5 and -0.5 respectively. A linear sweep on VS dc voltage from -100mV to 100mV was performed in the DC Analysis.

![image](https://user-images.githubusercontent.com/89927660/133513411-7fd55ea7-9dfc-4efd-8510-e70e52a41e60.png)

The waveform shows a finite DC range (output swing) that the amplifier has a high output resistance for high differential gain.
OVSR = VO(max) – VO(min) = 1.32V – 220mV = 1.1 V

### _Result: OUTPUT VOLTAGE SWING RANGE (OVSR) = 1.1V_

## _Differential Mode Voltage Gain_

Differential Gain is the gain by which the amplifier boosts the difference of the input signals. The differential gain was obtained by performing AC Analysis, sweeping variable frequency from 1mHz to 1GHz.

![image](https://user-images.githubusercontent.com/89927660/133513427-0662ac4e-eece-44f9-bbb0-67fc46d1a113.png)		

![image](https://user-images.githubusercontent.com/89927660/133513498-f8b56ab4-b72c-4f06-b663-64103ebf0749.png)

### _Result: DIFFERENTIAL MODE VOLTAGE GAIN = 80.9dB_

## _Phase Margin and Unity Gain Bandwidth_

GBW is the maximum frequency of the input signal that amplifier provides a voltage gain higher than 1 (magnitude of 0 dB in log scale). Phase Margin is the difference between the phase of the gain at 0 dB and 180º.

![image](https://user-images.githubusercontent.com/89927660/133513527-cf51b099-d5a6-4b6a-8f8e-41f9fe0e0dcf.png)

Frequency at 0 dB gives the GBW. 

### _Result: UNITY GAIN BANDWIDTH (GBW) = 14.19 MHz_

f(GBW) = -95.1375º and Phase Margin (PM) = 180 + (-95.1375º) = 84.86º

### _Result: PHASE MARGIN (PM) = 84.86º_

## _Common Mode Rejection Ratio_

While the purpose of a differential amplifier is to amplify just the difference between the input signals, it also passes through some of the common-mode component of the input signal. The ability of amplifier to ignore the average of the two input signals is called the common mode rejection ratio (CMRR). Similar to differential gain AC response, the common mode gain was simulated. 

![image](https://user-images.githubusercontent.com/89927660/133513551-800eb9f0-ac55-4b16-a1cb-0aaccdfa3bbb.png)

![image](https://user-images.githubusercontent.com/89927660/133513565-bbc2b740-d62b-42a9-a4d9-859d98cb3a8d.png)

### _Result: Common Mode Gain = -34.1134º_

CMRR =  (Differential Mode Gain)/(Common Mode Gain)
CMRR =  20 log⁡((Differential Mode Gain)/(Common Mode Gain))                                         			    
= 80.9 – (–34.1134) = 115 dB

### _Result: Common Mode Rejection Ration (CMRR) = 115dB_

## _Transient Response_

The concept of finding the Average Slew Rate lies on measuring how close the output voltage waveform follows the input voltage waveform. While the positive slew rate occurs when the signal is rising, the negative slew rate occurs when the signal is falling. Slew rate is not related to frequency response. To find the average slew rate, transient response was performed by having a square wave input with unity gain amplifier configuration. 

![image](https://user-images.githubusercontent.com/89927660/133513601-494e37e2-bfe1-4db8-bc58-6795a603ce24.png)

![image](https://user-images.githubusercontent.com/89927660/133513663-b8f3b085-80a2-42a5-9aa1-66b801d0179e.png)

Average Slew Rate =  (positive SR + negative SR)/2 =  (10.298 + 10.3522)/2 
= 10.3251 MV/S or 10.3251 V/μS
Average Slew Rate (SR) = 10.3251 V/us

## _Power Dissipation_

The total current includes from all current mirrors and current source also. Power is product of current and supply voltage. The total current was also verified using simulation. 

![image](https://user-images.githubusercontent.com/89927660/133513693-3461afd9-0ae6-4ae0-acf9-1edcbc1d19b4.png)

Power Dissipation (P_diss )= Sum of currents flowing through all branches × VDD
						= 200.8 uA × 1.6 V 
						= 0.321 mW
Power Dissipation (PDISS) = 0.321 mW

# RESULTS 

![image](https://user-images.githubusercontent.com/89927660/132464470-93c167fb-d960-447a-82dc-9399d6281b98.png)
