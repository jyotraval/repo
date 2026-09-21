# Comprehensive IoT Mid-Semester Exam Study & Preparation Guide
**Course Code:** 20IC401T | **Target Exam Duration:** 1 Hour | **Total Marks:** 25 Marks  
*(Covering Unit 1: Introduction to IoT & Unit 2: Technology for IoT)*

---

## Master Exam Strategy & 25-Mark Blueprint

Based on the 2024 (50-mark) and 2025 (25-mark) examination papers set by Dr. Abhishek Kumar and Dr. Abhishek Joshi, the 25-mark paper follows a distinct 3-tier structure:

```
┌───────────────────────────────────────────────────────────────────────────┐
│ Section / Q# │ Target Topics                           │ Mark Weightage   │
├──────────────┼─────────────────────────────────────────┼──────────────────┤
│ Question 1   │ Part A: Battery Lifetime / Duty Cycling │ 5 Marks          │
│ (Numerical)  │ Part B: Data Generation / Network BW    │ 5 Marks          │
├──────────────┼─────────────────────────────────────────┼──────────────────┤
│ Question 2   │ IoT-WF 7-Layer Architecture OR          │ 10 Marks         │
│ (System/Arch)│ Level 5+ Smart Campus / Domain Design   │                  │
├──────────────┼─────────────────────────────────────────┼──────────────────┤
│ Question 3   │ Access Technology (Zigbee / BLE / NFC)  │ 5 Marks          │
│ (Protocols)  │ OR SPI vs I2C / MQTT vs CoAP           │                  │
└───────────────────────────────────────────────────────────────────────────┘
```

---

# Module 1: High-Yield Numericals (Guaranteed 10 Marks)

Examiners draw directly from specific numerical templates: **Duty Cycle & Battery Lifetime**, **Data Volume & Network Throughput**, and **Shannon Capacity & Resource Allocation**.

---

### 1.1 Duty Cycling & Battery Lifetime Calculations

#### Core Formulae
1. **Average Current Consumption ($I_{\text{avg}}$):**
   $$I_{\text{avg}} = \frac{(I_{\text{active}} \times t_{\text{active}}) + (I_{\text{sleep}} \times t_{\text{sleep}})}{t_{\text{period}}}$$
   *Ensure $t_{\text{active}} + t_{\text{sleep}} = t_{\text{period}}$, and all currents are in identical units ($\text{mA}$ or $\mu\text{A}$). Note: $1\text{ mA} = 1000\ \mu\text{A}$.*

2. **Device Lifetime:**
   $$T_{\text{hours}} = \frac{\text{Battery Capacity (mAh)}}{I_{\text{avg}}\ (\text{mA})}$$
   $$T_{\text{days}} = \frac{T_{\text{hours}}}{24}, \quad T_{\text{years}} = \frac{T_{\text{days}}}{365}$$

3. **Battery Replacements over Period ($Y$ years) for $N$ devices:**
   $$\text{Replacements per Device} = \left\lfloor \frac{Y}{T_{\text{years}}} \right\rfloor \quad \text{or continuous: } \frac{Y}{T_{\text{years}}} - 1$$
   $$\text{Total Replacements} = N \times \text{Replacements per Device}$$

---

#### Solved Problem 1 (From 2025 Mid-Sem Exam — Q1.A [5 Marks])
> **Problem Statement:**  
> A smart university classroom deploys a battery-powered occupancy sensor ($3.7\text{ V}$, $2400\text{ mAh}$ Li-ion cell).  
> - **Active mode:** Current = $25\text{ mA}$ for $1\text{ s}$ every $2\text{ minutes}$ (sensing + wireless transmission).  
> - **Sleep mode:** Current = $80\ \mu\text{A}$ otherwise.  
> 
> **Find:**  
> a. Average current consumption ($I_{\text{avg}}$ in $\text{mA}$).  
> b. Device lifetime (hours, days, and years).  
> c. Total number of battery replacements needed for $40$ sensors over $3\text{ years}$ of operation.

**Step-by-Step Solution:**

* **Step A: Time & Current Conversions**  
  Total period $T = 2\text{ minutes} = 120\text{ seconds}$.  
  Active time $t_{\text{active}} = 1\text{ s} \implies I_{\text{active}} = 25\text{ mA}$.  
  Sleep time $t_{\text{sleep}} = 120 - 1 = 119\text{ s}$.  
  Sleep current $I_{\text{sleep}} = 80\ \mu\text{A} = \frac{80}{1000}\text{ mA} = 0.08\text{ mA}$.

* **Step B: Calculate $I_{\text{avg}}$**
  $$I_{\text{avg}} = \frac{(25\text{ mA} \times 1\text{ s}) + (0.08\text{ mA} \times 119\text{ s})}{120\text{ s}} = \frac{25 + 9.52}{120} = \frac{34.52}{120} \approx \mathbf{0.2877\text{ mA}}$$

* **Step C: Estimate Device Lifetime**
  $$T_{\text{hours}} = \frac{2400\text{ mAh}}{0.28767\text{ mA}} \approx \mathbf{8,342.9\text{ hours}}$$
  $$T_{\text{days}} = \frac{8,342.9}{24} \approx \mathbf{347.62\text{ days}}$$
  $$T_{\text{years}} = \frac{347.62}{365} \approx \mathbf{0.9524\text{ years}} \quad (\approx 11.43\text{ months})$$

* **Step D: Battery Replacements for 40 Sensors over 3 Years**  
  Lifetime of 1 battery = $0.9524\text{ years}$.  
  Total battery operational cycles required per sensor in $3\text{ years} = \frac{3}{0.9524} \approx 3.15$ batteries.  
  Since the initial battery is installed on Day 0, the sensor will exhaust its initial battery and need replacement at $t = 0.952\text{ yr}$, $t = 1.905\text{ yr}$, and $t = 2.857\text{ yr}$.  
  $$\text{Replacements per sensor in 3 years} = 3$$
  $$\text{Total Replacements for 40 sensors} = 40 \times 3 = \mathbf{120\text{ replacement batteries}}$$  
  *(Total batteries consumed including the initial ones = $40 \times 4 = 160$ batteries).*

---

#### Solved Problem 2 (Slide Problem / Question Bank #2)
> **Problem Statement:**  
> An IoT device consumes $10\text{ mA}$ when active and $0.5\text{ mA}$ in sleep mode. It is active for $2\text{ hours}$ and sleeps for $22\text{ hours}$ daily. Battery capacity is $1000\text{ mAh}$. Calculate battery life in days.

**Solution:**
$$\text{Daily Energy Consumption} = (10\text{ mA} \times 2\text{ h}) + (0.5\text{ mA} \times 22\text{ h}) = 20 + 11 = 31\text{ mAh/day}$$
$$\text{Battery Life} = \frac{1000\text{ mAh}}{31\text{ mAh/day}} = \mathbf{32.26\text{ days}}$$

---

### 1.2 Data Volume, Network Throughput & Latency

