# DC-DC Buck Converter

This project focuses on the **design, simulation, and hardware implementation of a high-frequency DC-DC Buck Converter**. The converter efficiently steps down a DC input voltage using controlled switching and LC filtering. 

The system's operation was comprehensively analyzed and verified under both **Continuous Conduction Mode (CCM)** and **Discontinuous Conduction Mode (DCM)**, comparing theoretical MATLAB/Simulink models against physical hardware data.

---
▶️ **Watch Demo Video:**  
[DC-DC Buck Converter Hardware Demonstration](https://drive.google.com/file/d/1EWnwqPw_YfhNXYwbQKV2mLtyXISwJYmo/view?usp=sharing)

## ⚡ Converter Specifications

| Parameter | Value |
|:---|:---|
| **Converter Type** | Buck Converter |
| **Input Voltage ($V_{in}$)** | 10 V |
| **Output Voltage ($V_{out}$)** | 5 V |
| **Switching Frequency ($f_s$)** | 15 kHz |
| **Duty Cycle ($D$)** | 50% |
| **Output Current ($I_{out}$)** | 1 A |
| **Operating Modes** | CCM & DCM |

---

## ⚙️ Working Principle

A buck converter is a switch-mode step-down DC-DC converter. By varying the duty cycle ($D$) of the switching signal, the average output voltage is controlled according to the ideal relationship:

$$V_{out} = D \cdot V_{in}$$

### Main Components
* **Power Stage:** MOSFET Switch, Freewheeling Diode
* **Filter Stage:** Inductor ($L$), Output Capacitor ($C$)
* **Control & Load:** Gate Driver Circuit, Load Resistance ($R$)

### Operating States

#### 1. Switch ON State
* The MOSFET conducts, forcing the diode into reverse bias.
* Energy flows from the source, charging the inductor and capacitor while supplying the load.
* The inductor current ($i_L$) increases linearly.

#### 2. Switch OFF State
* The MOSFET turns off, and the inductor induces a voltage that forward-biases the freewheeling diode.
* Stored energy in the inductor and capacitor discharges to maintain load current.
* The inductor current ($i_L$) decreases linearly.

---

## 💻 MATLAB Simulation

A MATLAB/Simulink model was developed to validate the theoretical design of the buck converter before hardware deployment. 

The simulation successfully verified:
* Stable step-down conversion from **10 V to 5 V** at a 50% duty cycle.
* Transient response and steady-state output voltage ripples.
* The boundary condition between CCM and DCM when modifying circuit load parameters.

---

## 🛠️ Hardware Implementation

The hardware prototype was constructed on a soldered perf-board to ensure reliable connections and minimize parasitic effects.

### 1. Gate Driver Circuit
* Generates the precise 15 kHz PWM signal with a 50% duty cycle.
* Provides isolation and shifts the logic-level signal to the required $V_{GS}$ threshold to fully drive the power MOSFET into saturation.

### 2. Power Stage & Filter
* Robust power MOSFET and ultra-fast recovery diode to minimize switching losses.
* Optimized LC filter network to maintain low voltage and current ripple.

---

## 📊 Waveform Analysis

### PWM Signal
* **Frequency:** 15 kHz | **Duty Cycle:** 50%
* Controls the exact timing of the energy storage and transfer cycles.

### Continuous Conduction Mode (CCM)
In CCM, the inductor current never drops to zero during the switching cycle due to a sufficiently large filter inductance or high load demand.

$$\Delta i_L < I_L \implies i_L(min) > 0$$

* **Characteristics:** Smooth triangular current waveform, lower output voltage ripple, continuous energy transfer.

### Discontinuous Conduction Mode (DCM)
DCM operation was demonstrated by significantly **increasing the load resistance ($R$)**. As the load resistance increases, the average load current drops below the critical threshold required for continuous conduction. Consequently, the stored inductor energy dissipates entirely before the next switching cycle begins.

$$i_L = 0 \text{ before the next switching period begins}$$

* **Characteristics:** Inductor current hits zero early, resulting in a resonant ringing effect across the switch and higher voltage ripples.

---

## ⚖️ CCM vs. DCM Comparison

| Feature | Continuous Conduction Mode (CCM) | Discontinuous Conduction Mode (DCM) |
|:---|:---|:---|
| **Inductor Current** | Never falls to zero ($i_L > 0$) | Falls to zero before the cycle ends |
| **Load Current** | Higher loads | Light loads / Lower average current |
| **Output Ripple** | Minimal and predictable | Relatively higher |
| **Load Resistance ($R$)** | Lower ($R < R_{crit}$) | Higher ($R > R_{crit}$) |
| **Energy Transfer** | Continuous | Pulsed / Intermittent |

---

## 📐 PCB Design

The PCB layout was engineered focusing on power electronics best practices:
* **Minimized Loop Areas:** High $di/dt$ switching loops were kept as small as possible to suppress electromagnetic interference (EMI).
* **Thick Power Traces:** Wide copper tracks were utilized for high-current paths ($V_{in}$, Switch, Inductor, $V_{out}$, GND) to handle power dissipation.
* **Isolation:** Proper separation between the low-power gate driver control signals and the high-power switching stage.

---

## 🏆 Key Results

* Successfully demonstrated **10V DC to 5V DC** regulated conversion.
* Confirmed stable **15 kHz** high-frequency switching.
* Successfully transitioned the system from CCM to DCM by **increasing the load resistance**.
* Captured and verified distinctive **CCM and DCM current profiles** on the oscilloscope.
* Proved tight correlation between theoretical equations, MATLAB simulations, and practical hardware data.

---

## 🧰 Tools & Components Used

### Software
* MATLAB / Simulink (Simulation & Data Analysis)
* PCB Design Tool (Layout Design)

### Hardware Components
* Power MOSFET & Ultra-fast Diode
* Inductor & Low-ESR Electrolytic Capacitors
* Gate Driver Circuit & Pulse Generator
* Regulated DC Power Supply
* Digital Oscilloscope
* Variable Power Resistors (Load)

---

## 📝 Conclusion

The DC-DC Buck Converter was successfully designed, modeled, and hardware-verified. The experimental results closely align with the theoretical frameworks and MATLAB simulations, showcasing proper switching behavior, predictable filter dynamics, and clear transitions between CCM and DCM operations achieved via load adjustment.

---

## 👥 Contributors

* **Group B1-G8**
* Electrical Machines and Power Electronics Laboratory
* **Indian Institute of Technology Indore**
