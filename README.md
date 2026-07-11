# CMOS Circuit Design and SPICE Simulation using SKY130 Technology

## 📖 Overview

This repository documents my learning and implementation of CMOS circuit design and SPICE simulation using the SKY130 Process Design Kit (PDK). It includes theoretical concepts, circuit schematics, SPICE simulations, waveform analysis, and observations recorded throughout the course.

## 🎯 Objectives

- Understand MOSFET operation
- Learn CMOS circuit design
- Perform SPICE simulations
- Analyze circuit behavior
- 

# Day 1 - Basics of NMOS Drain Current (Id) vs Drain-to-Source Voltage (Vds)

## Introduction to Circuit Design and SPICE Simulations

### L1 Why do we need SPICE Simulations?

 - Circuit design involves creating logic gates by connecting **PMOS** and **NMOS** transistors in a specific configuration.
- The arrangement of these transistors determines the functionality and behavior of the circuit.
- CMOS circuit design forms the foundation of modern digital integrated circuits.
 <img width="412" height="290" alt="image" src="https://github.com/user-attachments/assets/627ab8a6-44cd-4951-b14c-1a6d6928a186" />
- SPICE simulations are used to optimize circuit performance by tuning parameters such as propagation delay.
- The transistor **Width-to-Length (W/L) ratio** can be adjusted during SPICE simulation to achieve the desired delay and performance characteristics.
- Optimizing the W/L ratio helps balance speed, power consumption, and circuit reliability before fabrication.
  <img width="502" height="430" alt="image" src="https://github.com/user-attachments/assets/6c174865-cc6b-45fb-ad2d-cd3d198d77dd" />







WHY DO WE NEED SPICE ????
  
  SPICE (Simulation Program with Integrated Circuit Emphasis) forms the foundation of many VLSI design stages, including **Clock Tree Synthesis (CTS)**, **timing analysis**, and **crosstalk analysis**. These analyses rely on accurate delay estimation obtained through SPICE simulations. Without circuit delays, physical design concepts such as timing closure, clock tree optimization, and crosstalk analysis would not be meaningful.

Consider a circuit that has undergone **Clock Tree Synthesis (CTS)**, where buffers are inserted to drive different capacitive loads at the outputs, as shown in the figure below.

<img width="923" height="283" alt="image" src="https://github.com/user-attachments/assets/467ea9f0-6c25-4f23-9cea-e212951a074e" />

Now we will create a delay table for CBUF1 if we want to create the delay of this particular cell we dont use spice everytime we already have a readymade dealy table which is the combination of input slew and output load the intersection of this is considered 

<img width="904" height="536" alt="image" src="https://github.com/user-attachments/assets/10061137-4142-4942-80c8-92881bb0fbde" />

the dealy table has different values for both the cells as both the bufferes have different pmos and nmos transisters 




Lets say we take the input slew of 40ps the corresponding output load is shown in the figure 


the output cap is 60fF but since we dont have the value 60fF so it will lie between 50fF and 70fF
so x9 and x10 are the desired value and somewhere between x9 and x10 lies the delay of CBUF1


<img width="929" height="477" alt="image" src="https://github.com/user-attachments/assets/6a57aa83-a766-4bb3-95eb-7bfd5ede567b" />

### L2 Introduction to Basic Element in Circuit Design - NMOS


**NMOS** stands for **N-Channel Metal-Oxide-Semiconductor**. It is a type of MOSFET (Metal-Oxide-Semiconductor Field-Effect Transistor) widely used in CMOS technology for digital circuit design.


<img width="914" height="533" alt="image" src="https://github.com/user-attachments/assets/23f99f2e-0956-40ae-b5e4-7d16ca9e1f9f" />


Few important points to note:
1) isolation region helps in differentiating between two transistors
2) the nmos consists of n+ source and drain area
3) the gate terminal is very important terminal in nmos
4) the body is usually not denoted while we are representing the symbol and it is usually grounded,any voltage from it tunes
the threshhold voltage
5) PMOS is just the converse of NMOS