#### Core Formulae
1. $\text{Data Rate (bps)} = \frac{\text{Data Size (bits)}}{\text{Time (seconds)}} = \frac{\text{Data Size (Bytes)} \times 8}{\text{Time (seconds)}}$
2. $\text{Transmission Latency} = \frac{\text{Packet Size (bits)}}{\text{Bandwidth (bps)}}$
3. $\text{Bandwidth Utilization (\%)} = \left( \frac{\text{Device Data Rate}}{\text{Network Bandwidth}} \right) \times 100$
4. $\text{Received Signal Strength (RSSI)} = P_{\text{Tx}}\ (\text{dBm}) - \text{Signal Loss (dB)}$
5. $\text{Packet Loss Rate (\%)} = \left( \frac{N_{\text{sent}} - N_{\text{received}}}{N_{\text{sent}}} \right) \times 100$

---

#### Solved Problem 3 (From 2025 Mid-Sem Exam — Q1.B [5 Marks])
> **Problem Statement:**  
> A temperature sensor transmits data every $30\text{ seconds}$ with a packet size of $250\text{ bytes}$. A light sensor transmits data every $10\text{ seconds}$ with a packet size of $90\text{ bytes}$.  
> Find the number of packets generated by each sensor in $24\text{ hours}$ ($86,400\text{ seconds}$), and compute the total data generated.

**Step-by-Step Solution:**

* **Temperature Sensor:**
  $$\text{Transmission Interval } (T_1) = 30\text{ s}, \quad \text{Size } (S_1) = 250\text{ bytes}$$
  $$\text{Packets generated } (N_1) = \frac{86,400\text{ s}}{30\text{ s}} = \mathbf{2,880\text{ packets}}$$
  $$\text{Data generated } (D_1) = 2,880 \times 250\text{ bytes} = 720,000\text{ bytes} = \mathbf{720\text{ KB}} \quad (703.125\text{ KiB})$$

* **Light Sensor:**
  $$\text{Transmission Interval } (T_2) = 10\text{ s}, \quad \text{Size } (S_2) = 90\text{ bytes}$$
  $$\text{Packets generated } (N_2) = \frac{86,400\text{ s}}{10\text{ s}} = \mathbf{8,640\text{ packets}}$$
  $$\text{Data generated } (D_2) = 8,640 \times 90\text{ bytes} = 777,600\text{ bytes} = \mathbf{777.6\text{ KB}} \quad (759.375\text{ KiB})$$

* **Aggregate Values:**
  $$\text{Total Packets} = 2,880 + 8,640 = \mathbf{11,520\text{ packets}}$$
  $$\text{Total Data Generated} = 720,000 + 777,600 = \mathbf{1,497,600\text{ bytes}} = \mathbf{1.4976\text{ MB}} \quad (\approx 1.428\text{ MiB})$$

---

#### Solved Problem 4 (Latency & RSSI — Question Bank #3 & #5)
> **Problem Statement A:** A sensor node sends a 512-byte packet over a 1 Mbps link. Find transmission latency.  
> **Solution:**  
> $\text{Packet bits} = 512 \times 8 = 4096\text{ bits}$.  
> $\text{Bandwidth} = 1\text{ Mbps} = 10^6\text{ bps}$.  
> $$\text{Latency} = \frac{4096\text{ bits}}{1,000,000\text{ bps}} = 0.004096\text{ s} = \mathbf{4.096\text{ ms}}$$

> **Problem Statement B:** An IoT device transmits at $2.4\text{ GHz}$ with $P_{\text{Tx}} = 10\text{ dBm}$. Signal path loss is $100\text{ dB}$. Find received signal strength (RSSI).  
> **Solution:**  
> $$\text{RSSI} = P_{\text{Tx}} - \text{Loss} = 10\text{ dBm} - 100\text{ dB} = \mathbf{-90\text{ dBm}}$$

---

### 1.3 Shannon Capacity, TDMA Allocation & Offloading Calculations

#### Solved Problem 5 (TDMA Feasibility & Scaling — Class Slide Problem 1)
> **Problem Statement:**  
> Three sensors share a TDMA uplink frame ($T_{\text{frame}} = 100\text{ ms}$, Bandwidth $B = 1\text{ MHz}$).  
> Payloads: $S_1 = 100\text{ kbits}$ ($\text{SNR} = 10\text{ dB}$), $S_2 = 200\text{ kbits}$ ($\text{SNR} = 5\text{ dB}$), $S_3 = 150\text{ kbits}$ ($\text{SNR} = 20\text{ dB}$).  
> 1. Is the frame feasible?  
> 2. If not, find the minimum bandwidth required.  
> 3. Find the maximum payloads transmittable in $100\text{ ms}$ at $1\text{ MHz}$ maintaining payload ratios.

**Solution:**

1. **SNR Conversion (dB to Linear):** $\text{SNR}_{\text{lin}} = 10^{\frac{\text{SNR}_{\text{dB}}}{10}}$
   * $\text{SNR}_1 = 10^{1.0} = 10$
   * $\text{SNR}_2 = 10^{0.5} = 3.1623$
   * $\text{SNR}_3 = 10^{2.0} = 100$

2. **Shannon Capacity Rates:** $R = B \log_2(1 + \text{SNR})$
   * $R_1 = 10^6 \times \log_2(1 + 10) = 10^6 \times \frac{\ln(11)}{\ln(2)} \approx 3.459\text{ Mbps}$
   * $R_2 = 10^6 \times \log_2(1 + 3.1623) = 10^6 \times \frac{\ln(4.1623)}{\ln(2)} \approx 2.057\text{ Mbps}$
   * $R_3 = 10^6 \times \log_2(1 + 100) = 10^6 \times \frac{\ln(101)}{\ln(2)} \approx 6.658\text{ Mbps}$

3. **Transmission Time Required ($t = \frac{\text{Payload}}{R}$):**
   * $t_1 = \frac{100\text{ kbits}}{3459\text{ kbps}} = 0.02891\text{ s} = 28.91\text{ ms}$
   * $t_2 = \frac{200\text{ kbits}}{2057\text{ kbps}} = 0.09721\text{ s} = 97.21\text{ ms}$
   * $t_3 = \frac{150\text{ kbits}}{6658\text{ kbps}} = 0.02253\text{ s} = 22.53\text{ ms}$
   * $\text{Total Time} = 28.91 + 97.21 + 22.53 = \mathbf{148.65\text{ ms}}$  
   **Conclusion:** Since $148.65\text{ ms} > 100\text{ ms}$, the frame is **INFEASIBLE**.

4. **(a) Minimum Bandwidth Required:**  
   Since $t \propto \frac{1}{B}$:
   $$B_{\min} = 1\text{ MHz} \times \left( \frac{148.65\text{ ms}}{100\text{ ms}} \right) = \mathbf{1.4865\text{ MHz}}$$

