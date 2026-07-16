# CMOS Circuit Design and SPICE Simulation using SKY130 Technology

## 📖 Overview

This repository documents my learning and implementation of CMOS circuit design and SPICE simulation using the SKY130 Process Design Kit (PDK). It includes theoretical concepts, circuit schematics, SPICE simulations, waveform analysis, and observations recorded throughout the course.

## 🎯 Objectives

- Understand MOSFET operation
- Learn CMOS circuit design
- Perform SPICE simulations
- Analyze circuit behavior

# Table Of Contents

- **Introduction to Circuit Design and SPICE Simulations**
  - [L1 Why do we need SPICE Simulations?](#l1-why-do-we-need-spice-simulations)
  - [L2 Introduction to Basic Element in Circuit Design - NMOS](#l2-introduction-to-basic-element-in-circuit-design---nmos)
  - [L3 Strong Inversion and Threshold Voltage](#l3-strong-inversion-and-threshold-voltage)
  - [L4 Threshold Voltage with Positive Substrate Potential](#l4-threshold-voltage-with-positive-substrate-potential)

- **NMOS Resistive Region and Saturation Region of Operation**
  - [L1 Resistive Region of Operation with Small Drain-Source Voltage](#l1-resistive-region-of-operation-with-small-drain-source-voltage)
  - [L2 Drift Current Theory](#l2-drift-current-theory)
  - [L3 Drain Current Model for Linear Region of Operation](#l3-drain-current-model-for-linear-region-of-operation)
  - [L4 SPICE Conclusion to Resistive Operation](#l4-spice-conclusion-to-resistive-operation)
  - [L5 Pinch-Off Region Condition](#l5-pinch-off-region-condition)
  - [L6 Drain Current Model for Saturation Region of Operation](#l6-drain-current-model-for-saturation-region-of-operation)

- **Introduction to SPICE**
  - [L1 Basic SPICE Setup](#l1-basic-spice-setup)
  - [L2 Circuit Description in SPICE Syntax](#l2-circuit-description-in-spice-syntax)
  - [L3 Define Technology Parameters](#l3-define-technology-parameters)
  - [L4 First SPICE Simulation](#l4-first-spice-simulation)

- **SPICE Simulation**
  - [L1 SPICE Simulation for Lower Nodes](#l1-spice-simulation-for-lower-nodes)
  - [L2 Drain Current vs Gate Voltage for Long and Short Channel Device](#l2-drain-current-vs-gate-voltage-for-long-and-short-channel-device)
  - [L3 Velocity Saturation under Low and High Electric Fields](#l3-velocity-saturation-under-low-and-high-electric-fields)
  - [L4 Drain Current Model under Velocity Saturation](#l4-drain-current-model-under-velocity-saturation)
  - [L5 SKY130 Lab: Id–VGS Characteristics](#l5-sky130-lab-idvgs-characteristics)

- **CMOS Voltage Transfer Characteristics (VTC)**
  - [L1 MOSFET as a Switch](#l1-mosfet-as-a-switch)
  - [L2 Introduction to Standard MOS Voltage Current Parameters](#l2-introduction-to-standard-mos-voltage-current-parameters)
  - [L3 PMOS/NMOS Drain Current vs Drain Voltage](#l3-pmosnmos-drain-current-vs-drain-voltage)
  - [L4 Step1 – Convert PMOS Gate-Source Voltage to Vin](#l4-step1--convert-pmos-gate-source-voltage-to-vin)
  - [L5 Step2 & Step3 – Convert PMOS and NMOS Drain-Source Voltage to Vout](#l5-step2--step3--convert-pmos-and-nmos-drain-source-voltage-to-vout)
  - ### [L6 Step4 – Merge PMOS-NMOS Load Curves and Plot VTC](#l6-step4--merge-pmos-nmos-load-curves-and-plot-vtc)

- **Voltage Transfer Characteristics (VTC) – SPICE Simulations**
  - [L1 SPICE Deck Creation for CMOS Inverter](#l1-spice-deck-creation-for-cmos-inverter)
  - [L2 SPICE Simulation for CMOS Inverter](#l2-spice-simulation-for-cmos-inverter)
  - [L3 Labs SKY130 SPICE Simulation for CMOS](#l3-labs-sky130-spice-simulation-for-cmos)

- **Static Behaviour Evaluation – CMOS Inverter Robustness (Switching Threshold)**
  - [L1 Switching Threshold, Vm](#l1-switching-threshold-vm)
  -  [L2 Analytical Expression of Vm as a Function of (W/L)p and (W/L)n](#l2-analytical-expression-of-vm-as-a-function-of-wlp-and-wln)
  - [L3 Analytical Expression of (W/L)p and (W/L)n as a Function of Vm](#l3-analytical-expression-of-wlp-and-wln-as-a-function-of-vm)
  - [L4 Static and Dynamic Simulation of CMOS Inverter](#l4-static-and-dynamic-simulation-of-cmos-inverter)
  - [L5 Static and Dynamic Simulation of CMOS Inverter with Increased PMOS Width](#l5-static-and-dynamic-simulation-of-cmos-inverter-with-increased-pmos-width)
  -  [L6 Applications of CMOS Inverter in Clock Network and STA](#l6-applications-of-cmos-inverter-in-clock-network-and-sta)

- **Static Behaviour Evaluation – CMOS Inverter Robustness (Noise Margin)**
  - [L1 Introduction to Noise Margin](#l1-introduction-to-noise-margin)
  - [L2 Noise Margin Voltage Parameters](#l2-noise-margin-voltage-parameters)
  - [L3 Noise Margin Equation and Summary](#l3-noise-margin-equation-and-summary)
  - [L4 Noise Margin Variation with Respect to PMOS Width](#l4-noise-margin-variation-with-respect-to-pmos-width)
  - [L5 SKY130 Noise Margin Labs](#l5-sky130-noise-margin-labs)

- **Static Behaviour Evaluation – CMOS Inverter Robustness (Power Supply Variation)**
  - [L1 Smart SPICE Simulation for Power Supply Variations](#l1-smart-spice-simulation-for-power-supply-variations)
  - [L2 Advantages and Disadvantages Using Low Supply Voltage](#l2-advantages-and-disadvantages-using-low-supply-voltage)
  - [L3 SKY130 Supply Variation Labs](#l3-sky130-supply-variation-labs)

- **Static Behaviour Evaluation – CMOS Inverter Robustness (Device Variation)**
  - [L1 Sources of Variation – Etching Process](#l1-sources-of-variation--etching-process)
  - [L2 Sources of Variation – Oxide Thickness](#l2-sources-of-variation--oxide-thickness)
  - [L3 Smart SPICE Simulation for Device Variations](#l3-smart-spice-simulation-for-device-variations)
  - [L4 Conclusion](#l4-conclusion)





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



 ### L4 Threshold Voltage with Positive Substrate Potential


 <img width="958" height="548" alt="image" src="https://github.com/user-attachments/assets/b422a90c-fcce-4356-871e-c8feb1bfeb9f" />


 HERE IN THE IMAGE WE OBSERVE 2 SENARIOS 
 1) Vsb=0
 2) Vsb=POSITIVE

Here we will try an observe what will happen to the depletion region as we apply more positive Vsb

<img width="724" height="316" alt="image" src="https://github.com/user-attachments/assets/efd71fcb-a24c-4e30-a274-f2ba08f9205f" />

***  notice the marked red colour of the depletion region (the depletion region area is changing)

- When **VSB = 0 V**, the inversion channel is formed once **VGS** exceeds the threshold voltage, allowing electrons to accumulate beneath the gate oxide.

- When a **positive substrate-to-source voltage (VSB)** is applied, the **source-body PN junction becomes more reverse biased**, widening the depletion region near the source. As a result, some electrons that would contribute to the channel are pulled away, making channel formation more difficult.

- Since a stronger gate electric field is now required to attract enough electrons and establish the inversion layer, the **threshold voltage (VTH) increases**. Therefore, a **higher VGS** is required to turn the NMOS transistor ON.

  <img width="757" height="350" alt="image" src="https://github.com/user-attachments/assets/b9f3d086-1def-4eb3-94f0-0618b8bcc815" />


  




<img width="953" height="475" alt="image" src="https://github.com/user-attachments/assets/a404b8c8-918a-4aee-91fb-bc8a8a252a70" />

OBSERVE THE MARKED RED REGIONS IN SENARIO 1 AND 2

- In **Scenario 1 (VSB = 0 V)**, **surface inversion** occurs at a relatively **lower Gate-to-Source Voltage (VGS)**, allowing the inversion channel to form easily.

- As **VGS** is increased further, the inversion layer becomes fully established, creating a strong conductive channel between the source and drain.

- In **Scenario 2 (VSB > 0 V)**, the increased reverse bias widens the depletion region, making it more difficult to achieve surface inversion. Consequently, the same **VGS** that produces a strong inversion in Scenario 1 is **insufficient** in Scenario 2, and a **higher VGS** is required to fully form the inversion channel.


- To achieve **surface inversion** under a positive substrate bias, the **Gate-to-Source Voltage (VGS)** must be increased further.
- Surface inversion now occurs at a higher threshold voltage, which can be expressed as **VT = VT0 + V1**, where **VT0** is the threshold voltage with **VSB = 0 V**, and **V1** is the additional voltage required due to the positive substrate bias (body effect).
- Therefore, an extra gate voltage (**V1**) is needed to overcome the increased depletion region and establish a strong inversion channel.

 <img width="959" height="530" alt="image" src="https://github.com/user-attachments/assets/8a7c1a95-6e86-448c-bb88-1881f2313de5" />



  - To achieve **surface inversion** under a positive substrate bias, the **Gate-to-Source Voltage (VGS)** must be increased further.
- Surface inversion now occurs at a higher threshold voltage, which can be expressed as **VT = VT0 + V1**, where **VT0** is the threshold voltage with **VSB = 0 V**, and **V1** is the additional voltage required due to the positive substrate bias (body effect).
- Therefore, an extra gate voltage (**V1**) is needed to overcome the increased depletion region and establish a strong inversion channel.

  THRESHOLD VOLTAGE EQUATIONS

<img width="770" height="331" alt="image" src="https://github.com/user-attachments/assets/8cc9d109-750b-44d9-b961-6592774ac7ad" />


- SPICE uses technology parameters such as the **substrate doping concentration (NA)**, **silicon permittivity (εsi)**, **electron charge (q)**, **oxide capacitance (Cox)**, and **intrinsic carrier concentration (ni)** to calculate the threshold voltage (**VTH**) of a MOSFET.
- By providing these parameters in the SPICE model, the simulator automatically computes the threshold voltage and accurately predicts the transistor's electrical behavior under different operating conditions.

  <img width="440" height="293" alt="image" src="https://github.com/user-attachments/assets/3d4ccf63-4b69-4a09-be9b-be8e4224a167" />

  ## NMOS Resistive Region and Saturation Region of Operation

  ### L1 Resistive Region of Operation with Small Drain-Source Voltage

  - In the **resistive (linear) region of operation**, the **Gate-to-Source Voltage (VGS)** must be **greater than the Threshold Voltage (VTH)** to establish an inversion channel.
 
We shall observe how the channel width increases with increase in Vgs 
1) Vgs=1V


<img width="686" height="421" alt="image" src="https://github.com/user-attachments/assets/f28ade6e-01e0-41d2-8c9a-4e05ad2d9a5f" />


2) Vgs=1.5V

<img width="433" height="252" alt="image" src="https://github.com/user-attachments/assets/75440551-6f5f-4dc8-8024-a8c09a839371" />

3)Vgs=2V

<img width="414" height="274" alt="image" src="https://github.com/user-attachments/assets/8494874d-7e1d-4bc8-9f26-755676989bde" />

What can we conclude from this ?
  The charges accumulated in this area is propotional to (Vgs-Vth)

  Now let's apply very small Vds at start. And keep Vt=0.45V, Vgs also small initially.

  <img width="593" height="267" alt="image" src="https://github.com/user-attachments/assets/14791e13-f708-4315-afd6-db0d79dd491a" />



  We can see that there is a voltage gradient as soon as we apply Vds 

  <img width="440" height="314" alt="image" src="https://github.com/user-attachments/assets/4c50f621-d64c-40db-b40c-762bc91ab1ec" />


  
  

Here we plot a graph x axis-along the chanel
                        y-axis perpendicular to the chanel 

                        
  <img width="449" height="323" alt="image" src="https://github.com/user-attachments/assets/4c57d4fb-3b49-454a-9c40-757ec1d15415" />

### L2 Drift Current Theory

As we move along the channel, the **effective channel voltage** varies with the position **x**.

- At the **source (x = 0)**, the channel voltage is minimum, resulting in the **maximum effective gate-to-channel voltage**.
- As we move towards the **drain (x = L)**, the channel voltage gradually increases, reducing the effective gate-to-channel voltage.
- Since the induced inversion charge depends on the effective gate voltage, the **channel charge gradually decreases from the source towards the drain**.


<img width="768" height="331" alt="image" src="https://github.com/user-attachments/assets/92c8bc45-f019-4803-888f-c8cb253a9d31" />


The figure above shows the first-order analysis of the induced channel charge. It also highlights the parameters that influence the channel charge, such as the **gate oxide capacitance (Cox)**, **oxide thickness (tox)**, and **oxide permittivity (εox)**.

---

Current flow in a MOSFET can occur through **two mechanisms**:

- **Drift Current** – Caused by the electric field (potential difference) across the channel.
- **Diffusion Current** – Caused by the difference in carrier concentration.

Since a small **Drain-to-Source Voltage (VDS)** is applied in the **resistive (linear) region**, the dominant mode of current conduction is **drift current**.

<img width="952" height="473" alt="image" src="https://github.com/user-attachments/assets/e1c7faff-0c28-4dde-8e3a-c10b32f23982" />


To understand the drain current, we can visualize the transistor from its **top view**. The drain current mainly depends on:

- The velocity of the charge carriers.
- The amount of inversion charge available in the channel.
- The effective channel width (**W**).

An increase in any of these parameters results in a higher drain current.

<img width="958" height="572" alt="image" src="https://github.com/user-attachments/assets/53017864-275c-4fdd-a154-9b37fdd90d3c" />

### L3 Drain Current Model for Linear Region of Operation

The drain current depends on the movement of charge carriers through the inversion channel. Since the channel potential varies from the source to the drain, the **carrier velocity** also changes along the channel.

<img width="857" height="394" alt="image" src="https://github.com/user-attachments/assets/9e6c5323-9007-486a-b239-2ae46626be29" />


The carrier velocity is influenced by:

- Carrier mobility (**μn**)
- Electric field across the channel

Using these relationships, the drain current equation can be derived by combining the induced channel charge and carrier velocity.

---

The drain current equation is obtained by integrating over:

- **Channel length (L)** on the left-hand side.
- **Drain-to-Source Voltage (VDS)** on the right-hand side.

This integration results in the drain current expression for an NMOS transistor operating in the **linear (resistive) region**.

<img width="799" height="385" alt="image" src="https://github.com/user-attachments/assets/3845888b-8e19-46cb-bf7b-6fbf34da9e12" />


The final drain current equation depends on several technology and design parameters, including:

- Gate oxide capacitance (**Cox**)
- Width-to-Length ratio (**W/L**)
- Gate-to-Source Voltage (**VGS**)
- Threshold Voltage (**VTH**)
- Electron mobility (**μn**)

These parameters are provided to **SPICE**, which uses them to accurately predict the transistor characteristics.

 

Although the drain current expression contains a quadratic term (**VDS²**), in the linear region the applied **VDS** is very small compared to **(VGS − VTH)**.

Therefore, the **VDS²** term becomes negligible, simplifying the drain current equation.

<img width="529" height="314" alt="image" src="https://github.com/user-attachments/assets/7ba975cf-940b-4b90-bd22-d580a4fbfc5e" />


For an NMOS transistor to operate in the **linear (resistive) region**, the following condition must be satisfied:

- **(VGS − VTH) ≥ VDS**

Under this condition, the drain current becomes approximately **linearly proportional to VDS**, which is why this region is known as the **linear** or **resistive** region of operation.

<img width="518" height="311" alt="image" src="https://github.com/user-attachments/assets/8a7c26cc-1635-4ef6-98c6-09c3f0954068" />


### L4 SPICE Conclusion to Resistive Operation

To understand the behavior of an NMOS transistor in the **linear (resistive) region**, we need to analyze how the **Gate-to-Source Voltage (VGS)** and **Drain-to-Source Voltage (VDS)** affect the drain current.

For every selected value of **VGS**, the transistor remains in the **linear region** only if the following condition is satisfied:

- **(VGS − VTH) ≥ VDS**

<img width="950" height="531" alt="image" src="https://github.com/user-attachments/assets/72c5d0ea-20f3-4636-ad17-4e6295ced293" />


For different values of **VGS**, the maximum allowable **VDS** changes accordingly. Therefore, to obtain the drain current characteristics, **VDS** is swept from **0 V** up to **(VGS − VTH)** while keeping **VGS** constant.

Instead of manually calculating the drain current for every combination of **VGS** and **VDS**, **SPICE simulations** are used to automate the process. The simulator computes the drain current for different operating conditions and generates the corresponding characteristics efficiently.

<img width="743" height="305" alt="image" src="https://github.com/user-attachments/assets/a299b9b1-ad24-4542-aaae-3a4a7580e9c5" />

### L5 Pinch-Off Region Condition

As the **Drain-to-Source Voltage (VDS)** is gradually increased, the effective channel voltage near the drain decreases. Eventually, the transistor transitions from the **linear region** to the **saturation region**.

<img width="596" height="292" alt="image" src="https://github.com/user-attachments/assets/f4a13dfb-a0ca-44ff-befa-4be74a3d7240" />


Initially, the effective channel voltage (**VGS − VDS**) is greater than the threshold voltage (**VTH**). Therefore, a continuous inversion channel exists between the source and drain, allowing current to flow.

---

As **VDS** is increased further, the effective channel voltage at the drain gradually decreases. When the condition

- **VGS − VDS = VTH**

is reached, the inversion layer at the drain end becomes extremely thin, marking the beginning of the **pinch-off condition**.

<img width="584" height="268" alt="image" src="https://github.com/user-attachments/assets/178b7017-3998-4088-8bb9-4e02751caed7" />

At this point, the channel starts disappearing from the drain side, while the rest of the channel remains conductive.

---

If **VDS** is increased even further, the effective channel voltage becomes less than the threshold voltage:

- **VGS − VDS < VTH**

As a result, no inversion channel exists near the drain, and the transistor enters the **saturation region of operation**.

<img width="585" height="259" alt="image" src="https://github.com/user-attachments/assets/70de2adb-9100-4f0d-acd3-19e39008d177" />


Although the channel is pinched off near the drain, current continues to flow because the strong electric field in the pinch-off region sweeps electrons from the channel into the drain.

The condition for **pinch-off** can therefore be written as:

- **VGS − VDS ≤ VTH**

<img width="275" height="70" alt="image" src="https://github.com/user-attachments/assets/00ade7c7-2f3f-4be6-a9f4-df357ca224a0" />


### L6 Drain Current Model for Saturation Region of Operation

In the **saturation region**, the drain current no longer varies linearly with **VDS**. Once the transistor reaches pinch-off, the channel voltage remains fixed at **(VGS − VTH)**, and the drain current primarily depends on the gate voltage.

To derive the drain current equation for the saturation region, **VDS** is replaced with **(VGS − VTH)** in the linear region equation.

<img width="321" height="245" alt="image" src="https://github.com/user-attachments/assets/e37cea32-2219-4e3e-b9ed-6e260f32f5c3" />


The resulting equation shows that the drain current is proportional to the square of **(VGS − VTH)**. At first glance, this suggests that the drain current is **independent of VDS**, making the MOSFET appear to behave like an **ideal current source**.

---

However, in a practical MOSFET, this assumption is not entirely accurate.

As **VDS** increases further, the **depletion region near the drain expands**, causing the effective channel length to become shorter. Since the conducting channel is reduced, a slight increase in drain current is observed even in the saturation region.

This phenomenon is known as **Channel Length Modulation (CLM).**

<img width="593" height="227" alt="image" src="https://github.com/user-attachments/assets/630401e3-20ef-44e5-96cf-5c1774937a07" />


To account for this effect, the ideal saturation current equation is modified by introducing the **Channel Length Modulation parameter (λ)**.

The updated equation provides a more accurate representation of the drain current in practical MOSFETs by including the slight dependence of **ID** on **VDS**.

<img width="608" height="112" alt="image" src="https://github.com/user-attachments/assets/b170a5c3-ac83-4be5-a9bb-e77d3d771241" />


### L1 Basic SPICE Setup

Before performing any simulations, the analytical equations derived for the MOSFET must be translated into a format that the **SPICE simulator** can understand.


<img width="631" height="265" alt="image" src="https://github.com/user-attachments/assets/054da0b1-6674-46b6-a3da-b9e6153c9398" />


The threshold voltage equation, linear region equation, and saturation region equation are used by SPICE along with the corresponding **technology parameters** to predict the electrical behavior of the MOSFET.

---

The simulator requires several **SPICE model parameters**, such as the body-effect coefficient (**γ**), process transconductance (**kn**), and channel length modulation parameter (**λ**). These parameters define the characteristics of the fabrication technology and allow SPICE to accurately model the device.


<img width="417" height="431" alt="image" src="https://github.com/user-attachments/assets/cd559f15-6288-4f07-9fc0-6a60f2c71d81" />


To perform a simulation, the MOSFET must be represented as a **SPICE netlist**, which is a text-based description of the circuit. The netlist specifies the device connections, power supplies, input sources, and component values, enabling SPICE to analyze the circuit and generate the required output characteristics.


<img width="415" height="196" alt="image" src="https://github.com/user-attachments/assets/06f595f5-1e48-497c-93f3-6095e1881368" />


### L2 Circuit Description in SPICE Syntax

To simulate a circuit using **SPICE**, the circuit must first be described using a **SPICE netlist**. A netlist is a text-based representation of the circuit that defines all the components, their connections, and their electrical properties.

The first step in writing a SPICE netlist is to **identify and define the circuit nodes**.


<img width="532" height="307" alt="image" src="https://github.com/user-attachments/assets/7ea38b2b-3ac3-489b-bb8c-6c189bbdb78b" />


Each node in the circuit is assigned a unique name so that SPICE can determine how different components are interconnected. Since every component is connected between one or more nodes, correctly defining the nodes is essential for accurate circuit simulation.

---

A MOSFET has **four terminals**:

- Drain (D)
- Gate (G)
- Source (S)
- Substrate/Bulk (B)

Therefore, while writing the MOSFET statement in the netlist, the four node names must be specified in the following order:

**Drain → Gate → Source → Substrate (DGSS)**


<img width="538" height="184" alt="image" src="https://github.com/user-attachments/assets/dfd93d39-fb49-4148-bf38-02ac517e43c2" />


<img width="592" height="180" alt="image" src="https://github.com/user-attachments/assets/313f2579-f6f1-432e-8bf8-800a0962f7ef" />


<img width="573" height="181" alt="image" src="https://github.com/user-attachments/assets/6cd46dee-cbdd-47a3-93bb-50bdd58a3269" />



After specifying the terminal connections, the **MOSFET model name** and its physical dimensions (**Width** and **Length**) are included. These parameters determine the electrical characteristics of the device during simulation.

---

The same approach is followed for other circuit elements.

For a resistor, the SPICE syntax specifies:

- Resistor name
- Two connected nodes
- Resistance value (in ohms)

Similarly, for voltage sources, the netlist defines:

- Voltage source name
- Connected nodes
- Applied voltage value



<img width="579" height="194" alt="image" src="https://github.com/user-attachments/assets/75cc71ce-859f-41b5-bc90-c10c97353835" />


<img width="576" height="193" alt="image" src="https://github.com/user-attachments/assets/b59de5bc-c80b-4f56-99ff-108e26c55654" />


<img width="584" height="355" alt="image" src="https://github.com/user-attachments/assets/0deff794-02bf-412b-bd52-d8a64cace808" />


<img width="527" height="158" alt="image" src="https://github.com/user-attachments/assets/bb98a2f0-bfec-4301-bff2-4133c498c44c" />


<img width="404" height="237" alt="image" src="https://github.com/user-attachments/assets/5f5bb8b0-bcd3-4f0e-ab96-bfc3c70600bb" />








Once all the components have been defined, the complete **SPICE netlist** is ready. This netlist serves as the input to the SPICE simulator, which analyzes the circuit and generates the required electrical characteristics.



### L3 Define Technology Parameters

To accurately simulate an NMOS transistor, SPICE requires a **technology model** that contains all the device-specific parameters. Instead of manually specifying every parameter, SPICE uses a **technology file** that stores the complete MOSFET model.


<img width="581" height="280" alt="image" src="https://github.com/user-attachments/assets/fdbfa4a8-839d-4bb9-a5d1-11c29d576ccb" />


The MOSFET model name specified in the SPICE netlist is linked to the corresponding model definition in the technology file. This model contains important parameters such as threshold voltage, oxide thickness, carrier mobility, body-effect coefficient, and other technology-specific values.

---

Both **NMOS** and **PMOS** devices have their own model definitions. Each model includes a set of technology parameters that describe the electrical characteristics of the transistor.


<img width="390" height="77" alt="image" src="https://github.com/user-attachments/assets/6f590d3f-108e-4288-ad60-27ed60165554" />


Rather than writing these model parameters in every netlist, they are packaged into a separate **`.mod` (model)** file. This makes the circuit description simpler, reusable, and easier to maintain.

---

The technology file is then linked to the main SPICE netlist using the **`.LIB`** or **`.include`** statement. During simulation, SPICE reads this file and automatically loads all the required technology parameters for the selected MOSFET model.


<img width="381" height="344" alt="image" src="https://github.com/user-attachments/assets/fa888d17-67db-4452-9910-95c97a048a0e" />


<img width="438" height="148" alt="image" src="https://github.com/user-attachments/assets/91f5ca89-f7c7-4a7a-9626-49e4d849daaa" />



Comments can also be added to the SPICE netlist to improve readability and document different sections of the circuit description. These comments are ignored by the SPICE simulator during execution.


<img width="437" height="170" alt="image" src="https://github.com/user-attachments/assets/6db5b753-e51c-4da9-99b5-6aa30c25cd8f" />


Once the technology file has been included successfully, the SPICE netlist is complete and ready for performing simulations such as voltage sweeps, current analysis, and waveform generation.


### L4 First SPICE Simulation
Open Virtual Box
Type cd
Go to the browser and search for the github link of the sky workshop 
git clone https://github.com/kunalg123/sky130CircuitDesignWorkshop.git


<img width="733" height="173" alt="image" src="https://github.com/user-attachments/assets/19269185-842b-4b6a-8cb4-977291317d2d" />

here we can see that the contents of the skyworkshop is downloaded 
in order to check what all is present we give the commands as shown in the picture 


<img width="803" height="47" alt="image" src="https://github.com/user-attachments/assets/99c68051-6ecc-4ee8-b6cb-1edf7b0a4dd5" />

here we can see the files present in nfet_01v8



<img width="959" height="521" alt="image" src="https://github.com/user-attachments/assets/57ba11fc-91a7-4a0d-b276-6f9028d2f599" />

these are the model parameters present in nfet



<img width="950" height="537" alt="image" src="https://github.com/user-attachments/assets/27943d83-3e9c-43ab-8dc7-1641dac822a2" />

the corner spice file contains different W and L values 
In sky130 technology it has already presetted the w and l values we need to use these W and L values only
IF WE TAKE VALUES OUTSIDE THIS SET IT WONT SIMULATE 



<img width="959" height="540" alt="image" src="https://github.com/user-attachments/assets/2363c33f-eb61-4140-9fce-7bf6fd2849da" />

This is the common file for both nfet and pfet at different corners 
Here we are including corner spice files of both nfet and pfet 





Now open the day 1 file 

Here you can see the library file is included and its mentioned as tt(typical corner) if we want to do it at slow fast corner we need to 
change it to sf 

<img width="956" height="491" alt="image" src="https://github.com/user-attachments/assets/cca15b51-37bd-4801-b5c2-466b7a3b16de" />


<img width="956" height="491" alt="image" src="https://github.com/user-attachments/assets/7751cb68-be95-48d7-9ac4-e5f53ce3aa3f" />
Here this is the model name for nfet_01v8 
syntax is (drain,gate,source and bulk)

Here we are doing DC simulation of Id vs Vd

<img width="663" height="333" alt="image" src="https://github.com/user-attachments/assets/2a3be9d1-f6ea-4b7d-86b2-2428c2f0272c" />

If we want to see the value of Id at one particular point 
just press on it and left click


### L1 SPICE Simulation for Lower Nodes

We observed the Id VS Vd Curve 

Now we will Observe at different Vd values 


<img width="933" height="530" alt="image" src="https://github.com/user-attachments/assets/48f0f32f-c333-4dc2-980e-3cb75aa19353" />



We have drawn a line as the behavior of the nmos is diffrent in area 1 and area 2 

<img width="1700" height="925" alt="ChatGPT Image Jul 13, 2026, 09_26_05 AM" src="https://github.com/user-attachments/assets/5faedc5b-765a-4b49-80cd-5c14acc05238" />


In Area 1:The drain current is linear funtion of Vds 
In Area 2:the drain current is function of 1+λVds


<img width="949" height="547" alt="image" src="https://github.com/user-attachments/assets/bf12b9ad-a2bd-4b40-b395-8821887a70be" />

Here we can see the different equations of linear and saturation region 


We Plot the Id vs Vd curve for different values of W and L 
W-0.375u AND L=0.25u   (W/L=1.5)


<img width="695" height="349" alt="image" src="https://github.com/user-attachments/assets/f6b2a98a-41cc-422e-8c5c-05cc6d64325f" />

Notice the (-) symbol there its because of the conventional current flow v/s flow of electrons

Now we will see the difference between the two curves we plotted briefly

<img width="958" height="585" alt="image" src="https://github.com/user-attachments/assets/204f762c-001d-4ab0-ad01-bc0133fdd6b3" />

1)The saturation current is higher for the larger device (W = 1.8 μm, L = 1.2 μm).
2)The spacing between adjacent saturation current levels is more uniform for the smaller device (W = 0.375 μm, L = 0.25 μm).
3)Increasing the device width increases the saturation current and reduces the uniformity of the spacing between adjacent current levels.

## L2: Drain Current vs Gate Voltage for Long and Short Channel Device

For the long channel device the drain current at each and every gate voltage keeping Vds=2.5v has a "QUADRATIC DEPENDENCE"
Here we observe that it does *NOT LINEARLY INCREASE* with Vgs

We can see that the equations we have derived also suggests the same thing 
<img width="959" height="527" alt="image" src="https://github.com/user-attachments/assets/432c0fcc-3041-44b4-a59e-d87f96a7eca6" />


We can observe that for short channel device the drain current has *LINEAR DEPENDENCE*
<img width="503" height="419" alt="image" src="https://github.com/user-attachments/assets/cd7f12dd-d235-4e98-97e2-538ec1a50f1a" />

BUT WHY IS THIS HAPPENING ??
ANS:  BECAUSE OF VELOCITY SATURATION EFFECT 

WE WILL TRY TO PLOT THE GRAPH 

The only difference is vary your Vgs from 0 to 2.5 at the step count of 0.1V and Vdd is swept from 0 to 2.5 

SYNTAX: whatever is there in the left hand side will be sweeped or tuned at every value of what you see in the right hand side


<img width="377" height="211" alt="image" src="https://github.com/user-attachments/assets/566e8503-5b6b-4644-9627-12f237047962" />



If we plot the grpah for long chanel and short chanel

<img width="959" height="481" alt="image" src="https://github.com/user-attachments/assets/5bb15ea2-f1ae-4b75-98c2-3714ff21de4d" />

image 1: Short Channel: if we observe it the ID is increasing linearly 
image 2: long channel : if we obsereve it the ID has QUADRATIC DEPENDENCE


### L3 Velocity Saturation under Low and High Electric Fields

We can clearly observe the difference between long channel and short channel nmos

<img width="959" height="557" alt="image" src="https://github.com/user-attachments/assets/00604aee-acb2-4697-bcc7-75c01d638f51" />

VELOCITY SATURATION EFFECT

- At low electric fields, the carrier velocity increases almost linearly with the electric field, following the relation **velocity ∝ electric field**.
- As the electric field becomes very high, the carriers reach a maximum velocity called the **saturation velocity** and cannot accelerate further.
- This phenomenon is known as the **velocity saturation effect**, and it becomes significant in short-channel MOSFETs, limiting the drain current.

  
<img width="850" height="390" alt="image" src="https://github.com/user-attachments/assets/d2fe4659-2079-48a1-833b-ac4ad12f3797" />

<img width="923" height="452" alt="image" src="https://github.com/user-attachments/assets/7d2a482c-a06c-4580-916d-9d05f323c140" />


<img width="941" height="521" alt="image" src="https://github.com/user-attachments/assets/5c8b9345-0728-4ff1-93e7-13dde14d81a1" />

<img width="267" height="65" alt="image" src="https://github.com/user-attachments/assets/d9e68fe9-f254-43da-9f09-1d0322466c78" />

At continuity point we take e=ec 
<img width="267" height="65" alt="image" src="https://github.com/user-attachments/assets/1e6f917a-cf4c-4d28-9426-b70bac7d8596" />

that brings us with this equation 
<img width="316" height="92" alt="image" src="https://github.com/user-attachments/assets/76828ce0-859f-4d3e-8f97-4259b4b0846d" />

Re deriving the Drain Current Model

<img width="941" height="436" alt="image" src="https://github.com/user-attachments/assets/72ca2f12-1bbb-41bc-a1b7-aa74ae633ac4" />

The equation becomes TOO COMPLEX to handle 

### L4 Drain Current Model under Velocity Saturation

<img width="953" height="548" alt="image" src="https://github.com/user-attachments/assets/d4887232-6db5-4af3-853b-f57b83a84ff6" />

whichever is minimum we can substitute and get the drain current equation 


***Vdsat is a technology parameter***
<img width="606" height="143" alt="image" src="https://github.com/user-attachments/assets/550c5c27-0b87-44a9-a647-00de0a35be41" />

IF THE DEVICE IS OPERATING IN SATURATION REGION 
<img width="925" height="485" alt="image" src="https://github.com/user-attachments/assets/4d56297e-9874-43bf-8e9d-28508f008ecc" />

IF THE DEVICE IS OPERATING IN THE RESISTIVE REGION
<img width="929" height="494" alt="image" src="https://github.com/user-attachments/assets/8ba411c4-1d17-4e82-9f80-56cd0999f267" />

 IF THE DEVICE IS OPERATING IN THE SATURATION REGION (***ONLY FOR SHORT CHANNEL***)
 <img width="923" height="536" alt="image" src="https://github.com/user-attachments/assets/c1a23bae-887d-48fa-adaa-828836f3236e" />


When we move from higher values of the device to the lower values of the device the velocity saturation causes the device to saturate early
making the peak current for the same W/L ratio is different 

<img width="959" height="552" alt="image" src="https://github.com/user-attachments/assets/2a0d48b0-d895-413d-b7bb-72f1e01f6122" />

The peak current value is 400uamp and 200 micro-amp repectively

### L5 SKY130 Lab: Id–VGS Characteristics

<img width="959" height="538" alt="image" src="https://github.com/user-attachments/assets/c6726c69-c823-4cdb-9de4-80d3a9d29a22" />

**ID VS VDS**

<img width="959" height="518" alt="image" src="https://github.com/user-attachments/assets/58082889-a54d-4c92-9701-e89a6d6081ac" />
Here we can see the quadratic and linear region clearly 

Now we are going to observe 
**ID VS VGS**

<img width="959" height="528" alt="image" src="https://github.com/user-attachments/assets/b62be54a-2978-4128-83b2-2c1184173640" />

Here we are keeping VDS constant  1.8V and we are sweeping only Vgs value till 1.8V with step of 0.1

<img width="959" height="540" alt="image" src="https://github.com/user-attachments/assets/5a281990-d295-4492-80d4-1bb463da020d" />

HOW TO CALCULATE VTH IN ID VS VGS CURVE
ANS: We keep the cursor on the slop and draw a tangent to the curve where the tangent touches the x-axis that is the value of the VTH

<img width="848" height="482" alt="image" src="https://github.com/user-attachments/assets/edda9b97-5292-4a0e-a184-080c56d97de8" />

**it comes somwhere around 0.77**

## CMOS Voltage Transfer Characteristics (VTC)

### L1 MOSFET as a Switch

<img width="606" height="341" alt="image" src="https://github.com/user-attachments/assets/00454fb7-5d21-4b32-a80b-8547d24e16cf" />

We have spoken about this since lecture 1 , the image is self explanatory 

<img width="395" height="369" alt="image" src="https://github.com/user-attachments/assets/3325cea6-b5d3-4ea4-9720-62eff941c140" />



CMOS-COMPLIMENTARY MOSFET

**WHY THIS NAME**
 These transistors work in a complementary manner:
 
  When the NMOS is ON, the PMOS is OFF.
  When the PMOS is ON, the NMOS is OFF.

 Vin is HIGH and is EQUAL to Vdd

<img width="909" height="557" alt="image" src="https://github.com/user-attachments/assets/24f8fe71-a026-490e-9adb-de1b14587f4f" />

PMOS is turned OFF and NMOS is turned ON

### L2 Introduction to standard MOS voltage current parameters

-Vgs<-Vth for a PMOS to be turned on 
Vgs>Vth for a NMOS to be turned on 


<img width="959" height="570" alt="image" src="https://github.com/user-attachments/assets/4a04196f-4755-4466-a27f-0c62a5502f97" />


<img width="937" height="487" alt="image" src="https://github.com/user-attachments/assets/6307b943-8fbb-42dd-b54e-af1d09964561" />

here we observe the direction of currents


### L3 PMOS/NMOS drain current v/s drain voltage

We are going to see few relations for the NMOS region 

***In NMOS region Vss is connected to the GROUND***

<img width="350" height="175" alt="image" src="https://github.com/user-attachments/assets/99f6cbae-ee7a-4e2a-ac7e-d80ea8bafc11" />


<img width="405" height="177" alt="image" src="https://github.com/user-attachments/assets/c847bb05-f38f-47cb-aac2-d2c7106dcbc7" />


***FOR PMOS REGION***

<img width="359" height="320" alt="image" src="https://github.com/user-attachments/assets/7bbdce68-0020-4c57-82bb-a5651bf6e6a2" />

<img width="245" height="98" alt="image" src="https://github.com/user-attachments/assets/27a94a7b-523e-4fa9-92d9-e4231d0ad82a" />


***MOST IMPORTANT OBSERVATION***

<img width="214" height="143" alt="image" src="https://github.com/user-attachments/assets/87f2d737-9473-45fe-8c60-60f8d4f66c9e" />



**NMOS VS PMOS IdsN VS VdsN**

<img width="646" height="357" alt="image" src="https://github.com/user-attachments/assets/4cf64ac2-38c2-4494-9f2f-e5fc837e4b61" />


### L4 Step1 – Convert PMOS gate-source-voltage to Vin

We have tons of voltages but if we try to look at the invertor in the logic point of view we can only see Vin and Vout 

So there should be some way to identify the volatage and the current curves in such a fasion that they are only the function of **Vin and Vout**

Steps to obtain Voltage-Transfer Characterstics(VTC) for Static CMOS Inverter 

ASSUMPTION  :   Vdd=2V AND ITS A LONG CHANNEL DEVICE 

**We are actually converting everything in terms of Vin and Vout**

<img width="959" height="534" alt="image" src="https://github.com/user-attachments/assets/ab068d22-1abd-4adb-8955-67ca434acba4" />



**Now we try to convert everything to IdsN VIn**


<img width="650" height="545" alt="image" src="https://github.com/user-attachments/assets/0fc37d25-eb51-46e8-af2e-8dc7038f87af" />



### L5 Step2 & Step3 – Convert PMOS and NMOS drain-source-voltage to vout

When you say Vout=0V it basically says that the output capacitor is completely  discharged and we need to charge 
the capacitor


<img width="959" height="383" alt="image" src="https://github.com/user-attachments/assets/0b125b0d-22f0-4260-898a-547a76ef5522" />

**This is only TRUE FOR PMOS IS CLUBED WITH NMOS TO FORM CMOS**

**LOAD CURVE FOR PMOS TRANSISTOR**

<img width="341" height="339" alt="image" src="https://github.com/user-attachments/assets/500ebf17-65e2-401e-a9b8-9b8bf063f15a" />

Deriving the load curve for NMOS is easier 

<img width="945" height="584" alt="image" src="https://github.com/user-attachments/assets/e8b6c37d-ebe8-4a7d-8e92-1aca7756f243" />

The final step is to get the voltage transfer characterstics for the CMOS transister 

We achieve that by taking both the load curves of NMOS and PMOS together 


<img width="959" height="493" alt="image" src="https://github.com/user-attachments/assets/be805d72-ef11-4e41-b404-9e73605404b5" />



### L6 Step4 – Merge PMOS – NMOS load curves and plot VTC

We will superimpose the LOAD CURVE of NMOS and PMOS
BUT WHY????

   Because the Vin and Vout are common to NMOS and PMOS , graphically it should be the intersection point of the NMOS and PMOS 

For eg:  If Vin=0V

<img width="689" height="305" alt="image" src="https://github.com/user-attachments/assets/ad8c59ff-d0dd-4e7d-971b-f4a47e0560fb" />

take the intersection point or the common point of the corresponding load lines to plot the graph

<img width="607" height="271" alt="image" src="https://github.com/user-attachments/assets/2a60dce6-d86e-4582-b32c-980d6d8c1483" />

The point is in the LINEAR REGION (pmos is in the linear region)


Now if we combine both the load curves and plot the graph  we get 

<img width="959" height="298" alt="image" src="https://github.com/user-attachments/assets/0fcbf2f8-9ea3-430b-931e-a9e623d66678" /> 


<img width="290" height="199" alt="image" src="https://github.com/user-attachments/assets/263a8db7-4f2c-490e-adaa-629322b3992f" />



### L1 SPICE deck creation for CMOS inverter

First we need to create the SPICE deck

Then we need define the W/L ratio of PMOS and NMOS 

**GENERALLY W/L ratio of PMOS must be GREATER than NMOS**

We will assume the values of Cload=10uF ,Vdd=2.5V ,Vin=2.5V

Now we will identify the Nodes

<img width="457" height="346" alt="image" src="https://github.com/user-attachments/assets/b84dd9e1-90d8-4948-9c73-bdbc26edd3c7" />

<img width="959" height="590" alt="image" src="https://github.com/user-attachments/assets/d3c6c013-f7c7-4074-b7b9-660346c96614" />

PMOS lies between (DRAIN,GATE,SOURCE,SUBSTRATE)

Drain terminal is connected to the OUT
Gate terminal is connected to the IN 
Source and Subtrate are connected to Vdd


### L2 SPICE simulation for CMOS inverter

For NMOS transistor

<img width="728" height="335" alt="image" src="https://github.com/user-attachments/assets/84631446-49cf-4a59-9bef-0d1e607db50c" />


For Output load Capacitor,Supply Voltage and Vin


<img width="843" height="363" alt="image" src="https://github.com/user-attachments/assets/74a31826-b990-43f4-b396-c0fe523ace48" />

Simulation Commands

**here the model file is very important as it contains the complete description of NMOS and PMOS***


<img width="507" height="182" alt="image" src="https://github.com/user-attachments/assets/8ccae022-d7d1-41c9-a566-1b1f968e351b" />


We will do the  spice simulation for :

SPICE waveform : Wn = Wp = 0.375u, Ln,p = 0.25u device  (Wn/Ln = Wp/Lp = 1.5)


Now we will open the model file 


<img width="690" height="503" alt="image" src="https://github.com/user-attachments/assets/0c50d7d6-aa24-4c73-9f1d-eca4cc1c1370" />

We we can see the model NMOS and the technology parameters defined 



Similarly we have PMOS and all the technology parameters defined


<img width="437" height="211" alt="image" src="https://github.com/user-attachments/assets/3bc2c352-39ab-4208-b9ea-70ad69ac868d" />

This is the NETLIST we had defined before


<img width="368" height="253" alt="image" src="https://github.com/user-attachments/assets/d06da6b1-da4e-4597-8da7-b299373dddd4" />

Now if we plot the graph we get 


<img width="594" height="484" alt="image" src="https://github.com/user-attachments/assets/94efd302-18bd-450e-bc84-83663b3dccc9" />

Now we have increased the PMOS width of the transistor

SPICE waveform : Wn = 0.375u, Wp = 0.9375u, Ln,p = 0.25u device  (Wn/Ln = 1.5, Wp/Lp = 2.5)

<img width="448" height="326" alt="image" src="https://github.com/user-attachments/assets/05420496-402e-4099-a076-53f626d61888" />

if we plot the graph 

<img width="578" height="469" alt="image" src="https://github.com/user-attachments/assets/3dfa8af4-e386-4e48-883c-14e982169d5a" />

### L3 Labs Sky130 SPICE simulation for CMOS


<img width="959" height="540" alt="image" src="https://github.com/user-attachments/assets/3063f044-cbf8-4171-9178-c484bd0f7542" />


<img width="589" height="434" alt="image" src="https://github.com/user-attachments/assets/f35bef83-3f56-4b34-bcfe-9ba529b45c4e" />


<img width="952" height="535" alt="image" src="https://github.com/user-attachments/assets/708f5fa3-bf4f-4f65-a6a6-fc3fa9a42ced" />

To plot Switching Threshold 

Keep Zooming into the curve we will get the switching threshold at around 0.87


<img width="169" height="43" alt="image" src="https://github.com/user-attachments/assets/711833ca-f997-4f47-85ba-0fab5dcb6137" />

for transient analysis 


<img width="959" height="535" alt="image" src="https://github.com/user-attachments/assets/1da34618-0eaf-4ac4-8d17-f227609ef478" />


<img width="959" height="490" alt="image" src="https://github.com/user-attachments/assets/8751c8d3-8bba-4465-96c2-1aa2a6cfbacd" />


<img width="832" height="500" alt="image" src="https://github.com/user-attachments/assets/a54c0590-423c-4874-a83a-a65c0274233e" />

For rise delay we need to consider the area shown 


<img width="856" height="482" alt="image" src="https://github.com/user-attachments/assets/2a624543-70b0-4ba6-9141-ef37b9c1af72" />


<img width="215" height="60" alt="image" src="https://github.com/user-attachments/assets/41948025-f6d2-4439-bdb0-3a7c0d0de4fc" />

**Rise delay = 2.482ns-2.15ns = 0.333ns**

For Fall Delay

<img width="524" height="259" alt="image" src="https://github.com/user-attachments/assets/cd6ba46e-7154-42c3-a3ef-1c5807972de1" />


<img width="222" height="43" alt="image" src="https://github.com/user-attachments/assets/0e786f88-0776-4fb6-b5f1-8105ea3bd930" />


**Fall Delay = 4.334ns-4.050ns = 0.285ns**


###  L1 Switching Threshold, Vm

Let us compare the two waveforms

SPICE waveform : Wn = Wp = 0.375u, Ln,p = 0.25u device (Wn/Ln = Wp/Lp = 1.5)    and SPICE waveform : Wn = 0.375u, Wp = 0.9375u,Ln,p = 0.25u device (Wn/Ln = 1.5, Wp/Lp = 3.75)      


<img width="959" height="578" alt="image" src="https://github.com/user-attachments/assets/5ed6a72e-61cc-4b0f-9a88-a5b74c5ac49f" />

**Switching Threshold : Point at which the device switches**


This will define the **ROBUSTNESS** of the of the CMOS Inverter

Vm is the point where Vin  = Vout 


<img width="909" height="512" alt="image" src="https://github.com/user-attachments/assets/473ecc9e-d5cd-45e3-87f6-11e2ecd10cb4" />

these are the area wherein the PMOS and NMOS both are in saturation region 


**Vgs=Vds
Vgs>>>>>Vth**


<img width="959" height="598" alt="image" src="https://github.com/user-attachments/assets/71d293a5-4d83-4c07-96ef-408a52b161fa" />


### L2 Analytical expression of Vm as a function of (W/L)p and (W/L)n

We will calculate the Vm with respect to the NMOS and PMOS width and length


<img width="959" height="559" alt="image" src="https://github.com/user-attachments/assets/f77c0b1d-3c11-4659-8fb1-2090d8df1874" />

<img width="339" height="86" alt="image" src="https://github.com/user-attachments/assets/bbf3c2e1-a4e0-4711-bdcd-9ef0a3b0832c" />

<img width="556" height="143" alt="image" src="https://github.com/user-attachments/assets/7fcf6eb1-3d22-4613-b5b1-6224e1eef200" />



### L3 Analytical expression of (W/L)p and (W/L)n as a function of Vm

If we want the trasistor to switch exactly at 1.25V ie half of power supply 
what W/L ratio of PMOS and NMOS will we get


<img width="908" height="539" alt="image" src="https://github.com/user-attachments/assets/b7eba775-850c-4668-a6f7-3515f6bcf37b" />


take the   VDSATN and VDSATP common from both 


<img width="665" height="75" alt="image" src="https://github.com/user-attachments/assets/ee6ece9d-2154-4d2a-9444-ea9af99d67e8" />




Now we will derive everything in the terms of Kp and Kn 

<img width="346" height="134" alt="image" src="https://github.com/user-attachments/assets/36b36e71-2175-4fbb-aeda-71aec6783ca2" />

expanding the Kp and Kn

<img width="346" height="80" alt="image" src="https://github.com/user-attachments/assets/cdeee220-2576-4670-aee5-ea802e464b9e" />


How much grater should PMOS be than NMOS

<img width="399" height="69" alt="image" src="https://github.com/user-attachments/assets/2e075284-c4d1-48a9-bf46-658f68cda616" />


We will see the behavior of CMOS for different values of W/L ratio of PMOS and NMOS

<img width="220" height="171" alt="image" src="https://github.com/user-attachments/assets/0cb3dca6-20c3-479d-b132-ba6e0f8ce1c3" />


###  L4 Static and dynamic simulation of CMOS inverter


We will do dynamic simulation 

basically the input we will be providing will be a pulse 

and simulation command will be transient analysis 

<img width="689" height="426" alt="image" src="https://github.com/user-attachments/assets/1cc2d7f2-9e35-4735-8571-e225339ecc13" />

What is a pulse in SPICE DECK??
   <img width="926" height="444" alt="image" src="https://github.com/user-attachments/assets/e46caba4-7c8d-4568-80fa-ce66306ef2a3" />


We are doing a transient analysis 

<img width="436" height="132" alt="image" src="https://github.com/user-attachments/assets/b9e66766-c116-4a20-a3fe-2bb00df4bb4c" />


To identify the timing delay

we use the difference between the rising delay and the falling delay

<img width="578" height="471" alt="image" src="https://github.com/user-attachments/assets/59d5a653-315a-4d4f-9bc5-2fd537797b1c" />

We can also calculate the rise and fall delay for by using transient analysis which we did before

<img width="521" height="230" alt="image" src="https://github.com/user-attachments/assets/29880ee8-d853-40bd-9cd5-8b5f7e104932" />


### L5 Static and Dynamic simulation of CMOS inverter with increased PMOS width

Now we will be doing SPICE SIMULATION for increase width of PMOS and compare the results 

<img width="590" height="261" alt="image" src="https://github.com/user-attachments/assets/6707c829-d967-4ef5-adce-6215fe38a9cc" />

<img width="603" height="250" alt="image" src="https://github.com/user-attachments/assets/1a934781-97e4-4895-b790-247d9ef09e59" />

<img width="601" height="231" alt="image" src="https://github.com/user-attachments/assets/aef266ee-b61d-4b3e-906c-cc4f6d529350" />

<img width="602" height="232" alt="image" src="https://github.com/user-attachments/assets/71cf02e2-ca0c-4f85-bff2-3113bbb961e9" />

***The rise delay decreases with an increase in PMOS width because a wider PMOS transistor can source more current and has lower on-resistance. This enables the output capacitor to charge faster, thereby reducing the low-to-high transition time***


### L5 Static and dynamic simulation of CMOS inverter with increased PMOS width

We will use the PMOS which is double the size of NMOS ( width is double)

We just need to change the value of W in DC transfer characteristics 

<img width="515" height="322" alt="image" src="https://github.com/user-attachments/assets/f35601ac-5f2c-4cd3-9f54-c785fbfafd19" />

Same for the Transient Analysis also

<img width="506" height="301" alt="image" src="https://github.com/user-attachments/assets/af1e5493-1a44-41b1-bf35-552d2efb5835" />


**DC TRANSFER CHARACTERISTICS**

**PMOS is more stronger than NMOS AND HENCE THE GRAPH HAS SHIFTED TWOARDS THE RIGHT**


<img width="586" height="467" alt="image" src="https://github.com/user-attachments/assets/f3267d1c-9174-4aeb-bd5a-ee966be79b9a" />


**FOR TRANSIENT ANALYSIS**


<img width="427" height="331" alt="image" src="https://github.com/user-attachments/assets/6c26d3c9-e242-4618-a209-e961855e7aed" />


we calculate the RISE and the FALL delay for these curves


***NOW WE WILL CALCULATE FOR DIFFERENT VALUES OF PMOS width***


<img width="941" height="449" alt="image" src="https://github.com/user-attachments/assets/9b9cf237-d7ca-4fab-bf79-0edf29d6f4b1" />



<img width="959" height="398" alt="image" src="https://github.com/user-attachments/assets/0c593769-79d6-4878-9333-5dc9ae9f6a3a" />



<img width="956" height="484" alt="image" src="https://github.com/user-attachments/assets/06aafa52-8696-4750-b0b5-f155f9d98356" />


Rise delay is  the time which is needed by the output capacitor to charge completely 

**EVERYTIME WE INCREASE THE PMOS WIDTH THE RISE DELAY REDUCES**


<img width="685" height="259" alt="image" src="https://github.com/user-attachments/assets/ed8fa2fa-266a-4168-a7c3-cccd32d20716" />


###  L6 Applications of CMOS inverter in clock network and STA



<img width="524" height="180" alt="image" src="https://github.com/user-attachments/assets/d1c7e47f-8926-4ce7-b0e1-e7baf4ad058b" />


**CONCLUSIONS**

### Conclusions

* During CMOS fabrication, slight variations in the dimensions of the PMOS and NMOS transistors are unavoidable due to process variations. However, the CMOS inverter is highly robust, and these minor changes have very little impact on the switching threshold voltage (Vm). This demonstrates the inverter's ability to maintain reliable and consistent performance despite manufacturing imperfections.

* When the PMOS sizing is chosen such that (W/L)p = 2(W/L)n, the rise delay and fall delay become nearly equal. By further optimizing the PMOS-to-NMOS width ratio through simulation, an even more precise balance between the propagation delays can be achieved. This balanced behavior highlights the symmetry of the CMOS inverter and ensures uniform charging and discharging of the output capacitance.

* The symmetric rise and fall delays are a highly desirable characteristic in digital circuit design. This property makes CMOS inverters ideal for use as clock inverters and clock buffers, where equal propagation delays help minimize clock skew, improve signal integrity, and ensure accurate timing in high-speed VLSI systems.


<img width="546" height="175" alt="image" src="https://github.com/user-attachments/assets/f2a0f121-f9da-4e31-9643-53eaeb84f823" />

APPROXIMATELY EQUAL RISE AND FALL DELAY 



<img width="954" height="594" alt="image" src="https://github.com/user-attachments/assets/7c1ff56f-e8cc-4470-8fa8-6a19cb0b8460" />



<img width="959" height="595" alt="image" src="https://github.com/user-attachments/assets/052298d9-1af0-485e-ab39-d1d3c074b5e0" />



<img width="934" height="353" alt="image" src="https://github.com/user-attachments/assets/469c9057-d406-47f5-87f1-8a176b443f54" />

In order to achieve the below condition we need to use proper rise delay and fall delay 



<img width="959" height="554" alt="image" src="https://github.com/user-attachments/assets/c8631821-2b10-42fb-8824-37d44c5c5e83" />




### Static behaviour evaluation-CMOS inverter robustness-Noise Margin

### L1 Introduction to noise margin

What is NOISE margin

 It is a measure of how much unwanted electrical noise a logic circuit can tolerate on its input without producing an incorrect output.

 eg: If we consider an ideal inverter, input levels of 0 and 1 produce perfect 1 and 0 outputs, with an infinite transition slope at the switching point
 


 <img width="136" height="45" alt="image" src="https://github.com/user-attachments/assets/77e9943c-681c-4a16-96ec-607c02166cd1" />



 <img width="340" height="313" alt="image" src="https://github.com/user-attachments/assets/8be3f658-029e-45d3-999d-ec4e9630eeb7" />


• In real CMOS implementations, unavoidable parasitic resistances and capacitances introduce finite charging and discharging times, resulting in a gradual transition in the Voltage Transfer Characteristic (VTC) rather than an ideal vertical transition.

• The finite gain in the transition region makes the CMOS inverter more sensitive to input noise around the switching threshold (Vm). Consequently, even small input voltage fluctuations can produce significant output voltage changes, highlighting the importance of maintaining adequate noise margins for reliable circuit operation.


<img width="313" height="344" alt="image" src="https://github.com/user-attachments/assets/ed8cf480-7c3a-4403-875b-403115acd0a5" />




<img width="304" height="251" alt="image" src="https://github.com/user-attachments/assets/538ff609-a54a-4503-a7bc-00ba78339061" />



• VIL (Input Low Voltage): The maximum input voltage that is recognized as logic 0. Any input voltage between 0 V and VIL is treated as logic 0.

• VOH (Output High Voltage): The minimum output voltage guaranteed to represent logic 1. Any output voltage between VOH and VDD is treated as logic 1.

• VIH (Input High Voltage): The minimum input voltage that is recognized as logic 1. Any input voltage between VIH and VDD is treated as logic 1.

• VOL (Output Low Voltage): The maximum output voltage guaranteed to represent logic 0. Any output voltage between 0 V and VOL is treated as logic 0.






### L2 Noise Margin voltage paramters



Considering practical non-idealities such as parasitic resistances and capacitances, the Voltage Transfer Characteristic (VTC) of a CMOS inverter is not perfectly vertical in the transition region. Instead, the transition occurs over a finite range of input voltages, resulting in valid logic levels occupying finite voltage ranges.

For 0 < Vin < VIL, the input is recognized as a valid logic LOW, and the output remains in the range VOH ≤ Vout ≤ VDD, representing a valid logic HIGH. Similarly, for VIH < Vin < VDD, the input is recognized as a valid logic HIGH, and the output lies between 0 ≤ Vout ≤ VOL, representing a valid logic LOW. The region between VIL and VIH is known as the transition region, where both the PMOS and NMOS transistors conduct simultaneously. In this region, the output is neither a valid logic HIGH nor a valid logic LOW, making the inverter more susceptible to noise.

To ensure reliable operation when driving subsequent stages, the voltage levels satisfy the relationship:
VOL < VIL < VIH < VOH < VDD.

In the transition region, the slope of the VTC is approximately -1, indicating that an increase in the input voltage results in a corresponding decrease in the output voltage. This finite slope reflects the non-ideal switching behavior of practical CMOS inverters and plays an important role in determining their noise margins and switching performance.


<img width="293" height="265" alt="image" src="https://github.com/user-attachments/assets/0a2f0f87-21c9-4d88-b782-eb16ee613a10" />

###  L3 Noise margin equation and summary


Noise margins define the maximum amount of unwanted noise that a digital circuit can tolerate without causing an incorrect logic interpretation. They ensure reliable operation of CMOS inverters even in the presence of electrical disturbances.

• Noise Margin Low (NML): The voltage difference between VIL and VOL (NML = VIL − VOL). Any voltage variation within this range is still correctly interpreted as a logic LOW.

• Noise Margin High (NMH): The voltage difference between VOH and VIH (NMH = VOH − VIH). Any voltage variation within this range is still correctly interpreted as a logic HIGH.

Thus, voltages lying within the Noise Margin Low (NML) or Noise Margin High (NMH) are considered tolerable and do not affect the correct interpretation of logic levels. However, any input voltage that falls between VIL and VIH lies in the transition (undefined) region, where the output is not guaranteed to be either logic HIGH or logic LOW. In this region, the logic level may switch unpredictably due to noise, making it unsuitable for reliable digital operation.


<img width="546" height="311" alt="image" src="https://github.com/user-attachments/assets/1dbf593f-3963-495f-a402-41bdb1c9fefb" />


<img width="585" height="341" alt="image" src="https://github.com/user-attachments/assets/0a136d59-b8a1-4b01-8b1d-05675b171eea" />


###  L4 Noise margin variation with respect to PMOS width

To evaluate the robustness of the CMOS inverter against noise, the PMOS width is varied as an integral multiple of the NMOS width while keeping all other parameters constant. The corresponding Voltage Transfer Characteristics (VTCs) are then analyzed to observe the effect of transistor sizing on the noise margins.

The critical points of the VTC are identified by locating the points where the slope of the curve satisfies dVout/dVin = −1. These points correspond to the input threshold voltages VIL and VIH. From these points, projections are extended to the x-axis and y-axis to determine the values of VIL, VIH, VOL, and VOH.

Using these parameters, the noise margins are calculated as:
• Noise Margin Low (NML) = VIL − VOL
• Noise Margin High (NMH) = VOH − VIH

By comparing the noise margins for different PMOS-to-NMOS width ratios, the effect of transistor sizing on the inverter's immunity to noise can be evaluated. This analysis demonstrates the inherent robustness of the CMOS inverter, showing that it maintains reliable logic levels and adequate noise margins even with variations in transistor dimensions.


case 1

   <img width="633" height="275" alt="image" src="https://github.com/user-attachments/assets/8f1ba937-27de-41da-81c0-e5486feede2a" />


  A larger noise margin indicates a stronger and more noise-immune CMOS inverter, ensuring reliable logic interpretation 
  even in the presence of glitches and coupling noise

case 2

  <img width="642" height="256" alt="image" src="https://github.com/user-attachments/assets/c460c207-8665-4a93-a11e-4aa4bb7d4d55" />

 case 3

   <img width="648" height="257" alt="image" src="https://github.com/user-attachments/assets/b203fe88-b0e2-4aed-aec9-3ddce57d0af7" />

case 4

   <img width="368" height="348" alt="image" src="https://github.com/user-attachments/assets/9ccb4eed-f1f1-4fa1-ae21-5fa4cb26ed62" />

case 5

   <img width="618" height="257" alt="image" src="https://github.com/user-attachments/assets/69084249-e7d7-4ac2-92b9-9cd00dca0b3d" />

For PMOS width ratios of Wp/Lp = 4(Wn/Ln) and Wp/Lp = 5(Wn/Ln), the extracted Noise Margin High (NMH) and Noise Margin Low (NML) are nearly identical. This indicates that beyond a certain PMOS sizing ratio, the noise margins reach a saturation point and become relatively insensitive to further increases in PMOS width.

This behavior demonstrates that increasing the PMOS width beyond the optimum ratio does not significantly enhance the inverter's noise immunity. Instead, it leads to increased silicon area, higher parasitic capacitance, and greater power and delay overheads without providing any meaningful improvement in performance. Therefore, an optimum PMOS-to-NMOS width ratio should be selected to achieve the best trade-off between noise immunity, area, and overall circuit efficiency.


<img width="506" height="170" alt="image" src="https://github.com/user-attachments/assets/b269bbc1-835b-4848-9bf6-c2f0bfafbc46" />

We can also know about the ANALOG and DIGITAL design in CMOS invertor 


<img width="560" height="399" alt="image" src="https://github.com/user-attachments/assets/85aa0deb-ef77-46dc-8b17-0e7dfeeba4d3" />


<img width="548" height="388" alt="image" src="https://github.com/user-attachments/assets/04f2d0f9-e614-4234-b6c2-4e460a149195" />

###  Sky130 Noise margin labs


<img width="959" height="540" alt="image" src="https://github.com/user-attachments/assets/242dbb44-ede0-4f20-9d75-c4f4bc4eee6b" />


<img width="959" height="533" alt="image" src="https://github.com/user-attachments/assets/dae3102a-388c-4e20-9941-fb9f2a968811" />



<img width="224" height="108" alt="image" src="https://github.com/user-attachments/assets/6cf9841a-0524-4ffa-81ba-ae3d336cbf73" />


### L1 Smart SPICE simulation for power supply variations


To evaluate the robustness of the CMOS we need to also consider the power supply scalling 


We will do spice simulation 


<img width="845" height="301" alt="image" src="https://github.com/user-attachments/assets/bb217ab8-6215-499c-922b-5bb5269b7aa9" />



<img width="299" height="122" alt="image" src="https://github.com/user-attachments/assets/230f1953-cbb4-4303-b3b2-b13294707550" />



<img width="563" height="118" alt="image" src="https://github.com/user-attachments/assets/820ba112-a178-4dc8-8da0-df1baf10ad2a" />



Only chaning the Vdd(0.5,1,1.5)


<img width="590" height="470" alt="image" src="https://github.com/user-attachments/assets/64a05391-6f2b-4ca1-a97d-603323e6e1b4" />



### L2 Advantages and disadvantages using low supply voltage


<img width="647" height="407" alt="image" src="https://github.com/user-attachments/assets/9fb020ea-7586-43f5-9e5d-1680f52bb867" />

now we will caculate the gain for different values of V(2.5,0.5) and compare it 

Gain is the ratio of change in output volatage/change in input voltage



<img width="442" height="164" alt="image" src="https://github.com/user-attachments/assets/4b933eab-5320-4619-a58f-5f33a65672c4" />


Gain when a CMOS invertor at an voltage of 2.5V 


<img width="920" height="532" alt="image" src="https://github.com/user-attachments/assets/02d375e8-3e94-484e-9899-57308aa80c7e" />

If just subtract the energy at 2.5V and at 0.5V we see that there is 96% reduction in energy 


<img width="949" height="560" alt="image" src="https://github.com/user-attachments/assets/73d5f56b-85ba-44c1-b707-e67826f36698" />


<img width="611" height="330" alt="image" src="https://github.com/user-attachments/assets/3f326ad3-d3fd-4cbd-8a5b-eadc6c207e97" />


Disadvantages

  Performance impact 


  <img width="914" height="461" alt="image" src="https://github.com/user-attachments/assets/b0505896-f58a-48f8-acce-f818bcb417b8" />



 <img width="875" height="436" alt="image" src="https://github.com/user-attachments/assets/e5c12eb1-03da-4889-8e26-4d79c286f92b" />


 ### L3 Sky130 Supply Variation Labs


 <img width="959" height="543" alt="image" src="https://github.com/user-attachments/assets/b74b88d0-c89b-4ae1-a94f-d72f10466c2d" />


 <img width="859" height="484" alt="image" src="https://github.com/user-attachments/assets/55edc524-f9ab-4ced-9dcc-cf086a06f02b" />
 


 <img width="158" height="57" alt="image" src="https://github.com/user-attachments/assets/e728a504-e8be-40af-9dd1-d43ac6ae028a" />

 Gain is approximately 7.89 


  ### L1 Sources of variation – Etching process


  <img width="896" height="503" alt="image" src="https://github.com/user-attachments/assets/6017f776-4605-4e0d-82a2-e972657e4069" />


  Etching process - Will decide the shape and how will the shape has been done 

Single inverter 


  <img width="266" height="338" alt="image" src="https://github.com/user-attachments/assets/163b9b55-208b-4dc7-93ce-13ac1e448386" />

Inverter Chain 


  <img width="939" height="478" alt="image" src="https://github.com/user-attachments/assets/19499922-342e-4a8e-b608-5eadc2daac1f" />



<img width="876" height="530" alt="image" src="https://github.com/user-attachments/assets/e001f1b0-be41-43b8-851a-5f36d85042cd" />

there is a difference between the ideal mask and the actual mask due to fabrication 

The actual and ideal **LENGTH** and **AREA** will vary for **SURE**


<img width="922" height="329" alt="image" src="https://github.com/user-attachments/assets/94515614-691c-4ed9-a666-32ddb2b04a2e" />

In the middle the variation at the centre is almost the same structure like the actual mask 

Towards the side it may be connected to the flip flops and it might not be like the actual mask we know 


<img width="743" height="413" alt="image" src="https://github.com/user-attachments/assets/8fbd845c-dcb1-4b3b-ab89-95d0ef17a7bc" />

Any variation in the W and L will directly affect the drain current 


###  L2 Sources of variation – oxide thickness



<img width="956" height="507" alt="image" src="https://github.com/user-attachments/assets/cabbaa83-23fd-425d-8148-039ad0a5cde0" />



<img width="959" height="599" alt="image" src="https://github.com/user-attachments/assets/dc683e6d-34f1-4ca0-9858-b17aff292877" />




<img width="848" height="490" alt="image" src="https://github.com/user-attachments/assets/64a546e4-f2ef-4100-8df4-628f39bc8a6b" />


more the oxide variation more the drain current variation 


### L3 Smart SPICE simulation for device variations

 CMOS inverter is least responsive to the device variation 

 When we increase the size of the PMOS the resistance DECREASES (LEAST RESISTANCE)
 
 When we decrease the size of the NMOS the resistance DECREASES (HIGHEST RESISTANCE)

 
 
We are trying to test the extreame conditions


 <img width="958" height="463" alt="image" src="https://github.com/user-attachments/assets/a1d90e68-bfe7-469c-a56f-398aecd34fac" />
 

 <img width="422" height="128" alt="image" src="https://github.com/user-attachments/assets/f8730b88-bba2-4029-aa69-61849037dee4" />
 

 <img width="479" height="293" alt="image" src="https://github.com/user-attachments/assets/aa240771-2457-4587-9831-2ef96633a3d7" />
 

 <img width="586" height="467" alt="image" src="https://github.com/user-attachments/assets/dcbd65ea-7541-4eed-a767-3bd5d8c82930" />

 ### L4 Conclusion

 For caculating the switching threshold 



 <img width="486" height="355" alt="image" src="https://github.com/user-attachments/assets/935f9cef-d8c8-492e-9bd5-cfdd70eb2d1e" />

 there is about 1.2V variation in the switching threshold but it is acceptable 

 <img width="704" height="438" alt="image" src="https://github.com/user-attachments/assets/4f504b92-377e-437e-a9fe-3296bbaa3305" />


Varition in NOISE MARGIN

<img width="800" height="431" alt="image" src="https://github.com/user-attachments/assets/8716ae22-7427-48e5-9629-cca496ab7e57" />



<img width="686" height="343" alt="image" src="https://github.com/user-attachments/assets/69b5c48c-5b2a-4e91-8064-ecae84825867" />


The variation in Noise Margin is low 


<img width="638" height="422" alt="image" src="https://github.com/user-attachments/assets/ef023993-bd41-40f8-8156-1c97180a3144" />


###  L5 Sky130 Device Variation Labs

<img width="959" height="542" alt="image" src="https://github.com/user-attachments/assets/ca442555-c2a9-4d9b-ab80-55d284fef971" />

Strong Pfet and wear Nfet


<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/ed8d331b-32ee-478c-90b6-055cb4ba1aa0" />

To obtain switching thresold

<img width="959" height="538" alt="image" src="https://github.com/user-attachments/assets/5109222c-a07a-4fbf-8402-cdf4c471d96b" />

<img width="193" height="36" alt="image" src="https://github.com/user-attachments/assets/e9caffbc-de13-4467-bb3f-5584c97bb366" />


Though we gave the device varition more the diffrence in switching variation is approximately 80mV 
FROM THIS WE CONCLUDE THAT CMOS IS VERY ROBUST 















  
















    
  










 




















 





















































































































  


  





 

  






  














        