### Threshold Voltage (VTH)

**Threshold Voltage (VTH)** is the minimum **Gate-to-Source Voltage (VGS)** required to create a conductive channel between the source and drain of an NMOS transistor. When **VGS** exceeds **VTH**, the transistor turns **ON** and current begins to flow.

### Working of an NMOS Transistor

An NMOS transistor has a **metal gate**, an **oxide layer (SiO₂)**, and a **p-type substrate**, making the gate electrically insulated from the semiconductor. Since the gate is separated by an oxide layer, it behaves like a **capacitor**, where the gate and substrate act as capacitor plates.

The source-body and drain-body junctions behave like **back-to-back PN junction diodes**. Under normal operation, these junctions remain reverse-biased, and current flow is controlled by the electric field created at the gate rather than by the PN junctions.

- **When VGS = 0 V:** No conductive channel exists between the source and drain. The holes remain near the surface of the p-type substrate, and the NMOS transistor remains **OFF**.
- **When VGS is positive:** The positive voltage applied to the gate repels holes away from the oxide interface and attracts electrons toward it. As **VGS** increases beyond the threshold voltage (**VTH**), an **inversion layer (n-channel)** is formed, creating a conducting path between the source and drain, allowing current to flow.

  <img width="958" height="479" alt="image" src="https://github.com/user-attachments/assets/aa0c7a93-98de-4d91-a766-9468ac855019" />



### L3 Strong Inversion and Threshold Voltage

IN SHORT 
- When a **positive Gate-to-Source Voltage (VGS)** is applied, holes (the majority charge carriers in the p-type substrate) are repelled away from the oxide interface.
- This creates a **depletion region**, where the positive charge carriers are depleted, similar to the depletion region formed in a **reverse-biased PN junction**.
- As **VGS** increases further, electrons are attracted towards the oxide interface. Once **VGS** exceeds the **threshold voltage (VTH)**, an **inversion layer (n-channel)** is formed, allowing current to flow between the source and drain.

  <img width="748" height="262" alt="image" src="https://github.com/user-attachments/assets/b84d7b00-ab50-4423-9253-d14e59caf86c" />

  When we increase the Vgs the depletion region width is increased and gets further increased , we reach a point where a small portion of a p-substrate gets
  convered into a n type substrate

  THIS IS CALLED STRONG INVERSION


  <img width="824" height="316" alt="image" src="https://github.com/user-attachments/assets/21429c31-1353-4dbc-af06-4592eba57762" />



  The voltage at which STRONG INVERSION occurs is called the THRESHOLD VOLTAGE



  - As **VGS** is increased further, the depletion region has already been depleted of its majority charge carriers and does not expand significantly.
- The additional positive gate voltage attracts more **electrons** from the **N+ source** towards the oxide interface, increasing the electron concentration in the channel.
- As a result, the **channel width increases**, enhancing the conductivity between the source and drain, while the depletion region remains nearly unchanged.


  <img width="739" height="260" alt="image" src="https://github.com/user-attachments/assets/f14fcc2a-6288-4a01-ade9-d97b118ac4c6" />


  - The application of a **positive Gate-to-Source Voltage (VGS)** creates a continuous **inversion channel** (or conductive path) between the source and drain.
- Although a channel is formed, **no current flows** through the transistor as long as **Drain-to-Source Voltage (VDS) = 0 V**, since there is no potential difference to drive the electrons.
- When a **positive VDS** is applied, electrons flow from the **source to the drain** through the inversion channel, resulting in drain current (**ID**).



<img width="959" height="522" alt="image" src="https://github.com/user-attachments/assets/2d20563a-15a0-4904-ad47-c6bd6d2df0eb" />

 Increasing the source-to-body voltage (VSB) increases the reverse bias of the source-body PN junction, which widens the depletion region and increases the threshold voltage (VTH).


 <img width="769" height="336" alt="image" src="https://github.com/user-attachments/assets/c1fd14ea-fa9f-4040-b334-799a2c10c672" />













        