5. **(b) Scaled Maximum Payloads at $1\text{ MHz}$ within $100\text{ ms}$:**  
   $$\text{Scaling factor } \alpha = \frac{100}{148.65} \approx 0.67274$$
   * $D_1' = 100\text{ kbits} \times 0.67274 = \mathbf{67.27\text{ kbits}}$
   * $D_2' = 200\text{ kbits} \times 0.67274 = \mathbf{134.55\text{ kbits}}$
   * $D_3' = 150\text{ kbits} \times 0.67274 = \mathbf{100.91\text{ kbits}}$

---

#### Solved Problem 6 (Edge Offload vs. Local Processing — Slide Problem 3)
> **Problem Statement:**  
> A device executes a job requiring $2 \times 10^8$ CPU cycles once per second.  
> - **Local:** CPU frequency $f = 200\text{ MHz}$, energy per cycle $e_c = 10^{-10}\text{ J}$.  
> - **Offload:** Transmit $D = 500\text{ kb}$ to edge node. Channel $B = 1\text{ MHz}$, $\text{SNR} = 10\text{ dB}$, $P_{\text{Tx}} = 100\text{ mW} = 0.1\text{ W}$. Edge compute time and downlink delays are negligible.  
> Compare latency and energy consumption.

**Solution:**

* **Local Execution:**
  $$t_{\text{local}} = \frac{2 \times 10^8\text{ cycles}}{200 \times 10^6\text{ cycles/s}} = \mathbf{1.0\text{ s}}$$
  $$E_{\text{local}} = 2 \times 10^8 \times 10^{-10}\text{ J} = \mathbf{0.02\text{ J}}$$

* **Offloaded Execution:**
  $$R = 10^6 \times \log_2(1 + 10) = 3.459\text{ Mbps}$$
  $$t_{\uparrow} = \frac{500\text{ kbits}}{3459\text{ kbps}} = \mathbf{0.1445\text{ s}}$$
  $$E_{\uparrow} = P_{\text{Tx}} \times t_{\uparrow} = 0.1\text{ W} \times 0.1445\text{ s} = \mathbf{0.01445\text{ J}}$$

* **Conclusion:**  
  Offloading is **superior** in both metrics:  
  - **Latency:** Reduced by $85.55\%$ ($0.1445\text{ s}$ vs $1.0\text{ s}$).  
  - **Energy:** Reduced by $27.75\%$ ($0.01445\text{ J}$ vs $0.02\text{ J}$).

---

# Module 2: IoT Architectures & System Design (Guaranteed 10 Marks)

---

### 2.1 The IoT World Forum (IoTWF) 7-Layer Reference Model

```
Top (Business Value)
 ▲  Layer 7: Collaboration & Processes (People, business decisions, workflow)
 │  Layer 6: Application (UI, analytics dashboards, mobile apps)
 │  Layer 5: Data Abstraction (Business logic, data modeling, schema normalization)
 │  Layer 4: Data Accumulation (Storage in DBs, data lakes, time-series DBs)
 │  Layer 3: Edge Computing (Data pre-filtering, anomaly detection, packet reduction)
 │  Layer 2: Connectivity (Routing, switching, transmission: 802.15.4, 6LoWPAN, Wi-Fi)
 ▼  Layer 1: Physical Devices & Controllers ("Things", sensors, actuators, MCUs)
Bottom (Physical World)
```

#### Detailed Breakdown of Layers

1. **Layer 1: Physical Devices & Controllers**  
   The "Things" layer. Includes sensors that convert analog environmental phenomena into digital signals (temperature, vibration, PIR) and actuators that effect physical changes (relays, valves, motors). Includes endpoint controllers (ESP32, STM32).
2. **Layer 2: Connectivity**  
   Responsible for reliable transmission across physical and data-link media. Handles protocol conversion, packet switching, and network routing. Technologies: IEEE 802.15.4, LoRaWAN, BLE, Cellular (NB-IoT, LTE-M), 6LoWPAN.
3. **Layer 3: Edge Computing**  
   Transforms "data in motion" into localized insights before overloading the network. Converts raw sensor data streams into manageable packets through filtering, threshold evaluation, and data aggregation.
4. **Layer 4: Data Accumulation (Storage)**  
   Converts data from network streams into persistent storage ("data at rest"). Organizes unstructured raw payloads into relational models, non-relational time-series formats, or distributed data lakes (e.g., AWS S3, DynamoDB).
5. **Layer 5: Data Abstraction**  
   Reconciles differing formats across multi-vendor fleets into unified schemas. Handles API integration, semantics, ontologies (e.g., OPC-UA), and role-based data access.
6. **Layer 6: Application**  
   Software programs that process data to deliver software services. Examples: web dashboards, predictive maintenance modules, mobile monitoring apps.
7. **Layer 7: Collaboration & Processes**  
   The human/enterprise dimension where business intelligence triggers business actions. Integrates into ERP/CRM workflows, stakeholder alerts, and operational policy modifications.

---

### 2.2 Comparison: 3-Layer vs. 5-Layer vs. 7-Layer IoT Architectures

```
 3-Layer Model             5-Layer Model                      7-Layer (IoTWF)
┌────────────────┐        ┌─────────────────────────┐        ┌─────────────────────────┐
│                │        │ Layer 5: Application    │        │ Layer 7: Collaboration  │
│ Layer 3:       │───────>│ (UI / Dashboards)       │───────>│ Layer 6: Application    │
│ Application    │        ├─────────────────────────┤        ├─────────────────────────┤
│                │        │ Layer 4: Middleware     │        │ Layer 5: Abstraction    │
│                │        │ (Data Mgmt, Broker)     │        │ Layer 4: Accumulation   │
├────────────────┤        ├─────────────────────────┤        ├─────────────────────────┤
│ Layer 2:       │───────>│ Layer 3: Transport      │───────>│ Layer 3: Edge Computing │
│ Network        │        │ (Routing, Network)      │        │ Layer 2: Connectivity   │
├────────────────┤        ├─────────────────────────┤        ├─────────────────────────┤
│                │        │ Layer 2: Processing     │        │                         │
│ Layer 1:       │───────>│ (Edge, MCU Logic)       │───────>│ Layer 1: Physical       │
│ Perception     │        ├─────────────────────────┤        │ Devices & Controllers   │
│                │        │ Layer 1: Perception     │        │                         │
└────────────────┘        └─────────────────────────┘        └─────────────────────────┘
```

* **Perception $\rightarrow$ Physical:** Sensors & actuators interacting with physical phenomena.
* **Network $\rightarrow$ Transport/Connectivity:** Physical/link/network routing stacks.
* **Middleware / Accumulation / Processing:** Sits between raw transmission and the end-user app to provide analytics, storage, message brokering, and hardware abstraction.

---

### 2.3 IoT System Levels (Level 1 to Level 6)

The standard classification (by Arshdeep Bahga & Vijay Madisetti) defines how sensing, analysis, storage, and presentation are distributed between **Local** nodes and the **Cloud**:

