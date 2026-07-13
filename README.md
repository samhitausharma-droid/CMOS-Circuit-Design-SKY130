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


<img width="558" height="390" alt="image" src="https://github.com/user-attachments/assets/7e2aae84-5542-401c-a3c1-254a9b035092" 

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






















































  


  





 

  






  














        


