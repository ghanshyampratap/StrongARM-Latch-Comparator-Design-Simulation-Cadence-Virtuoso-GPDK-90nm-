#  StrongARM Latch Comparator – Design & Simulation 

##  INTRODUCTION
A StrongARM latch is a high-speed dynamic comparator widely used in ADCs and mixed-signal ICs. It offers:

- Zero static power consumption  
- High gain and fast regeneration  
- Differential input comparison  
- Clock-controlled dynamic operation  

The comparator operates in two phases:

1. **Precharge Phase (CLK = 0):** Outputs precharged to VDD  
2. **Evaluation Phase (CLK = 1):** Regenerative comparison begins through the differential pair  

This project involves designing and simulating the StrongARM latch in **Cadence Virtuoso** using **GPDK 90nm** technology with transient analysis using Spectre.

---

## CIRCUIT DIAGRAM

### Fig 1 – StrongARM Latch Comparator  
<img width="817" height="779" alt="image" src="https://github.com/user-attachments/assets/d9b3d769-66b8-459f-9899-abe936d0c810" />


---

## ⚙️ WORKING

### Components
- **M1–M2:** Differential NMOS input pair  
- **M3–M6:** Cross-coupled PMOS–NMOS regenerative latch  
- **M7:** Tail NMOS (clock-controlled)  
- **M8–M9:** PMOS precharge devices
  
###  Operation
- **CLK = 0 (Precharge Phase):**  
  Outputs Out+ and Out− charged to VDD, tail NMOS OFF  

- **CLK = 1 (Evaluation Phase):**  
  Tail NMOS ON, differential pair discharges nodes based on Vin+ and Vin−  
  Positive feedback regenerates decision to logic levels  

---

### Fig 2 – SR Latch  
<img width="1090" height="371" alt="image" src="https://github.com/user-attachments/assets/68d32a36-7e1c-4c5f-8293-a914e732b6a5" />


### SR Latch Explanation
The SR latch is added to:

- Capture the StrongARM decision  
- Prevent metastability  
- Hold output state between cycles  

---
##  RESULT ANALYSIS

### About Simulation Software
Cadence Virtuoso provides:
- Schematic design  
- Transistor-level simulation  
- Mixed-signal verification  
- Spectre for analog transient analysis  

### Tools Used
1. Virtuoso Schematic Editor  
2. Virtuoso ADE L/XL  
3. Spectre Simulator  
4. GPDK 90nm PDK  

---

## PROCEDURE

### 1. Library Setup
- Create new library  
- Attach GPDK 90nm tech  
- Open schematic editor and place devices  

### 2. Schematic Design
- Build differential pair, tail transistor, feedback pair, precharge PMOS  
- Apply sources:  
  - **Vin+** : Sine (DC=0.7V, Amp=0.7V, 1MHz)  
  - **VDD** : 1.8V  
  - **CLK** : 0–1.8V pulse, 10ns period  
- Save schematic  

### 3. Simulation in ADE L
- Select Transient analysis  
- Plot Vin+, Vin−, CLK, and OUT  
- Run Spectre  

---

##  LOW POWER TECHNIQUE (Isolation Transistors)
In the standard StrongARM latch, a momentary direct path from VDD → GND causes **short-circuit dynamic power**.

To reduce this, **isolation transistors** are added:

### Fig 3 – With Isolation Transistors  
<img width="1010" height="579" alt="image" src="https://github.com/user-attachments/assets/7c3a06cf-15cc-4eba-80a4-32c510d6e6c5" />


### Fig 4 – Without Isolation Transistors  
<img width="1090" height="561" alt="image" src="https://github.com/user-attachments/assets/63d4eb1f-5e44-4000-8888-de416e848645" />


Benefits of isolation transistors:
- Reduce short-circuit current  
- Avoid direct VDD→GND conduction  
- Maintain speed while lowering power  

---

## RESULTS AND OUTPUT ANALYSIS

### Precharge Phase (CLK = 0)
- Tail OFF  
- Out+ and Out− ≈ VDD  
- Zero static power  

### Evaluation Phase (CLK = 1)
- Tail ON  
- Input difference decides discharge rate  
- Regenerative feedback amplifies to full swing  

The output correctly shows:
- Logic high when **V+ > V−**  
- Logic low when **V− > V+**

### Fig 5 – Transient Output  
<img width="1090" height="398" alt="image" src="https://github.com/user-attachments/assets/80bbffeb-a548-4af4-b035-fcc8dac8c222" />

---


##  CONCLUSION
The StrongARM latch was successfully designed and simulated in Cadence Virtuoso using GPDK 90nm. The comparator demonstrates:

- High-speed operation  
- Zero static power  
- Strong regenerative behavior  
- Reduced dynamic power using isolation transistors  

This work reinforces understanding of dynamic comparators, clocked operation, and low-power VLSI design.

---

##  REFERENCES
1. B. Razavi, *Design of Analog CMOS Integrated Circuits*, McGraw-Hill, 2001  
2. T. Kobayashi et al., IEEE JSSC, 1993  
3. J. Yuan & C. Svensson, IEEE JSSC, 1989  
4. Cadence Virtuoso – Spectre User Guide, 2023  
5. GPDK 90nm PDK Documentation, 2023  