```
Level 1: Local Sensing + Local Storage + Local Analytics + Local App (Single Board, e.g. Home temp display)
Level 2: Local Sensing + Local Analytics + Cloud Storage + Cloud App (Data volume large, analytics light)
Level 3: Local Sensing + Cloud Storage + Cloud Analytics + Cloud App (Computationally intensive)
Level 4: Multiple Nodes + Local Analytics + Cloud Storage/Analytics + Observer Nodes
Level 5: Multiple End Nodes + Coordinator Node (WSN) + Cloud Storage/Analytics (Distributed clusters)
Level 6: Multiple Independent End Nodes + Centralized Controller + Cloud Analytics + Cloud Database
```

```
                   LEVEL 5 ARCHITECTURE DIAGRAM
 ┌────────────────────────────────────────────────────────┐
 │                      LOCAL DOMAIN                      │
 │                                                        │
 │   [End Node 1] ──┐                                     │
 │   (Sensor Only)  │ 802.15.4 /                          │
 │                  ▼ BLE                                 │
 │   [End Node 2] ───> [Coordinator Node]                 │
 │   (Sensor Only)    (Aggregates / Gateway)              │
 │                          │                             │
 └──────────────────────────┼─────────────────────────────┘
                            │ IP Uplink (MQTT / HTTPS / 4G)
 ┌──────────────────────────▼─────────────────────────────┐
 │                      CLOUD DOMAIN                      │
 │                                                        │
 │   ┌─────────────────┐       ┌──────────────────────┐   │
 │   │  Cloud Storage  │<─────>│ Analytics Engine     │   │
 │   │ (Time-Series DB)│       │ (AI/ML Predictions)  │   │
 │   └────────┬────────┘       └──────────┬───────────┘   │
 │            │                           │               │
 │            ▼                           ▼               │
 │   ┌────────────────────────────────────────────────┐   │
 │   │     Application Service / End-User Dashboards  │   │
 │   └────────────────────────────────────────────────┘   │
 └────────────────────────────────────────────────────────┘
```

---

### 2.4 Master Design Question: Smart Campus Architecture (2025 Exam Q2 [10 Marks])

> **Question:**  
> Design the IoT-WF based IoT system architecture of level 5 and beyond to make our university an IoT enabled smart academic campus to optimize **energy**, **space**, **mobility**, and **safety**.

#### Complete Design Blueprint

```
                     SMART CAMPUS ARCHITECTURE OVERVIEW
                     
 [Layer 7: Collaboration]   Facilities Directorate, Security Control, Campus Green Policy
                                          ▲
 [Layer 6: Applications]    Energy Optimization, Space Scheduler, Parking/Nav, Emergency App
                                          ▲
 [Layer 5: Abstraction]     Unified Campus Data Models, oneM2M Middleware, REST APIs
                                          ▲
 [Layer 4: Accumulation]    AWS IoT Core / InfluxDB (Time Series) + DynamoDB + S3 Lake
                                          ▲
 [Layer 3: Edge Computing]  Building Gateway Hubs (Raspberry Pi 4 / BeagleBone) 
                            - Pre-filters noise, evaluates safety-critical rules locally
                                          ▲
 [Layer 2: Connectivity]    LoRaWAN (Campus wide) + Zigbee Mesh (Rooms) + Wi-Fi 6 / 6LoWPAN
                                          ▲
 [Layer 1: Physical Things] Energy: Smart Meters, HVAC relays | Space: PIR, ToF crowd counters
                            Mobility: Boom-barriers, RFID    | Safety: Smoke, Gas, CO2, Panic
```

#### Layer-by-Layer Campus Implementation

1. **Layer 1: Physical Devices & Controllers (Subsystems Mapping)**
   * **Energy Optimization:** Digital smart meters on electrical distribution boards; current sensing transformers; solid-state relays controlling corridor lighting and centralized air-conditioning (HVAC).
   * **Space Optimization:** Passive Infrared (PIR) sensors and ceiling Time-of-Flight (ToF) optical counters deployed in lecture halls and computer labs to evaluate real-time desk occupancy.
   * **Mobility Management:** Ultrasonic distance sensors in campus parking bays; automated RFID readers and ANPR (Automatic Number Plate Recognition) cameras at entry/exit gates.
   * **Safety & Security:** MQ-2 smoke/flammable gas sensors, indoor environmental CO2 air quality monitors, ambient flame detectors, and push-button panic alarms connected to ESP32 microcontrollers.

2. **Layer 2: Connectivity (Heterogeneous Networking)**
   * **Indoor Room Level (Short-range, ultra-low power):** Zigbee mesh networks (IEEE 802.15.4) allow room sensors to route data to the departmental floor router without Wi-Fi congestion.
   * **Campus-Wide Outdoor (Long-range, low throughput):** LoRaWAN ($868\text{ MHz}$) connects outdoor parking sensors and perimeter safety nodes directly to campus base stations up to $5\text{ km}$ away.
   * **High Throughput Nodes:** Wi-Fi 6 ($802.11\text{ax}$) handles high-density surveillance cameras.
   * **Network Protocol:** 6LoWPAN provides end-to-end IPv6 logical addressing for constrained microcontrollers.

3. **Layer 3: Edge Computing (Level 5 Coordinator Nodes)**
   * Floor-level edge gateways (Raspberry Pi 4 running Linux + Edge runtime / FreeRTOS micro-edge controllers) receive raw telemetry from local Zigbee/LoRa coordinators.
   * **Local Real-Time Actions:** If an emergency gas leak or smoke threshold is exceeded, the edge gateway directly trips local ventilation relays within $<100\text{ ms}$, bypassing cloud round-trip delay.
   * **Data Aggregation:** Compresses 1-second temperature and occupancy samples into 1-minute averages, cutting cloud bandwidth demand by over $90\%$.

4. **Layer 4: Data Accumulation (Cloud Ingestion & Storage)**
   * Data packets arrive at an enterprise broker (e.g., AWS IoT Core / Azure IoT Hub) over secure MQTT over TLS.
   * Sensor time-series feeds are pushed into high-write databases (e.g., InfluxDB / Amazon Timestream). Unstructured video/logs route to AWS S3.

5. **Layer 5: Data Abstraction**
   * Translates multi-vendor protocols into standard oneM2M schemas.
   * Manages Virtual Device Representations ("Device Shadows" / "Device Twins") representing the virtual state of lecture halls (e.g., `Room_301: {occupied: true, ac_setpoint: 24, power_draw: 1.2kW}`).

6. **Layer 6: Application Layer**
   * Web dashboards and cross-platform mobile apps for campus managers and students:
     * *Energy Manager:* Automated HVAC scheduling based on student timetable integration.
     * *Campus Mobility App:* Real-time map displaying vacant parking spots and shuttle bus locations.
     * *Automated Room Booking:* Dynamically frees room reservations if no human presence is detected after 15 minutes.

7. **Layer 7: Collaboration & Business Processes**
   * Integrates insights directly into operational policies: automatically generates work orders for facility teams, sends SMS alerts to campus security during fire events, and delivers monthly ESG sustainability reports.

---

# Module 3: Access Technologies & Communication Protocols

---

### 3.1 Access Technology Breakdown: Zigbee, Bluetooth/BLE & NFC

This addresses **2024 Q4 [10 Marks]** and **2025 Q3 [5 Marks]** (which requires: Working Principle, Network Architecture, Packet Structure, Technical Specifications).

```
┌─────────────────┬──────────────────────┬──────────────────────┬──────────────────────┐
│ Metric          │ Zigbee               │ Bluetooth / BLE      │ NFC                  │
├─────────────────┼──────────────────────┼──────────────────────┼──────────────────────┤
│ Standard        │ IEEE 802.15.4        │ IEEE 802.15.1        │ ISO/IEC 18092        │
│ Frequency       │ 2.4 GHz, 868/915 MHz │ 2.4 GHz ISM Band     │ 13.56 MHz            │
│ Range           │ 10 – 100 m           │ BLE: 10–50 m (Mesh)  │ < 10 cm (typically 4)│
│ Max Data Rate   │ 250 kbps             │ BLE: 1–2 Mbps        │ Up to 424 kbps       │
│ Topologies      │ Star, Tree, Mesh     │ Piconet / Scatternet │ Point-to-point       │
│ Power Target    │ Ultra-low (years)    │ Ultra-low (BLE)      │ Passive / Negligible │
│ Channel Access  │ CSMA/CA              │ FHSS (1600 hops/sec) │ Inductive Coupling   │
└─────────────────┴──────────────────────┴──────────────────────┴──────────────────────┘
```

---

#### 3.1.1 Zigbee (Deep Dive for Q3 Architecture / Packet Question)

```
                       ZIGBEE MESH TOPOLOGY
                       
                         [Coordinator] (ZC)
                            /         \
                           ▼           ▼
                      [Router] (ZR)  [Router] (ZR)
                       /      \            \
                      ▼        ▼            ▼
                   [ZED]      [ZED]       [ZED]
                   
       ZC: Sets channel, PAN ID, security key, routes packets
       ZR: Relays packets across hops, always powered
       ZED: Sleeps continuously, wakes briefly, battery operated
```

1. **Working Principle:**  
   Zigbee operates on top of the IEEE 802.15.4 physical and MAC layers. It uses CSMA-CA (Carrier Sense Multiple Access with Collision Avoidance) to access wireless channels in the license-free $2.4\text{ GHz}$ ISM band. It minimizes power consumption through aggressive duty cycling: End Devices remain in sleep mode ($<1\ \mu\text{A}$) and only power up their transceivers when sending data to their parent router.

2. **Network Architecture (Node Roles):**
   * **Zigbee Coordinator (ZC):** Exactly one per network. Initializes the PAN (Personal Area Network), selects the RF channel, assigns 16-bit short network addresses, and holds the root security trust center.
   * **Zigbee Router (ZR):** Intermediate nodes that remain permanently powered. They execute routing tables, forward packets across multiple hops, and allow child nodes to join.
   * **Zigbee End Device (ZED):** Constrained, battery-powered sensor/actuator nodes. They do not forward traffic; they talk only to their parent router and sleep between cycles.

3. **Packet Structure / Formation:**  
   Total Maximum Physical Layer Protocol Data Unit (PPDU) is **127 bytes**:

```
 4 Bytes    1 Byte     1 Byte       0 - 127 Bytes (PHY Payload / PSDU)
┌──────────┬───────┬────────────┬───────────────────────────────────────────┐
│ Preamble │  SFD  │ Frame Len  │ MAC Layer Payload (MPDU)                  │
└──────────┴───────┴────────────┴───────────────────────────────────────────┘
                                 ┌─────────┬─────────┬───────────┬─────────┐
                                 │ Frame   │ Seq Num │ Address   │ Payload │
                                 │ Control │ (1 Byte)│ Fields    │ (Data)  │
                                 │ (2 Byte)│         │ (Up to 20)│ + FCS   │
                                 └─────────┴─────────┴───────────┴─────────┘
```
   * *Preamble (4 Bytes):* Synchronization.
   * *Start of Frame Delimiter - SFD (1 Byte):* Pattern `0xA7`.
   * *Frame Length (1 Byte):* Specifies PSDU size (max 127 bytes).
   * *MAC Layer:* Contains Frame Control, Sequence Number, Destination/Source PAN ID and Addresses, followed by 128-bit AES encrypted payload and 2-byte Frame Check Sequence (FCS/CRC).

4. **Key Technical Specifications:**  
   * RF Band: $2.4\text{ GHz}$ (16 channels, $5\text{ MHz}$ spacing).
   * Modulation: O-QPSK (Offset Quadrature Phase Shift Keying).
   * Range: $10\text{ m}$ to $100\text{ m}$ indoor line-of-sight.
   * Data rate: $250\text{ kbps}$.
   * Security: 128-bit AES encryption at Network and Application Support (APS) layers.

---

#### 3.1.2 Near Field Communication (NFC)

1. **Working Principle:**  
   Operates via **inductive magnetic coupling** between two loop antennas tuned to $13.56\text{ MHz}$ located within each other's near field ($<10\text{ cm}$).
   * The **Poller (Initiator/Reader)** drives an alternating RF current through its coil, creating an electromagnetic field.
   * The **Listener (Target/Tag)** intercepts this magnetic field. In passive tags, this field induces current via Faraday's Law of Induction, powering up the tag's internal microchip (Energy Harvesting).
   * **Data Transmission:** Forward direction uses Amplitude Shift Keying (ASK); reverse direction uses **Load Modulation** (the tag varies its coil's impedance, altering current draw from the reader, which the reader detects as amplitude changes).

2. **Operating Modes:**
   * **Reader/Writer Mode:** Active reader reads/writes data to passive unpowered tags (e.g., smart posters, asset tags).
   * **Card Emulation Mode:** Active device (e.g., smartphone) behaves like a standard contactless ISO 14443 smart card (e.g., Apple Pay / Google Wallet terminals, door access cards).
   * **Peer-to-Peer (P2P) Mode:** Two active NFC devices establish a bi-directional link to exchange data (e.g., Android Beam, contact sharing).

3. **Protocol Layers:**
   * **Physical Layer:** $13.56\text{ MHz}$ carrier frequency, ISO/IEC 18092 / 14443.
   * **Logical Link Control Protocol (LLCP):** Connects endpoints, manages point-to-point link arbitration and error flow.
   * **Application Layer (NDEF):** *NFC Data Exchange Format*, standard lightweight binary format encapsulating URLs, text, or vCards.

---

### 3.2 Bus Interconnects: SPI vs. I2C (2024 Exam Q3 [10 Marks])

```
                     SPI (4-Wire Bus)                         I2C (2-Wire Bus)
             ┌─────────────┐                          ┌─────────────┐
             │ Master Unit │                          │ Master Unit │
             └──┬──┬──┬──┬─┘                          └───┬─────┬───┘
    SCLK        │  │  │  │                                │     │   Pull-up Resistors
   ─────────────┼──┼──┼──┼───────────────       SCL   │     │   (Rp to 3.3V)
    MOSI        │  │  │  │                 ───────────────┼─────┼────────────
   ─────────────┼──┼──┼──┼───────────────       SDA   │     │
    MISO        │  │  │  │                 ───────────────┴─────┼────────────
   ─────────────┼──┼──┼──┼───────────────                       │
    SS1 ────────┴──┼──┼──┼───────────────> Slave 1              ▼
    SS2 ───────────┴──┼──┼───────────────> Slave 2       ┌──────────────┐
    SS3 ──────────────┴──┼───────────────> Slave 3       │ Slave Device │
                         ▼                               │  (Address)   │
                                                         └──────────────┘
```

| Parameter | SPI (Serial Peripheral Interface) | I2C (Inter-Integrated Circuit) |
| :--- | :--- | :--- |
| **Origin** | Motorola (1979) | Philips Semiconductors (1982) |
| **Wire Count** | 4 wires minimum ($+1$ SS line per additional slave) | Exactly 2 wires regardless of slave count |
| **Signal Lines** | **SCLK** (Clock), **MOSI** (Master Out), **MISO** (Master In), **SS/CS** (Slave Select) | **SDA** (Serial Data), **SCL** (Serial Clock) |
| **Bus Topology** | Single-Master (typical), multi-slave via chip-select | Multi-Master and Multi-Slave capable |
| **Duplex** | Full Duplex (simultaneous Tx/Rx) | Half Duplex (bidirectional over single SDA) |
| **Data Rates** | Very High ($>10\text{ Mbps}$ to $50+\text{ Mbps}$) | Standard: $100\text{ kbps}$, Fast: $400\text{ kbps}$, High-Speed: $3.4\text{ Mbps}$ |
| **Addressing** | Hardware pin selection (pulling SS low selects device) | Software addressing (7-bit or 10-bit address header) |
| **Overhead** | Minimal (pure data shifting, zero addressing overhead) | Higher (Start/Stop conditions, 7-bit address, ACK/NACK bits) |
| **Hardware Complexity**| High pin consumption on MCU; simpler silicon logic | Conserves MCU pins (only 2); needs pull-up resistors ($4.7\text{ k}\Omega$) |

#### Working Principle of I2C Bus Communication
1. **START Condition:** Initiated by Master pulling SDA LOW while SCL is HIGH.
2. **Address Frame:** Master transmits 7-bit device address + 1 Read/$\overline{\text{Write}}$ bit ($0 = \text{Write}, 1 = \text{Read}$).
3. **ACK/NACK:** Target slave pulls SDA LOW on the 9th clock pulse to acknowledge receipt.
4. **Data Frames:** Data transmitted in 8-bit bytes, MSB first, each followed by an ACK/NACK bit.
5. **STOP Condition:** Master releases SDA to transition from LOW to HIGH while SCL remains HIGH.

---

### 3.3 Application Layer Protocols: MQTT vs. CoAP

| Feature | MQTT (Message Queuing Telemetry Transport) | CoAP (Constrained Application Protocol) |
| :--- | :--- | :--- |
| **Standard** | OASIS / ISO/IEC 20922 | IETF RFC 7252 |
| **Transport** | **TCP** (Connection-oriented, reliable) | **UDP** (Connectionless, datagram) |
| **Architecture** | Broker-based **Publish/Subscribe** | Client/Server **RESTful Request/Response** |
| **Header Overhead** | Extremely lightweight: **2-byte fixed header** | Compact: **4-byte fixed binary header** |
| **Communication** | Asynchronous (broker decouples client states) | Synchronous & Asynchronous (Supports CoAP Observe) |
| **Security** | TLS/SSL over TCP | DTLS (Datagram TLS) over UDP |
| **Ideal Use Case** | Continuous telemetry streaming, cloud analytics, mobile apps | Constrained mesh networks, sleepy sensor nodes |

```
                MQTT MESSAGE FORMAT (Fixed Header = 2 Bytes)
 7             4 3   2 1    0
┌───────────────┬───┬──────┬──────┐
│  Packet Type  │DUP│ QoS  │RETAIN│  Byte 1: Control Packet Flags
│  (4 Bits)     │1b │2 Bits│ 1 Bit│
├───────────────┴───┴──────┴──────┤
│    Remaining Length (1-4 Bytes) │  Byte 2 (up to 4): Encoded with continuation bit (CB)
├─────────────────────────────────┤
│    Variable Header (Optional)   │  Bytes 3+: Packet ID, Topic Names
├─────────────────────────────────┤
│    Payload (Data / Telemetry)   │  Application payload
└─────────────────────────────────┘
```

#### MQTT Quality of Service (QoS) Mechanics

```
    QoS 0: At-Most-Once                 QoS 1: At-Least-Once                QoS 2: Exactly-Once
      (Fire & Forget)                      (Acknowledged)                   (Four-Step Handshake)

 Client             Broker            Client             Broker            Client             Broker
   │                  │                 │                  │                 │                  │
   │─── PUBLISH ─────>│                 │─── PUBLISH ─────>│                 │─── PUBLISH ─────>│
   │   (No ACK,       │                 │   (Store local)  │                 │   (Store local)  │
   │    No Retry)     │                 │<── PUBACK ───────│                 │<── PUBREC ───────│
   ▼                  ▼                 │   (Delete local) │                 │─── PUBREL ──────>│
                                        ▼                  ▼                 │<── PUBCOMP ──────│
                                                                             │   (Safe delete)  │
                                                                             ▼                  ▼
```

* **QoS 0 (At-Most-Once):** Best-effort delivery. No retries, no acknowledgment. A dropped TCP packet means permanent data loss. Suitable for frequent environmental telemetry (e.g., ambient temperature every second).
* **QoS 1 (At-Least-Once):** Packet is stored locally by the sender until a `PUBACK` is received. If the acknowledgment timer expires, the packet is resent with the `DUP` flag set to 1. Handshake guarantees delivery, but may produce duplicate messages at the receiver.
* **QoS 2 (Exactly-Once):** Four-way handshake (`PUBLISH` $\rightarrow$ `PUBREC` $\rightarrow$ `PUBREL` $\rightarrow$ `PUBCOMP`). Prevents duplicate message delivery. Used for critical transactional actions (e.g., billing, activating safety actuators, locking doors).

---

# Module 4: Embedded Platforms, OS & Programming Frameworks

---

### 4.1 Embedded Platform Spectrum: MCU vs. MPU vs. SBC

| Dimension | Microcontroller (MCU) | Single Board Computer (SBC) |
| :--- | :--- | :--- |
| **Examples** | ESP32, STM32, ATmega328P | Raspberry Pi 4/5, BeagleBone Black |
| **Architecture** | Self-contained: CPU + Flash + SRAM on one die | MPU (SoC) requiring external RAM, Flash/SD card |
| **Clock / Power** | Tens to hundreds of MHz (e.g., ESP32 @ $240\text{ MHz}$) | Multi-core Gigahertz (e.g., RPi 4 Quad @ $1.5\text{ GHz}$) |
| **Power Draw** | Milliwatts ($\text{mW}$) to Microwatts ($\mu\text{W}$ in deep sleep) | Watts ($2.5\text{ W} - 15\text{ W}$), unsuited for small batteries |
| **Operating System**| Bare-metal or Real-Time OS (FreeRTOS, Zephyr) | Full General-Purpose OS (Linux Debian/Ubuntu) |
| **Timing Behavior** | **Deterministic (Hard/Soft Real-time)** | **Non-deterministic (Best-effort execution)** |
| **Best Used For** | Direct sensor sampling, PWM motor driving, battery motes | Edge gateways, local video/vision AI, data brokering |

---

### 4.2 RTOS Fundamentals & FreeRTOS Architecture (Question Bank Q19, Q21, Q22)

#### Definition of RTOS
A Real-Time Operating System (RTOS) is an operating system designed to process inputs and produce outputs within **guaranteed, strictly bounded time windows (deadlines)**.  
*Key principle:* In an RTOS, **correctness depends not only on logical output, but on the time at which the output is delivered**. A late result is considered a failed result.

#### The Four FreeRTOS Task States

```
                 ┌───────────────┐
                 │   SUSPENDED   │
                 └───────▲───────┘
         vTaskSuspend()  │   ▲ vTaskResume()
                         │   │
                         │   │
       Task Creation     │   │
             │           │   │
             ▼           │   │
       ┌───────────┐     │   │     ┌───────────┐
       │   READY   │─────┴───┴────>│  RUNNING  │
       └─────▲─────┘  Dispatched   └─────┬─────┘
             │        by Scheduler       │
             │                           │
  Event Occurs /                         │ Calls Blocking API
  Delay Expires                          │ (vTaskDelay, Queue read)
             │                           │
             │       ┌───────────┐       │
             └───────┤  BLOCKED  │<──────┘
                     └───────────┘
```

1. **Running:** The task is actively executing instructions on a CPU core. (On a single-core MCU, only one task can be in this state at any instant).
2. **Ready:** The task is ready to execute, but is currently waiting for the scheduler to allocate CPU time because an equal or higher-priority task is currently running.
3. **Blocked:** The task is waiting for an external event or resource (e.g., waiting for an interval timer via `vTaskDelay()`, waiting for data on an empty Queue, or waiting to acquire a Mutex). It consumes zero CPU cycles while blocked.
4. **Suspended:** The task is explicitly removed from the scheduler's purview via `vTaskSuspend()`. It will remain dormant regardless of events until another task calls `vTaskResume()`.

#### The FreeRTOS Kernel Building Blocks
* **Priority-Based Preemptive Scheduler:** Each task is assigned an integer priority (e.g., 1 to 5). The scheduler guarantees that the **highest-priority READY task will immediately seize the CPU**. If an interrupt or unblocking event makes a higher-priority task Ready, the currently running lower-priority task is preempted. Tasks of equal priority share the CPU using round-robin time slicing.
* **Queues (FIFO Buffers):** Thread-safe inter-task data pipelines. Tasks write data using `xQueueSend()` and read data using `xQueueReceive()`. If a consumer task attempts to read from an empty queue, it automatically enters the **Blocked** state, freeing the CPU for other operations until a producer posts data.
* **Semaphores & Mutexes:**
  * *Binary Semaphore:* Single-token flag used primarily for synchronization between Interrupt Service Routines (ISRs) and tasks.
  * *Mutex (Mutual Exclusion):* A binary token designed for resource protection (e.g., guarding access to a single hardware I2C port).  
  * **Priority Inversion & Priority Inheritance:** If a low-priority task holds a mutex required by a high-priority task, execution can be blocked by intermediate tasks. FreeRTOS mutexes resolve this via **priority inheritance**, temporarily promoting the low-priority task to match the blocked task's higher priority until it releases the shared mutex.

---

### 4.3 IoT Programming Framework Shootout

| Metric | Arduino Framework | ESP-IDF (Espressif IoT Dev Framework) | MicroPython | FreeRTOS (Bare-metal) |
| :--- | :--- | :--- | :--- | :--- |
| **Language** | Simplified C/C++ | Native C (C99 / C++11) | Python 3 dialect | Pure C |
| **Abstraction** | Very High (`setup()`, `loop()`) | Low-to-Moderate (Direct register & API access)| High (Python byte-code interpreter)| Low (Direct API and hardware drivers) |
| **Concurrency** | Single-threaded "Superloop"; `delay()` blocks CPU | Native Preemptive Multi-tasking (built on FreeRTOS) | Cooperative event loop (`asyncio`); limited preemptive threads | Preemptive multi-tasking |
| **Memory Footprint**| Low-Moderate | Small, optimized for chip flash | Large (requires $\sim 256\text{ KB}+$ RAM for runtime) | Minimal ($\sim 6\text{ KB} - 12\text{ KB}$ flash) |
| **Learning Curve**| Gentle (Beginner friendly) | Steep (Demands understanding of pointers, CMake, RTOS) | Very Gentle (Interactive REPL prompt) | Steep |
| **Suitability** | Rapid educational prototypes | Commercial production firmwares | Quick edge scripting, hardware validation | Hard real-time deterministic control |

#### Essential Code Implementations

##### 1. Arduino Framework (ESP32 / ESP8266 Blinking LED)
```cpp
const int LED_PIN = 2;

void setup() {
  pinMode(LED_PIN, OUTPUT); // Configure GPIO 2 as digital output
}

void loop() {
  digitalWrite(LED_PIN, HIGH); // Turn LED ON (3.3V)
  delay(1000);                 // Blocking delay (freezes loop execution)
  digitalWrite(LED_PIN, LOW);  // Turn LED OFF (0V)
  delay(1000);
}
```

##### 2. FreeRTOS Task Implementation (Arduino-ESP32 Core)
```cpp
void vBlinkTask(void *pvParameters) {
  pinMode(2, OUTPUT);
  while(1) {
    digitalWrite(2, HIGH);
    // Non-blocking delay: blocks ONLY this task; frees CPU for other tasks
    vTaskDelay(1000 / portTICK_PERIOD_MS);
    digitalWrite(2, LOW);
    vTaskDelay(1000 / portTICK_PERIOD_MS);
  }
}

void setup() {
  // Arguments: Task Function, Name, Stack Size (bytes), Param, Priority, Handle
  xTaskCreate(vBlinkTask, "Blink Task", 2048, NULL, 1, NULL);
}

void loop() {
  // Loop remains empty; all operations execute in concurrent FreeRTOS tasks
}
```

##### 3. MicroPython (ESP32)
```python
import machine
import time

led = machine.Pin(2, machine.Pin.OUT)

while True:
    led.value(1)       # Drive GPIO2 HIGH
    time.sleep(1.0)    # Sleep 1 second
    led.value(0)       # Drive GPIO2 LOW
    time.sleep(1.0)
```

##### 4. Raspberry Pi Python (GPIO Interfacing - DHT/Relay)
```python
import RPi.GPIO as GPIO
import time

RELAY_PIN = 11

GPIO.setmode(GPIO.BOARD)       # Physical pin numbering scheme
GPIO.setup(RELAY_PIN, GPIO.OUT)

try:
    while True:
        GPIO.output(RELAY_PIN, GPIO.LOW)  # Active LOW relay: Turn ON
        time.sleep(2)
        GPIO.output(RELAY_PIN, GPIO.HIGH) # Turn OFF
        time.sleep(2)
except KeyboardInterrupt:
    GPIO.cleanup()                        # Safe pin reset on termination
```

---

# Module 5: IoT Virtualization & Resource Management

---

### 5.1 Virtualization in IoT (Question Bank Q18 & Unit 2 Lecture)

#### Definition
Virtualization in IoT refers to the **abstraction of physical hardware devices, sensors, actuators, network links, and computing resources into software-based virtual representations**.

#### Virtualization Categories in IoT
1. **Device & Sensor Virtualization ("Virtual Sensors"):** Software entities that emulate the behavior, reading streams, and interfaces of physical transducers. Enables parallel testing without field deployment, and combines multiple physical sensors into a single composite metric (e.g., combining temperature, humidity, and wind speed into an abstract "Comfort Index").
2. **Network Virtualization (Software-Defined Networking - SDN):** Slices physical access networks into isolated virtual channels. Allows mission-critical safety packets to run on a prioritized virtual slice separate from high-bandwidth, non-critical telemetry.
3. **Platform Virtualization (Containers vs. VMs):**
   * *Virtual Machines (VMs):* Emulate physical hardware via a Hypervisor; each instance runs a full Guest Operating System. High memory and processing overhead.
   * *Containers (e.g., Docker):* Share the host OS kernel and package only the application binaries and runtime dependencies. Lightweight footprint, rapid startup ($<1\text{ s}$), and ideal for edge compute gateways (Raspberry Pi).

```
┌──────────────────────────────────────┐     ┌──────────────────────────────────────┐
│       VIRTUAL MACHINES (VMs)         │     │         CONTAINERS (DOCKER)          │
├──────────────────┬───────────────────┤     ├──────────────────┬───────────────────┤
│ App A (User Code)│ App B (User Code) │     │ App A (User Code)│ App B (User Code) │
├──────────────────┼───────────────────┤     ├──────────────────┼───────────────────┤
│ Guest OS (Linux) │ Guest OS (Win)    │     │ Bins / Libraries │ Bins / Libraries  │
├──────────────────┴───────────────────┤     ├──────────────────┴───────────────────┤
│ Hypervisor (Type 1 / Type 2)         │     │ Container Engine (Docker Daemon)     │
├──────────────────────────────────────┤     ├──────────────────────────────────────┤
│ Host Operating System (Optional)     │     │ Host Operating System (Shared Linux) │
├──────────────────────────────────────┤     ├──────────────────────────────────────┤
│ Underlying Server Hardware           │     │ Underlying Edge Hardware (e.g., RPi) │
└──────────────────────────────────────┘     └──────────────────────────────────────┘
```

---

### 5.2 Key Resource Management Challenges in Constrained IoT

* **Compute Limitations:** 8-bit and 32-bit MCUs have minimal cycle throughput. Requires lightweight parsing libraries (CBOR instead of verbose JSON; binary protocols over plain text).
* **Memory Constraints:** MCUs feature small SRAM ($2\text{ KB}$ in ATmega328P to $520\text{ KB}$ in ESP32). Dynamic heap memory allocation can lead to heap fragmentation and kernel crashes. Static allocation is preferred.
* **Energy Scarcity:** Devices rely on non-rechargeable chemical cells or energy-harvesting transducers (solar, thermal). Firmware must minimize the duty cycle, keep radios off most of the time, and leverage deep sleep modes ($<10\ \mu\text{A}$).
* **Network Bandwidth Bottlenecks:** Low-rate channels (e.g., LoRaWAN at $250\text{ bps}$ to $50\text{ kbps}$, Zigbee at $250\text{ kbps}$) cannot handle standard HTTP/TCP headers. 6LoWPAN compresses 40-byte IPv6 headers down to 2–4 bytes to fit payloads within short frame budgets.

---

# Module 6: Rapid Revision "Cheat Sheet" & Final Night Checklist

Keep these essential constants, port numbers, pin allocations, and definitions top-of-mind entering the exam hall:

```
┌──────────────────────────┬────────────────────────────────────────────────────────┐
│ Concept / Item           │ Key Value / Specification to Remember                  │
├──────────────────────────┼────────────────────────────────────────────────────────┤
│ Default MQTT Port        │ 1883 (TCP Plaintext), 8883 (MQTT over TLS)             │
│ Default CoAP Port       │ 5683 (UDP Unencrypted), 5684 (CoAP over DTLS)          │
│ Zigbee Standard          │ IEEE 802.15.4 (Physical & MAC layer)                   │
│ Bluetooth Standard       │ IEEE 802.15.1 | BLE introduced in Bluetooth 4.0        │
│ NFC Operating Frequency  │ 13.56 MHz (Inductive Coupling, Range < 10 cm)          │
│ ESP32 ADC Resolution     │ 12-bit (Value Range: 0 to 4095 over 0V to 3.3V)        │
│ ESP32 ADC Voltage Calc   │ V_in = (ADC_reading / 4095) * 3.3V                     │
│ ESP32 PWM Resolution     │ 8-bit default (Value Range: 0 to 255)                  │
│ Restricted ESP32 Pins    │ GPIO 6–11 (Connected internally to SPI Flash - DO NOT USE)│
│ Input-Only ESP32 Pins    │ GPIO 34, 35, 36, 39 (No internal software pull-up)     │
│ MQTT Header Size         │ 2 Bytes fixed header (Byte 1: Type/Flags, Byte 2: RL)  │
│ CoAP Header Size         │ 4 Bytes fixed header (Ver, Type, Token Length, Code)   │
│ IEEE 802.15.4 Max Frame  │ 127 Bytes total physical layer packet (MTU)            │
│ FreeRTOS Delay Function  │ vTaskDelay(ms / portTICK_PERIOD_MS)                    │
└──────────────────────────┴────────────────────────────────────────────────────────┘
```

### High-Yield Diagram Checklist
Before the exam, practice sketching these 5 diagrams by hand:
1. **IoT-WF 7-Layer Architecture** (Layer 1 Physical up to Layer 7 Collaboration).
2. **FreeRTOS 4-State Machine** (Ready, Running, Blocked, Suspended + transitions).
3. **SPI vs. I2C Bus Topologies** (4-wire master-slave vs. 2-wire open-drain with pull-ups).
4. **MQTT QoS Levels** (QoS 0 single arrow, QoS 1 exchange, QoS 2 four-step handshake).
5. **Level 5 IoT Topology** (End nodes $\rightarrow$ Coordinator/Gateway $\rightarrow$ Cloud DB/Analytics $\rightarrow$ Apps).
