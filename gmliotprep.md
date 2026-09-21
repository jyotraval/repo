# IoT Mid-Semester Exam — Complete Study Prep

**Course:** Internet of Things (20IC401T / 201C401T)  
**Source Material:** Prof. Dr. Abhishek Joshi / Dr. Abhishek Kumar slides (Unit 1 & Unit 2), PYQs 2024 & 2025, IoT Numericals handout, IoT Question Bank.  
**Scope:** Mid-Sem → Unit 1 (Introduction to IoT) + Unit 2 (Technology for IoT).

---

## 0. Exam Pattern & Strategy (READ THIS FIRST)

### 0.1 PYQ Pattern Analysis

| Year | Marks | Duration | Q-Count | Style |
|------|-------|----------|---------|-------|
| **2024** | 50 | 2 hours | 5 questions | Heavy theory + design (no numerical) |
| **2025** | 25 | 1 hour | 3 questions | Numerical + design + access-tech |

### 0.2 Topic Frequency (last 2 years → high probability for 2026)

| Topic | 2024 | 2025 | 2026 Likelihood |
|-------|------|------|------------------|
| **Numericals** (battery/data-rate/latency) | ✗ | ✓ (10 marks) | 🔴 VERY HIGH |
| **IoT-WF 7-Layer Architecture + Levels** | ✓ (10M) | ✓ (10M) | 🔴 VERY HIGH |
| **Access Technologies** (BT/Zigbee/NFC/NB-IoT/Sigfox) | ✓ (10M) | ✓ (5M) | 🔴 VERY HIGH |
| **Sensors / Actuators / Embedded board** | ✓ (8M) | ✗ | 🟠 HIGH |
| **SPI & I2C Protocols** | ✓ (10M) | ✗ | 🟠 HIGH |
| **IoT System Design** (Framework+Virtualization+Distributed) | ✓ (12M) | ✗ | 🟡 MEDIUM |
| Resource Management / RTOS / Frameworks / Programming | ✗ | ✗ | 🟡 MEDIUM (QB has these) |

### 0.3 Suggested Time Allocation (1-hour exam, 25 marks)

- **5 min** — Read paper, plan answers, allocate marks-per-minute (1 mark ≈ 2.4 min).
- **15 min** — Numerical (Q1) — show every formula step.
- **25 min** — Architecture/Design (Q2) — draw the diagram FIRST, then explain.
- **12 min** — Short notes / access tech (Q3) — bullet points with diagrams.
- **3 min** — Re-check units, formula, numbers, labels.

### 0.4 Exam Day Rules (from the question paper itself)

1. Do not write anything except roll number on the question paper.
2. Assume suitable data wherever essential and **mention it clearly**.
3. **Writing appropriate units, nomenclature, and drawing neat sketches/schematics is an integral part of the answer.** → No diagram = marks lost even if text is correct.
4. Font: Times New Roman, size 12 (answer-paper convention).

---

# UNIT 1 — INTRODUCTION TO IoT

## 1.1 Definition of IoT

**Internet of Things (IoT)** is the network of smart physical objects — devices, vehicles, buildings, etc. — embedded with **sensors/actuators, computation unit, memory, power source, and network connectivity**, which enables the object to:

- **Collect and exchange data** with other devices/systems over the internet.
- **Analyze** the collected data to extract new insight.
- **Respond** accordingly without direct human intervention.

> **Goal of IoT:** *"Connect the unconnected."* — Kevin Ashton (coined the term "IoT" in 1999).

**Alternate (Gartner) Definition:**  
*"The Internet of Things (IoT) is the network of physical objects that contain embedded technology to communicate and sense or interact with their internal states or the external environment."*

### Historical Milestones (commonly asked 2-mark trivia)

| Year | Event |
|------|-------|
| 1982 | Carnegie Mellon students networked a Coca-Cola vending machine (first IoT-like device). |
| 1990 | John Romkey connected a toaster to the Internet (first IoT device). |
| 1991 | Cambridge students used a webcam to monitor a coffee pot. |
| 1999 | Kevin Ashton (MIT Auto-ID Center) coins "Internet of Things". |
| 2000s | LG launches the first internet-connected refrigerator. |

### IoT vs M2M (Frequently Asked)

| Aspect | M2M (Machine-to-Machine) | IoT |
|--------|--------------------------|-----|
| Communication | Point-to-point, no IP needed | Internet / IP-based |
| Data use | Local, closed | Cloud, analytics, cross-domain |
| Architecture | Vendor-specific silos | Open, standardized, layered |
| Scale | Tens-thousands of devices | Billions of devices |
| Intelligence | Mostly rule-based | Data-driven, AI/ML at edge/cloud |

---

## 1.2 Characteristics of IoT

Remember the **7 Cs & Ss mnemonic**: Smart, Connected, Configured, Identified, Interoperable, Intelligent, Communicating.

1. **Smart Devices** — Embedded processing & decision-making.
2. **Connected Devices** — Always-on network (Wi-Fi, BLE, LoRa, cellular, etc.).
3. **Unique Identity** — Each device has an IP address (IPv6) or unique ID.
4. **Zero / Self-Configuration** — Auto-discovery, auto-provisioning.
5. **Common Communication Network** — IP-based, standardized.
6. **Semantic Interoperability** — Common data models (JSON, CBOR, SenML).
7. **Collective Intelligence** — Aggregate data → cloud ML → smarter system over time.

---

## 1.3 Building Blocks of an IoT System

A generic IoT device contains the following hardware blocks:

```
        +------------------+
        |  Sensors (input) |  --> capture physical phenomena
        +------------------+
                 |
        +------------------+
        |  Processor/MCU   |  --> compute, decide, store locally
        +------------------+
                 |
        +------------------+
        |  Internet Radio  |  --> Wi-Fi / BLE / LoRa / cellular
        +------------------+
                 |
        +------------------+
        |  Actuators (op)  |  --> move, switch, alert
        +------------------+
        +------------------+
        |  Power Source    |  --> battery, harvesting, mains
        +------------------+
        +------------------+
        |  Memory/Storage  |  --> flash + RAM
        +------------------+
        +------------------+
        | Audio/Video I/F  |  --> mic, camera
        +------------------+
```

### IoT Components Overview (the 6 logical blocks)

```
                          Controller
IoT Device  ──>  Resources  ──>  Database
                          Service

              Application
   Analysis  ──>  Web Service
              Services
```

- **IoT Device** — Physical thing + sensors + actuators + connectivity.
- **Resource** — Memory, compute, energy, network bandwidth (constrained!).
- **Controller / Service** — Local service layer that orchestrates the device.
- **Database Service** — Stores device metadata + sensor readings.
- **Web Service** — Exposes device data to the internet (REST/MQTT).
- **Analysis Service** — Analytics / ML on aggregated data.

---

## 1.4 Things in IoT: Sensors & Actuators

### 1.4.1 Sensor — Definition

> A **sensor** is a transducer that converts a physical quantity (temperature, pressure, light, motion, gas concentration, etc.) into an electrical signal (voltage/current/frequency) that a processor can read.

### 1.4.2 Actuator — Definition

> An **actuator** is a transducer that converts an electrical command from the processor into a physical action (motion, switch, sound, heat, light).

### 1.4.3 Embedded Board — Definition

> An **embedded board** is a small-form-factor computer built around a microcontroller (MCU) or microprocessor (MPU), with on-board GPIO, ADC, communication interfaces (I2C/SPI/UART), memory, and power regulation — designed to run a specific, dedicated task such as sensing-and-actuating in an IoT node. Examples: Arduino Uno (AVR), ESP32 DevKit, Raspberry Pi Pico, STM32 Nucleo, BeagleBone Black.

### 1.4.4 Three Sensors You MUST Be Able to Illustrate (2024 Q1)

Pick any three from the table below — for each one: **Diagram + Technical Specification + Working Principle**.

#### Sensor A: DHT11 / DHT22 — Temperature & Humidity

- **Specs:** Temp range 0–50 °C (±2 °C), Humidity 20–90 %RH (±5 %), Vcc = 3.3–5 V, sampling 1 Hz (DHT11) / 0.5 Hz (DHT22), single-wire digital interface.
- **Working Principle:** A **NTC thermistor** measures temperature (resistance drops as T rises). A **capacitive humidity sensor** (dielectric polymer absorbs water vapour → capacitance changes). An onboard MCU digitises both readings and transmits a 40-bit packet over a single data line (8 hum + 8 hum-checksum + 8 temp + 8 temp-checksum).
- **Diagram (text-art):**
  ```
        +-----------+
  3.3V -| VCC       |
        |           |--- DATA  ──> GPIO (with 10 kΩ pull-up)
  GND  -| GND       |
        +-----------+
              DHT11 / DHT22
  ```

#### Sensor B: HC-SR04 — Ultrasonic Distance

- **Specs:** Operating voltage 5 V, current 15 mA, range 2 cm – 400 cm, resolution 0.3 cm, measuring angle <15°, frequency 40 kHz, trigger input 10 µs TTL pulse.
- **Working Principle:** A 10 µs HIGH pulse on the **TRIG** pin causes the module to emit eight 40 kHz ultrasonic bursts. The waves reflect off an obstacle and return to the receiver. The module sets the **ECHO** pin HIGH for a duration proportional to round-trip time. Distance is calculated as  
  **d = (speed of sound × time) / 2 = (343 m/s × t) / 2 ≈ t / 58 cm** (with t in µs).
- **Diagram:**
  ```
   TRIG ──> [TX 40 kHz] ))) ((( reflected )))) [RX] ──> ECHO (pulse-width)
        VCC = 5V, GND = 0V
        MCU measures pulse-width on ECHO using pulseIn().
  ```

#### Sensor C: LDR (Light Dependent Resistor) — Light Intensity

- **Specs:** Resistance ~1 MΩ in dark, ~1 kΩ in bright light, response time ~10 ms, peak spectral response ~540 nm, max voltage ~150 V DC, power ~100 mW.
- **Working Principle:** Made of CdS (cadmium sulphide) semiconductor. In the **dark**, few electron-hole pairs → high resistance. When **light** strikes, photons excite electrons to the conduction band → free carriers increase → resistance drops. Wired in a **voltage divider** with a fixed resistor; the divided voltage is read by an ADC and converted to lux.
- **Diagram:**
  ```
        3.3V
          |
        [R_fixed = 10 kΩ]
          |
          +──> ADC pin
          |
        [LDR]
          |
         GND
  ```

#### (Backup) Sensor D: PIR — Passive Infrared Motion

- **Specs:** Vcc 4.5–20 V, detection range up to 7 m, detection angle <100°, delay adjustable 5 s–4 min, quiescent current <60 µA, operating temp −20 to +80 °C.
- **Working Principle:** A **pyroelectric infrared sensor** (e.g. RE200B) responds to changes in IR radiation (8–14 µm wavelength — body heat). A Fresnel lens in front focuses IR from multiple zones onto two sensor elements wired in opposite polarity. When a warm body moves between zones, the differential signal spikes; an onboard BISS0001 comparator triggers the output HIGH for the set delay.
- **Diagram:** 3-pin module — VCC, GND, OUT (digital, active-HIGH).

#### (Backup) Sensor E: MQ-2 / MQ-135 — Gas Sensor

- **Specs:** Detects CH₄, LPG, CO, smoke, alcohol; 5 V heater; analog + digital output; preheat ~24 h on first use; sensing range 100–10000 ppm.
- **Working Principle:** A **SnO₂ (tin-dioxide) semiconductor** heater raises sensing element to ~300 °C. In clean air, oxygen adsorbs on the surface → high resistance. When a combustible gas is present, it reacts with adsorbed oxygen → electrons released → resistance drops. Output voltage across a load resistor is read by an ADC.

---

## 1.5 Technology Evolution (RFID → WSN → M2M → IoT)

| Stage | Year | Key Idea | Limitation That Pushed Next Stage |
|-------|------|-----------|------------------------------------|
| **Barcodes / RFID** | 1970s–1990s | Identify & track objects by radio | One-way, no sensing |
| **WSN (Wireless Sensor Networks)** | 1990s–2000s | Many low-power sensor nodes form a mesh | Closed, application-specific, no IP |
| **M2M** | 2000s | Devices talk point-to-point over cellular/SMS | No internet, no cloud, no scalability |
| **IoT** | 2010+ | IP-connected things + cloud + analytics + AI | → current paradigm |

The enabling shift at each stage:
- RFID → WSN: added **sensing** to identification.
- WSN → M2M: added **actuation + long-range** links.
- M2M → IoT: added **IP, cloud, analytics, semantic interoperability**.

---

## 1.6 IoT Reference Architectures

Three architectures are taught — **3-Layer, 5-Layer, and IoT-WF 7-Layer**. Memorize all three; the 7-layer is the most-asked.

### 1.6.1 Three-Layer Architecture (Basic)

```
   ┌────────────────────────┐
   │  Application Layer     │  → user apps, dashboards, business logic
   ├────────────────────────┤
   │  Network Layer         │  → routing, IP, gateways, Wi-Fi/cellular
   ├────────────────────────┤
   │  Perception Layer      │  → sensors, actuators, edge nodes
   └────────────────────────┘
```

### 1.6.2 Five-Layer Architecture (Expanded)

```
   ┌────────────────────────┐
   │  Application Layer      │  → end-user services (smart home, smart city)
   ├────────────────────────┤
   │  Business Layer        │  → business models, billing, analytics, KPIs
   ├────────────────────────┤
   │  Application Layer      │  → (sometimes split as "Service Layer")
   ├────────────────────────┤
   │  Processing / Middlew. │  → data analytics, edge compute, storage
   ├────────────────────────┤
   │  Transport / Network   │  → routing, gateways, IP
   ├────────────────────────┤
   │  Perception Layer       │  → sensors, actuators, MCU
   └────────────────────────┘
```

### 1.6.3 IoT-WF 7-Layer Architecture (World Forum IoT Reference Model) — MOST IMPORTANT

This is the **IEEE / Cisco World Forum** reference model — directly asked in 2024 (Q2) and 2025 (Q2). The 7 layers:

```
Layer 7 │  Application Layer        Smart city, healthcare, smart home, industry
Layer 6 │  (Collaboration / Bus.)   Business process, cross-domain orchestration
Layer 5 │  Data Abstraction /       Data virtualisation, aggregation, analytics,
        │  Analytics                reporting, dashboards
Layer 4 │  Data Accumulation        Storage, ETL, databases, data lakes
Layer 3 │  Edge Computing           Local processing, filtering, protocol conversion
Layer 2 │  Connectivity / Network   Gateways, routers, 6LoWPAN, IPv6
Layer 1 │  Physical / Devices       Sensors, actuators, embedded boards, RFID tags
```

**Layer-by-layer description (memorize this):**

| Layer | Name | Role | Examples |
|-------|------|------|----------|
| **L1** | Physical Devices | The "things" — sense & actuate | DHT11, PIR, ESP32, STM32, RFID tags |
| **L2** | Connectivity | Network protocols + gateways | Wi-Fi, BLE, Zigbee, LoRa, 6LoWPAN, MQTT brokers |
| **L3** | Edge Computing | Pre-process near the source — filter, aggregate, convert | ESP32 gateway, Azure IoT Edge, AWS Greengrass |
| **L4** | Data Accumulation | Persistent storage | DynamoDB, InfluxDB, time-series DB |
| **L5** | Data Abstraction | Virtualise data — REST APIs, schema, analytics | AWS IoT Rules Engine, Azure Stream Analytics |
| **L6** | Application (Collaboration) | Cross-domain business logic | Smart-fleet + smart-energy joint analysis |
| **L7** | Application (Presentation) | End-user dashboards & apps | ThingSpeak, Power BI, mobile app |

**Layer 5+** is what the 2025 question asks about — this means **Data Abstraction + Collaboration + Application** — i.e. the cloud-side analytics + business apps that turn raw sensor data into actionable insight.

### 1.6.4 Sample Architecture: Smart Home

```
[Temp sensor]──┐                                              ┌──> [Mobile App]
[Motion sensor]┼─> [Edge Gateway (RPi)] ─Wi-Fi─> [Cloud MQTT]─┼──> [Voice Assistant]
[Smart bulb]   ┘                                              └──> [Dashboard]
```

---

## 1.7 IoT Levels 1-6 (Component Placement) — Important for Q2 of 2025 PYQ

The 6 levels classify **how the IoT components (sensing, analysis, storage, application) are placed** between local node and cloud. Difficulty increases with level.

| Level | Nodes | Where analysis happens | Where data stored | Where app runs | Typical use |
|-------|-------|-------------------------|-------------------|----------------|-------------|
| **L1** | 1 | Locally on node | Locally on node | Locally | Low-cost single-node (e.g. smart switch) |
| **L2** | 1 | Locally | Cloud | Cloud | Single-node + big data (e.g. home weather station) |
| **L3** | 1 | Cloud | Cloud | Cloud | Big-data + heavy compute (e.g. image classifier) |
| **L4** | Multiple (local analysis) | Local | Cloud | Cloud + observer nodes | Multi-node WSN, e.g. environmental monitor |
| **L5** | Multiple + 1 coordinator | Cloud | Cloud | Cloud | WSN with coordinator → cloud (e.g. smart agriculture) |
| **L6** | Multiple independent | Cloud | Cloud | Cloud + central controller | Big mesh, central controller aware of all nodes (e.g. smart city) |

**For "Level 5 and beyond" (2025 Q2):** Design a smart campus with multiple end-nodes per building → coordinator per building → cloud analytics + central controller → cross-campus applications. Mention all 7 IoT-WF layers.

---

## 1.8 IoT Communication Protocols

### 1.8.1 Protocol Stack (mapped to OSI layers)

| Layer | Protocols / Standards |
|-------|-----------------------|
| Application | **MQTT, CoAP, HTTP, DDS, XMPP, AMQP** |
| Presentation | TLS/SSL, CBOR, JSON, XML |
| Session | MQTT-Sessions, CoAP-Observe, WebSocket |
| Transport | TCP, UDP, QUIC |
| Network | IPv4, **IPv6, 6LoWPAN** |
| Data Link | IEEE 802.15.4, Wi-Fi (802.11), Ethernet (802.3), BLE, LoRa |
| Physical | Sub-GHz ISM, 2.4 GHz, light, electrical |

### 1.8.2 Common Application-Layer Protocols — Comparison Table

| Protocol | Transport | Model | Header Size | Best Use |
|----------|-----------|-------|--------------|----------|
| **MQTT** | TCP | Pub/Sub | 2 bytes | Smart home, telemetry |
| **CoAP** | UDP | Request/Response (RESTful) | 4 bytes | Constrained sensor nodes |
| **HTTP** | TCP | Request/Response | Large | Universal web, REST APIs |
| **AMQP** | TCP | Pub/Sub with transactions | Medium | Industrial, financial |
| **DDS** | UDP/TCP/shm | Pub/Data-Centric | Medium | Real-time industrial, defence |
| **XMPP** | TCP | XML presence + Pub/Sub | Heavy | Chat, presence |

### 1.8.3 Communication Models (the 4 patterns)

1. **Request-Response** — Client → Server → Client (HTTP, CoAP).
2. **Publish-Subscribe** — Publisher → Broker → Subscriber(s) (MQTT, AMQP).
3. **Push-Pull** — Producers push to queues, consumers pull (Kafka, RabbitMQ).
4. **Exclusive Pair** — Persistent bi-directional full-duplex (WebSocket).

### 1.8.4 6LoWPAN

**IPv6 over Low-Power Wireless Personal Area Networks.** Enables IPv6 on tiny 802.15.4 devices by:
- **Header compression** — squashes 40-byte IPv6 + 8-byte UDP into ~7 bytes.
- **Fragmentation** — supports 127-byte 802.15.4 MTU.
- **Mesh forwarding** below IP layer.

Crucial because every IoT device gets an IP address — enabling end-to-end IPv6 reachability and billions of uniquely-addressed things.

### 1.8.5 REST and WebSocket APIs

- **REST** (Representational State Transfer) — constraints: uniform interface, statelessness, cacheability, layered system, code-on-demand. Uses HTTP verbs **GET, POST, PUT, DELETE**. Maps to **Request-Response** model.
- **WebSocket** — bi-directional, full-duplex, persistent connection. Maps to **Exclusive Pair** model. Ideal for real-time dashboards.

---

## 1.9 SPI and I²C Protocols (2024 Q3 — 10 Marks)

Both are **on-board serial communication protocols** between ICs (chip-to-chip, <1 m). Both are well-suited for slow communication with on-board peripherals.

| Property | SPI | I²C |
|----------|-----|------|
| **Inventor (year)** | Motorola (1979) | Philips (1982) |
| **Lines** | 4 (SCLK, MOSI, MISO, SS) | 2 (SDA, SCL) |
| **Topology** | Single master, multi-slave | Multi-master, multi-slave |
| **Slave addressing** | Hardware SS pin per slave | 7-bit software address |
| **Speed** | Up to tens of Mbps | 100 kbps std / 400 kbps fast / 3.4 Mbps high |
| **Duplex** | Full-duplex (separate MISO/MOSI) | Half-duplex (shared SDA) |
| **ACK mechanism** | No hardware ACK | Hardware ACK after each byte |
| **Wires needed for N slaves** | 3 + N (one SS per slave) | 2 (always) |

### 1.9.1 SPI — Serial Peripheral Interface

**4 signal lines:**
1. **SCLK** — clock from master to all slaves; all signals are synchronous to this clock.
2. **MOSI** (Master Out-Slave In) — master → slave data.
3. **MISO** (Master In-Slave Out) — slave → master data.
4. **SSn** — one Slave-Select line per slave (active LOW).

**Working (write the steps in the answer):**
1. SPI is a **single-master protocol** — one device initiates all communication.
2. Master pulls the **SS** line of the desired slave **LOW**.
3. Master activates **SCLK** at a frequency both ends support.
4. On each clock edge, master toggles **MOSI** (data out) and samples **MISO** (data in) — full-duplex simultaneous read/write.
5. Data bits toggle on **SCLK falling edge**, sampled on **SCLK rising edge** (SPI Mode 0). Other SPI modes flip which edge does what.
6. After all bytes exchanged, master raises **SS** HIGH to release the slave.

**Diagram (single slave):**
```
                 SCLK ─────────────────────────────►
   MASTER        MOSI ─────────────────────────────►     SLAVE
                 MISO ◄─────────────────────────────
                  SS  ──────────────[ LOW ]────────►
```

**Diagram (multi-slave):**
```
                  SCLK ────────────────► ────► ────►
                  MOSI ────────────────► ────► ────►
                  MISO ◄──────────────── ◄──── ◄────
   MASTER           SS0 ───[ LOW ]─────►
                    SS1 ─────────────[ LOW ]──►
                    SS2 ───────────────────────[ LOW ]──►
                                              S0   S1   S2
```

### 1.9.2 I²C — Inter-Integrated Circuit

**2 signal lines:**
1. **SDA** — Serial Data (bidirectional).
2. **SCL** — Serial Clock (master drives).

Both lines are **open-drain** — pulled HIGH by external pull-up resistors (typically 4.7 kΩ); any device can drive them LOW. This allows multi-master bus.

**Working (write the steps):**
1. **START condition** — master pulls SDA LOW while SCL is HIGH → "attention" signal. All slaves listen.
2. Master sends **7-bit slave address** + **1-bit R/W** (0 = write, 1 = read).
3. Every slave compares the address with its own. The matching slave responds with **ACK** (pulls SDA LOW for one clock period).
4. Master and slave exchange **8-bit data bytes**, each followed by an **ACK** bit from the receiver.
5. **STOP condition** — master releases SDA to HIGH while SCL is HIGH → bus is free for next transfer.

**Diagram:**
```
                SDA: ──┐  ┌─Addr7─┬R/W┬─ACK─┬─Data0─┬─ACK─┬─...┬─STOP─┐──
                      │  │       │   │     │       │     │    │      │
   Idle ◄──START──────┘  └───────┘   └─────┘───────┘─────┘    └──────┘►Idle
                SCL: ──┐  ┌─┐ ┌─┐ ┌─┐ ┌─┐ ┌─┐ ┌─┐ ┌─┐ ┌─┐ ... ┌─┐ ┌─┐──
                      └──┘ └─┘ └─┘ └─┘ └─┘ └─┘ └─┘ └─┘ └─┘     └─┘ └─┘
                       START            ACK         ACK        STOP
```

**Speeds:** Standard 100 kbps | Fast 400 kbps | High-Speed 3.4 Mbps.

**I²C advantages over SPI:** Fewer wires (2 vs 4+N), hardware ACK, multi-master support, simpler PCB routing.  
**SPI advantages over I²C:** Higher speed, full-duplex, lower protocol overhead, simpler slave hardware.

---

## 1.10 Access Technologies (Bluetooth, Zigbee, NFC, NB-IoT, Sigfox, LoRa)

This is the **most-likely 5-10 marks question**. The 2024 PYQ asks you to write **short notes on any TWO** of {Bluetooth, Zigbee, NB-IoT, Sigfox, NFC}. The 2025 PYQ asks you to **illustrate working principle + network architecture + packet structure + key specs** for any one mid-range technology.

**Classification by range:**
- **Short-range (≤10 cm):** NFC.
- **Personal-area (10–100 m):** Bluetooth, BLE, Zigbee.
- **Local-area (50–200 m):** Wi-Fi.
- **Wide-area (1–15 km):** LoRa, Sigfox, NB-IoT, LTE-M.

### 1.10.1 Bluetooth (IEEE 802.15.1)

- **Frequency band:** 2.4 GHz ISM, 79 channels of 1 MHz each.
- **Modulation:** GFSK (Basic Rate), π/4-DQPSK & 8-DPSK (EDR).
- **Data rate:** 1 Mbps (BR), 2–3 Mbps (EDR), ≤24 Mbps (HS), 1–2 Mbps (BLE 5).
- **Range:** Class 3 = 1 m, Class 2 = 10 m, Class 1 = 100 m.
- **Topology:** Piconet (1 master + up to 7 active slaves), Scatternet (multiple piconets linked).
- **Packet format:** 72-bit access code + 54-bit header + payload (0–2744 bits). Header has 3-bit active member address (AMA), 4-bit type code, 3-bit flow control, 1-bit sequence, 1-bit ACK, 1-bit header-error-check, 8-bit CRC.
- **States:** STANDBY → INQUIRY (discover) → PAGE (connect) → CONNECTED (active/park/hold/sniff).
- **Frequency Hopping:** 1600 hops/sec, time-division duplex (TX/RX alternate slots of 625 µs).
- **Protocol stack:** Baseband, LMP, L2CAP, RFCOMM, SDP, HCI, app profiles (SPP, A2DP, HFP, etc.).
- **Energy management:** Sniff (low duty cycle), Hold (no ACL traffic), Park (slave releases AMA, gets PM_ADDR).
- **Use case:** Wearables, audio, BLE beacons, fitness trackers.

### 1.10.2 Zigbee (IEEE 802.15.4) — IMPORTANT (asked 2024)

- **Frequency band:** 2.4 GHz (global), 868 MHz (EU), 915 MHz (US).
- **Modulation:** O-QPSK (offset quadrature phase-shift keying) DSSS.
- **Data rate:** 250 kbps (2.4 GHz), 20 kbps (868 MHz), 40 kbps (915 MHz).
- **Range:** 10–100 m indoor (extendable via mesh).
- **Network size:** Up to 65 535 nodes (16-bit short address).
- **Topology:** Star, Tree, **Mesh** (most popular — self-healing).
- **Device roles:** **Coordinator** (forms network, one per network), **Router** (forwards packets, mains-powered), **End Device** (battery, sleeps, talks only to parent).
- **Layers:** PHY (modulation, TX/RX), MAC (channel access — CSMA/CA), NWK (routing, addressing, security), APS (network↔app bridge), Application Framework.
- **Security:** 128-bit AES encryption.
- **Power:** End devices can run years on a coin cell thanks to sleep modes.
- **Pros:** Low-cost, scalable, self-healing mesh, secure.
- **Cons:** Low data rate (no video), limited range without enough routers, 2.4 GHz interference with Wi-Fi/BT, mesh multi-hop latency.
- **Applications:** Smart home (lights, thermostats), industrial IoT monitoring, smart energy metering, healthcare patient tracking, smart agriculture.

**Why named "Zigbee"?** Inspired by honeybees' **zigzag waggle dance** they use to communicate the location of food sources. "Zig" = zigzag dance, "Bee" = cooperative community — like a resilient self-healing mesh.

### 1.10.3 NFC (Near Field Communication) — IMPORTANT (asked 2024 & 2025)

- **Frequency:** 13.56 MHz.
- **Range:** ≤4 cm (≤10 cm in some specs).
- **Data rate:** 106, 212, or **424 kbps**.
- **Modulation:** ASK (amplitude shift keying).
- **Origin:** Built on RFID. First RFID patent filed by Charles Walton (1983); NFC itself developed by **Sony + NXP** (2002); **NFC Forum** founded by Nokia, Philips, Sony (2004).
- **vs RFID:** NFC is two-way (peer-to-peer), RFID is one-way; NFC is short-range → more privacy/security.
- **vs Bluetooth:** NFC much shorter range and slower, but pairs in 0.1 s vs 6 s for Bluetooth — used for **easy pairing**.

**Working Principle (must include in answer):**
1. One device has an **NFC reader/writer** (active, powered); the other has an **NFC tag** (passive, unpowered).
2. Reader passes an AC current through a coil → generates an **alternating magnetic field** in its near vicinity.
3. Bringing the tag's coil into this field causes **inductive coupling** (transformer-like).
4. The tag harvests energy from the field to power its IC and replies via **load modulation** — by changing its own impedance, the tag changes the amplitude of the reader's field. The reader demodulates this amplitude change.

**Three Modes of Operation:**
1. **Reader/Writer Mode** — Read/write passive NFC tags/stickers. Example: tapping a smart poster to open a URL.
2. **Peer-to-Peer (P2P) Mode** — Two NFC devices exchange data. Example: Android Beam.
3. **Card Emulation Mode** — NFC device acts as a contactless smart card. Example: **Apple Pay / Google Pay** at a POS terminal.

**Protocol Stack (3 layers):**
- **L1 RF / Physical Layer** — 13.56 MHz, modulation, signal interface (ISO/IEC 18092).
- **L2 Logical Link Control (LLCP)** — connection management, error detection, flow control.
- **L3 Application Layer** — **NDEF (NFC Data Exchange Format)** records: vCard, URL, text, smart-poster.

**Role in IoT:** Tap-to-pair IoT devices; short-range secure authentication; passive tags can be powered by the reader → zero-power data exchange.

### 1.10.4 NB-IoT (Narrowband IoT) — for short note

- **3GPP Release 13 (2016).**
- **Licensed cellular spectrum** — operates in 200 kHz bandwidth inside LTE bands.
- **Modulation:** OFDMA downlink, SC-FDMA uplink.
- **Data rate:** ~200 kbps downlink, ~250 kbps uplink (multi-tone), ~20 kbps single-tone.
- **Range:** 10+ km (rural), 1 km (urban).
- **Battery life:** 10+ years on AA cells (thanks to PSM, eDRX).
- **Use case:** Smart metering, asset tracking, smart parking — small periodic uplink data.

### 1.10.5 Sigfox — for short note

- **Unlicensed ISM bands** (868 MHz EU / 902 MHz US).
- **Ultra-narrowband** (100 Hz per message).
- **Data rate:** 100 bps uplink, 600 bps downlink.
- **Payload:** 12 bytes uplink, 8 bytes downlink; max 140 messages/day.
- **Range:** 10 km urban, 40 km rural.
- **Topology:** Star-of-stars — devices → Sigfox base stations → Sigfox Cloud → customer app.
- **Use case:** Asset tracking, simple presence sensors, basic metering — where bytes-per-day is enough.

### 1.10.6 LoRa & LoRaWAN — bonus for completeness

- **Physical layer:** Chirp Spread Spectrum (CSS) on Sub-GHz ISM (868/915 MHz).
- **Data rate:** 0.3–50 kbps.
- **Range:** 15+ km rural, 2–5 km urban.
- **Network architecture:** End-devices → Gateway → Network Server → Application Server.
- **Three classes:** Class A (lowest power, uplink-triggered), Class B (scheduled beacons), Class C (always-on).
- **Use case:** Smart agriculture, smart city (parking, lighting), long-range leak sensors.

### 1.10.7 Comparison Cheat-Sheet

| Tech | Freq | Range | Rate | Topology | Power |
|------|------|-------|------|----------|-------|
| Bluetooth (BR) | 2.4 GHz | 10–100 m | 1–3 Mbps | Piconet/Scatternet | Medium |
| BLE | 2.4 GHz | 10–50 m | 1–2 Mbps | Star | Low |
| Zigbee | 2.4 GHz | 10–100 m | 250 kbps | Star/Tree/Mesh | Ultra-low |
| Wi-Fi | 2.4/5 GHz | 50–100 m | 100+ Mbps | Star | High |
| NFC | 13.56 MHz | <10 cm | 424 kbps | P2P | Passive / very low |
| LoRa | Sub-GHz | 15+ km | 0.3–50 kbps | Star-of-stars | Low |
| Sigfox | Sub-GHz | 10–40 km | 100 bps | Star-of-stars | Ultra-low |
| NB-IoT | LTE band | 10+ km | 200 kbps | Cellular | Ultra-low |

---

## 1.11 Resource Management in IoT

### 1.11.1 Why It Matters

Most IoT devices have **limited**:
- Battery / Power
- Processing power (CPU cycles)
- Memory (RAM/Storage)
- Network bandwidth

Goal: deliver the required QoS while maximising battery lifetime and respecting these constraints.

### 1.11.2 Key Techniques

1. **Energy-Aware Allocation** — schedule tasks based on remaining battery; defer non-critical ones.
2. **Edge Computing** — process locally → less radio usage → big power savings (radio is the largest energy consumer).
3. **AI/ML-Based Management** — predict workload, optimise duty cycle.
4. **Duty Cycling** — sleep between active windows; e.g. weather sensor wakes every 30 min → battery lasts years.
5. **TDMA Bandwidth Allocation** — assign fixed slots to nodes → no contention overhead.
6. **Offload vs Local Decision** — when is it cheaper (energy & latency) to send data to the edge for processing vs compute locally? See Numerical §3.3.

### 1.11.3 Three Resource-Management Worked Examples (from the slides)

#### TDMA Bandwidth & Time Allocation
3 sensors share TDMA uplink (T_frame = 100 ms, B = 1 MHz). Payloads: S1 = 100 kbits @ 10 dB SNR, S2 = 200 kbits @ 5 dB, S3 = 150 kbits @ 20 dB. Is frame feasible? If not, find (a) min bandwidth, (b) max payloads at 1 MHz in 100 ms.

**Solution outline:**
- Convert SNR dB → linear: 10 dB → 10, 5 dB → 3.162, 20 dB → 100.
- Shannon rate per sensor: R = B·log₂(1 + SNR).
  - R1 = 1 MHz × log₂(11) = 3.459 Mbps
  - R2 = 1 MHz × log₂(4.162) = 2.057 Mbps
  - R3 = 1 MHz × log₂(101) = 6.658 Mbps
- Times: t1 = 100 kbits / 3.459 Mbps = 28.91 ms; t2 = 200 / 2.057 = 97.21 ms; t3 = 150 / 6.658 = 22.53 ms. Total = 148.65 ms > 100 ms → **infeasible**.
- (a) B_min = 1 MHz × (148.65/100) = **1.486 MHz**.
- (b) Scale payloads by α = 100/148.65 = 0.6727:
  - D1' = 67.27 kbits, D2' = 134.55 kbits, D3' = 100.91 kbits.

#### Duty Cycling & Lifetime
Battery 3 V, 2000 mAh. Active: 20 mA for 0.5 s/min (sensing + 100 ms Tx). Sleep: 50 µA otherwise. Lifetime?

- I_avg = (20 mA × 0.5 s + 50 µA × 59.5 s) / 60 s = (10 + 2.975)/60 = 0.216 mA.
- Lifetime = 2000 mAh / 0.216 mA = **9248 h ≈ 385 days ≈ 12.7 months**.

#### Offload vs Local
Local: 2×10⁸ cycles/s @ 200 MHz CPU, energy/cycle 10⁻¹⁰ J. Offload: upload D = 500 kb at B = 1 MHz, SNR = 10 dB, TX power = 100 mW. Compare latency & energy per job.

- Local: t = 2×10⁸/200 MHz = **1.0 s**; E = 2×10⁸ × 10⁻¹⁰ = **0.02 J**.
- Offload: t↑ = 500 kb / 3.459 Mbps = **0.1445 s**; E↑ = P·t↑ = 0.1 W × 0.1445 = **0.01445 J**.
- **Conclusion:** Offloading is better in both latency and energy.

---

# UNIT 2 — TECHNOLOGY FOR IoT

## 2.1 Programming for IoT

### 2.1.1 Why Multiple Languages?

IoT devices have wildly different capabilities — from 1 KB RAM microcontrollers to 8 GB single-board computers running full Linux. No single language fits all.

| Layer | Languages | Examples |
|-------|-----------|----------|
| Application Logic | Python, JavaScript, Node.js | Business rules, UI, data processing |
| Device Firmware | C, C++, Rust, MicroPython | Hardware control, sensors, actuators |
| Cloud/Gateway | Python, JavaScript, Go | Data aggregation, analytics, REST/GraphQL APIs |

### 2.1.2 Language Selection Guide

| Resource Tier | RAM | Languages | Example Boards |
|---------------|-----|-----------|----------------|
| Constrained | KB | C / C++ / MicroPython | Arduino Uno, ESP8266, small sensors |
| Balanced | MB + radio | C++ / MicroPython | ESP32, Raspberry Pi Pico |
| Powerful | GB + OS | Python / JavaScript | Raspberry Pi, gateways, cloud |

2026 trends: Rust gaining for safety-critical IoT; MicroPython adoption rising; C/C++ remain dominant in industry.

### 2.1.3 Bare-Minimum Arduino Code Skeleton (must know)

```cpp
// 1. DIRECTIVES — handled before compilation
#include <Library.h>      // bring in a library
#define LED_PIN 2          // named constant — no semicolon

// 2. setup() — runs ONCE on boot/reset
void setup() {
    pinMode(LED_PIN, OUTPUT);
    Serial.begin(115200);
}

// 3. loop() — runs FOREVER after setup()
void loop() {
    digitalWrite(LED_PIN, HIGH);
    delay(1000);            // WARNING: delay() blocks the whole MCU!
    digitalWrite(LED_PIN, LOW);
    delay(1000);
}
```

### 2.1.4 ESP32 Function Toolkit (must memorise)

| Function | Purpose | Pin mode needed |
|----------|---------|-----------------|
| `pinMode(pin, mode)` | Configure pin as INPUT / OUTPUT | (call in setup) |
| `digitalWrite(pin, val)` | Set pin HIGH (3.3 V) or LOW (0 V) | OUTPUT |
| `digitalRead(pin)` | Read HIGH/LOW | INPUT or INPUT_PULLUP |
| `analogRead(pin)` | Read ADC value 0–4095 (12-bit) | ADC-capable pin |
| `analogWrite(pin, val)` | PWM output 0–255 | PWM-capable pin |
| `delay(ms)` | Blocking delay in ms | — |
| `Serial.begin(baud)` | Start UART for serial monitor | — |
| `Serial.print(val)` / `Serial.println(val)` | Print to serial monitor | — |

### 2.1.5 ESP32 GPIO Quick Notes

- Logic level **3.3 V — NOT 5 V tolerant**.
- **GPIO 6–11** reserved for internal flash — never use.
- **GPIO 34–39** input-only (no internal pull-ups).
- Internal pull-up resistors can be enabled in software (`INPUT_PULLUP`).
- ADC: **12-bit** → values 0–4095 over 0–3.3 V.  
  `Voltage = (ADC Value / 4095) × 3.3`

### 2.1.6 Functions vs Macros (#define)

| # | Macro `#define SQ(x) ((x)*(x))` | Function `int sq(int x){return x*x;}` |
|---|--------------------------------|----------------------------------------|
| Replaced by | Preprocessor (text substitution) | Compiled as real code |
| Type checking | None — bug-prone | Yes |
| Debuggable | No (never "exists" at runtime) | Yes (breakpoints, step-through) |
| Use when | Trivial one-line swap | Anything beyond one line |

### 2.1.7 MicroPython — Blink

```python
from machine import Pin
import time

led = Pin(2, Pin.OUT)
while True:
    led.value(1)        # HIGH
    time.sleep(1)
    led.value(0)        # LOW
    time.sleep(1)
```

**Advantages:** no compile step, REPL for live testing, beginner-friendly syntax.  
**Disadvantages:** slower than compiled C, larger RAM footprint, not ideal for tight timing.

---

## 2.2 IoT Frameworks

### 2.2.1 What is an IoT Framework?

> **An IoT framework is a software/hardware structure that serves as a foundation for the development, deployment, and management of IoT systems. It provides standard protocols, libraries, and tools to integrate different IoT components.**

**Purpose / Importance:**
- **Simplify development** with reusable components.
- **Interoperability** between devices and systems.
- **Security** via standard protocols.
- **Scalability & flexibility** in deployments.
- **Manage and analyse** large volumes of data.

**Key components of any IoT framework:**
1. Devices & sensors
2. Connectivity (Wi-Fi, BLE, Zigbee, LTE, 5G)
3. Data processing (edge + cloud)
4. User interface (mobile apps, web dashboards, voice assistants)
5. Security (encryption, authentication, secure boot)

### 2.2.2 Cloud-Based vs Open-Source

| Aspect | Cloud-Based (PaaS) | Open-Source (Self-Hosted) |
|--------|---------------------|---------------------------|
| Hosting | Provider-managed | Self-managed |
| Maintenance | Minimal; auto updates & scaling | Full responsibility |
| Scalability | Automatic | Manual planning |
| Cost | Pay-as-you-go | Free software + hosting cost |
| Vendor lock-in | High | Low |
| Customization | Limited | Extensive |
| Best for | Rapid enterprise deployment | Custom needs, compliance |

### 2.2.3 Major Cloud IoT Frameworks

#### AWS IoT Core
- **What:** Managed cloud service by Amazon; secure device↔cloud connectivity; supports device-to-cloud and cloud-to-device messaging.
- **Protocols:** MQTT, MQTT over WebSocket, HTTPS.
- **Devices supported:** ESP32, Raspberry Pi, industrial controllers, smart meters, sensors, actuators, connected vehicles.

**Key features:**

| Feature | What it does |
|---------|--------------|
| Device Gateway | Secure two-way device–cloud communication |
| Message Broker | Pub/Sub model |
| Rules Engine | Filters & routes device data to AWS services (e.g. Lambda) |
| Device Registry | Stores device identity, metadata, configuration |
| Device Shadow | Cloud-side representation of device state (desired + reported) |
| Security | X.509 certs + TLS + IAM policies |
| Greengrass | Local processing, ML inference, cloud sync |
| OTA Updates | Secure over-the-air firmware updates |

**Architecture flow:**
```
[Sensor] ─► [ESP32] ─MQTT/HTTPS─► [AWS IoT Core]
                                     │
                                     ├─ Device Gateway (entry point)
                                     ├─ Message Broker (pub/sub)
                                     ├─ Rules Engine ──► Lambda / DynamoDB / S3
                                     ├─ Device Shadow (state sync)
                                     └─ Device Registry (identity)
```

#### Azure IoT Hub
- Microsoft's equivalent. Protocols: MQTT, AMQP, HTTPS.
- **Device Twins** (≈ AWS Device Shadow), **Direct Methods** (remote RPC), **File Upload** to Azure Storage, **Device Provisioning Service** (securely onboard at scale).
- **Security:** SAS tokens + X.509 + TPM-based auth.
- **Edge computing:** Azure IoT Edge — local AI, analytics, custom modules.
- Integrates with Power BI, Azure ML, etc.

#### Other Cloud Frameworks (1-line each)
- **Google Cloud IoT** — fully managed, global device ingestion. Use: environmental monitoring, supply chain.
- **IBM Watson IoT** — advanced analytics + AI. Use: automotive, manufacturing.
- **Cisco IoT** — networking + security. Use: industrial automation, energy.

### 2.2.4 Open-Source IoT Frameworks

| Framework | Type | Best Suited For |
|-----------|------|-----------------|
| **ThingsBoard** | Device mgmt + visualization | Custom IoT solutions needing rich dashboards |
| **Kaa IoT** | Enterprise platform | Industrial, complex device fleets |
| **ESP RainMaker** | Cloud for ESP devices | ESP32 / ESP32-S / ESP32-C products |
| **Home Assistant** | Smart-home automation | Home automation enthusiasts |
| **Eclipse IoT** | Collection of frameworks | Standardized modular IoT |
| MACCHINA.io | — | Edge gateways |
| ZETTA | — | Data flow pipelines |
| GE PREDIX | — | Industrial IoT |
| **ThingSpeak** | IoT analytics PaaS | Aggregating/visualizing live data |
| DeviceHive | — | M2M/IoT backend |
| OpenHAB | — | Smart home automation |

### 2.2.5 AWS IoT vs Azure IoT (Comparison Table)

| Feature | AWS IoT Core | Azure IoT Hub |
|---------|--------------|---------------|
| Protocols | MQTT, HTTPS, WebSocket | MQTT, AMQP, HTTPS |
| Device Management | Device Shadows | Device Twins |
| Data Processing | Rules Engine → AWS services | Time Series / Azure services |
| Security | IAM + X.509 | SAS tokens + X.509 |
| ML/AI | SageMaker + Greengrass | Azure ML + IoT Edge |
| Edge Computing | AWS Greengrass | Azure IoT Edge |
| Scalability | Billions of devices | Elastic scaling |

---

## 2.3 Virtualization Concepts in IoT

### 2.3.1 Definition

> **IoT virtualization** refers to the **abstraction of physical devices and resources into virtual representations**, allowing multiple virtual devices to run on a single physical device — enabling management, optimization, and scaling of IoT systems.

### 2.3.2 Benefits (5 points)

1. **Resource Optimization** — efficient use of physical devices (share one gateway among many "virtual sensors").
2. **Scalability** — easily scale IoT systems as needed.
3. **Security** — isolate and protect virtual devices.
4. **Flexibility** — quickly deploy and configure virtual devices.
5. **Cost-Efficiency** — reduce hardware & maintenance costs.

### 2.3.3 Virtual Sensors & Actuators

Software-based entities that **emulate the behavior** of physical sensors and actuators. Used to simulate sensor data or control actions in virtual environments for testing, development, or scalability.

### 2.3.4 Use Cases of IoT Virtualization

- **Smart Cities** — virtualization of city-wide sensor networks.
- **Industrial IoT** — virtual production lines and machines.
- **Healthcare** — virtual monitoring of patient data.
- **Home Automation** — virtual devices for managing smart homes.
- **Testing & Development** — virtual environments for IoT application development.

### 2.3.5 Challenges (must mention)

1. **Performance Overhead** — potential latency & resource bottlenecks.
2. **Security Risks** — increased attack surface in virtual environments.
3. **Interoperability** — compatibility issues between virtual and physical devices.
4. **Complexity** — managing & configuring virtual devices is complex.
5. **Reliability** — ensuring reliability of virtual devices & systems.

### 2.3.6 Virtualization vs Containerization (QB Q18)

| Aspect | Virtualization | Containerization |
|--------|----------------|------------------|
| Isolation unit | VM (full guest OS) | Container (shared host kernel) |
| Boot time | Minutes | Seconds |
| Resource overhead | High (OS per VM) | Low |
| Use case | Strong isolation, multi-OS | Microservices, IoT edge apps |

---

## 2.4 Embedded Platforms for IoT

### 2.4.1 What is an Embedded Platform?

> **A combination of hardware and software designed for a specific function.**  
> Hardware: MCU/MPU, memory, I/O, peripherals, radios.  
> Software: bare metal, RTOS, or Linux.  
> In IoT, it converts raw signals into useful data and actions.  
> Examples: **STM32, ESP32, BeagleBone, Raspberry Pi**.

**IoT system stack:** Things/Sensors → Edge/Gateway → Cloud → Applications.  
**Embedded platform sits at the edge** — it is the "brain" of the IoT device.  
**Core edge functions:** **Sense → Compute → Connect → Act.**

### 2.4.2 MCU vs MPU vs SBC

| | **MCU** (Microcontroller Unit) | **MPU** (Microprocessor Unit) | **SBC** (Single Board Computer) |
|--|---|---|---|
| Integration | CPU + memory + peripherals on one chip | CPU only; needs external memory & peripherals | Complete computer on one board |
| OS | Bare-metal or RTOS | Full OS like Linux | Linux, rich I/O, networking, display |
| Power | Low | Higher | Highest |
| Cost | Low | Medium | Higher |
| Examples | STM32, ESP32 | Cortex-A chips | BeagleBone, Raspberry Pi |

### 2.4.3 Hardware Building Blocks

- **CPU core** — ARM Cortex-M (MCU) or Cortex-A (Linux SBC).
- **Memory** — Flash/SRAM on MCU; DDR + eMMC/SD on SBC.
- **I/O & peripherals** — GPIO, UART, I2C, SPI, ADC, PWM, CAN.
- **Connectivity** — Wi-Fi, BLE, Ethernet, LoRa, cellular.
- **Power subsystem** — battery, regulator, sleep modes.
- **Expansion** — headers, capes, HATs, shields.

### 2.4.4 Microcontroller Platforms

**STM32 (STMicroelectronics)**
- ARM Cortex-M cores (M0 to M7).
- Bare metal or RTOS (FreeRTOS, Zephyr).
- Excellent real-time, low power, rich analog & timers.
- Ideal for: motor control, industrial sensors, precise I/O.
- Connectivity: usually external (LoRa, BLE, Ethernet).

**ESP32 (Espressif)**
- Dual-core Xtensa / RISC-V, up to 240 MHz.
- Integrated Wi-Fi + Bluetooth/BLE.
- FreeRTOS, ESP-IDF, Arduino support.
- Ideal for: connected sensor nodes, small gateways, wearables.
- Low cost, good compute for an MCU.

### 2.4.5 Linux SBC Platforms

**BeagleBone (Black / AI)**
- ARM Cortex-A + PRU (Programmable Real-time Unit) co-processors.
- Runs Linux (Debian).
- Extensive I/O, capes for industrial expansion.
- Ideal for: industrial gateways, real-time Linux control, robotics.
- Strong maker + industrial community.

**Raspberry Pi (4 / 5 / Zero)**
- ARM Cortex-A, up to 8 GB RAM.
- Runs Linux (Raspberry Pi OS, Ubuntu).
- Rich compute, USB, HDMI, camera, networking.
- Ideal for: edge gateways, vision, dashboards, prototyping.
- Huge ecosystem, but **not hard real-time**.

### 2.4.6 Platform Comparison (memorize this table)

| Feature | STM32 | ESP32 | BeagleBone | Raspberry Pi |
|---------|-------|-------|------------|--------------|
| Class | MCU | MCU + radio | Linux SBC | Linux SBC |
| OS | Bare metal / RTOS | FreeRTOS | Linux + PRU | Linux |
| CPU | Cortex-M | Xtensa / RISC-V | Cortex-A + PRU | Cortex-A |
| Connectivity | External | Wi-Fi + BLE | Ethernet, Wi-Fi | Ethernet, Wi-Fi, BT |
| Real-time | Excellent | Good | Good (PRU) | Limited |
| Power | Very low | Low | Medium | High |
| Compute | Low | Medium | Medium-High | High |
| Best for | Control, sensors | Connected nodes | Industrial edge | Gateways, vision |

### 2.4.7 Selection Criteria

- **Power** — battery life, sleep modes, energy harvesting. STM32/ESP32 win; SBCs need mains.
- **Real-time** — deterministic response, jitter, latency. STM32 best; BeagleBone PRU good; RPi limited.
- **Compute & Memory** — data processing, vision, analytics, multi-tasking. RPi best; ESP32 moderate; STM32 limited.
- **Connectivity** — Wi-Fi, BLE, LoRa, cellular, Ethernet. ESP32 has integrated; SBCs have Ethernet/Wi-Fi; STM32 often external.
- **Cost** — unit cost, development cost, ecosystem cost.
- **Security** — secure boot, crypto, secure storage, OTA updates.
- **Ecosystem** — tools, libraries, community, industrial support.

### 2.4.8 Decision Framework — Use Case → Platform

| Use Case | Recommended Platform | Why |
|----------|---------------------|-----|
| Battery soil sensor, long range | ESP32 + LoRa or STM32 + LoRa | Low power, external radio |
| Motor control, µs timing | STM32 | Deterministic real-time |
| Smart home gateway, MQTT, dashboard | Raspberry Pi | Linux, networking, compute |
| Industrial machine control, Linux + precise I/O | BeagleBone | PRU for real-time, capes |
| Vision-based edge node | Raspberry Pi | GPU, camera, compute |
| Cheap BLE wearable | ESP32 or STM32 + BLE | Low power, small, connected |

---

## 2.5 RTOS & FreeRTOS

### 2.5.1 What is an RTOS?

> **An RTOS is an operating system designed to process inputs and produce a response within a guaranteed, bounded time — a deadline.**

> **Key idea:** *Correctness depends on time.* A late answer is a wrong answer — not just a slow one. This is what separates an RTOS from a general-purpose OS optimized for average throughput.

**Hard vs Soft Real-Time:**
- **Hard real-time** — missing a deadline = system failure. Examples: airbag deployment, ABS, pacemaker.
- **Soft real-time** — missing a deadline degrades quality, system survives. Examples: video streaming, IoT sensor sending a reading a little late.
- **Most IoT nodes are soft real-time** — this is the class FreeRTOS targets.

### 2.5.2 RTOS vs General-Purpose OS

| Aspect | RTOS (FreeRTOS) | General-Purpose OS |
|--------|-----------------|---------------------|
| Scheduling goal | Meet deadlines — determinism | Maximize average throughput / fairness |
| Scheduler | Priority-based, preemptive, predictable | Time-sliced, best-effort, variable latency |
| Memory footprint | Few KB – hundreds of KB RAM | Tens to hundreds of MB RAM |
| Boot time | Milliseconds | Seconds to tens of seconds |
| Typical hardware | Microcontrollers (ESP32, AVR, Cortex-M) | SoCs / SBCs (Raspberry Pi, PC) |
| Examples | FreeRTOS, Zephyr, RIOT, VxWorks | Linux, Windows, Android |

### 2.5.3 Why Constrained IoT Devices Need an RTOS

1. **Determinism** — sensor sampling, control loops, radio timing (BLE/Zigbee slots) need *predictable* response, not just fast.
2. **Tiny footprint** — runs in a few KB of RAM/flash; fits microcontrollers that could never boot Linux.
3. **Concurrency without complexity** — one MCU juggling sensing, processing, networking as independent tasks instead of one tangled loop.
4. **Power efficiency** — built-in idle / tickless modes sleep the CPU between events — critical for battery-powered motes.

### 2.5.4 RTOS Options Landscape

| RTOS | Notes |
|------|-------|
| **FreeRTOS** | Free, open-source (MIT), tiny kernel, de facto on ESP32/STM32/AVR. AWS-backed. |
| **Zephyr** | Linux-Foundation, broad hardware abstraction, built-in networking. |
| **RIOT OS** | Academic roots, strong 6LoWPAN & CoAP for constrained mesh nodes. |
| **Mbed OS** | ARM's RTOS for Cortex-M, large driver/library ecosystem. |
| **VxWorks** | Commercial, safety-certified. Aerospace, industrial, automotive. |

### 2.5.5 Why FreeRTOS Is Preferred

- **Free & open source (MIT)** — no licensing cost; source is auditable.
- **Minimal footprint** — kernel fits in ~6–12 KB of flash.
- **Broad MCU support** — 40+ architectures: ESP32, ARM Cortex-M, AVR, PIC, RISC-V.
- **Industry backing** — maintained by AWS; integrates directly with AWS IoT Core.
- **Mature ecosystem** — native to ESP-IDF; huge community, documentation, examples.

### 2.5.6 FreeRTOS Architecture

```
   ┌─────────────────────────────────────┐
   │           Application Tasks         │  ← Sensing · Processing · Networking · UI
   ├─────────────────────────────────────┤
   │           FreeRTOS Kernel           │  ← Scheduler · Task Control Blocks
   │                                     │    · Queues · Semaphores/Mutexes
   │                                     │    · Software Timers
   ├─────────────────────────────────────┤
   │  Hardware Abstraction / Port Layer   │  ← Tick timer ISR · Context switch
   │                                     │    · Interrupt handling
   ├─────────────────────────────────────┤
   │           MCU Hardware              │  ← e.g. ESP32 (Xtensa LX6 dual-core)
   └─────────────────────────────────────┘
```

### 2.5.7 Tasks and Task States

A **task** is an independent thread of execution with its own stack and priority — the basic unit of concurrency in FreeRTOS.

**Four task states:**
1. **Ready** — capable of running but a higher-/equal-priority task is using the CPU.
2. **Running** — currently executing on the CPU. Only one task per core can be Running.
3. **Blocked** — waiting for a time delay to expire, a queue/semaphore to receive data, or another event. Not eligible to run until that event occurs.
4. **Suspended** — explicitly taken out of scheduling; only `vTaskResume()` can return it.

> **Blocked vs Suspended:** Blocked is **temporary & event-driven** (kernel auto-wakes the task). Suspended is **explicit & manual** — only another task's `vTaskResume()` can undo it.

> **Running is always singular (per core).** Every other Ready task waits its turn — the scheduler arbitrates using **priority**.

### 2.5.8 Scheduler — Priority-Based Preemption

**Rule:** The **highest-priority READY task always runs**. Equal-priority tasks share the CPU via **round-robin time slicing**.

Preemption example: Process task (priority 2) runs until Tx task (priority 3) becomes ready → Tx immediately preempts → Process resumes once Tx finishes. Idle task (priority 1) runs only when nothing else is ready.

### 2.5.9 Inter-Task Communication — Queues

A **queue** is a **FIFO buffer the kernel manages so tasks never touch shared memory directly — avoiding race conditions.**

```
[Sensor Task]──xQueueSend()──►[  ][  ][  ][  ]◄──xQueueReceive()──[Tx Task]
                            (Queue)
```

- Decouples producer and consumer — they can run at different speeds.
- A task calling `xQueueReceive()` on an **empty** queue **automatically blocks** (frees the CPU) until data arrives.
- This is how a sensing task hands readings to a transmission task on the ESP32.

### 2.5.10 Synchronization — Semaphores & Mutexes

| Type | Use |
|------|-----|
| **Binary Semaphore** | Single-count flag for signaling — e.g. an ISR signals "data ready" to unblock a task. |
| **Counting Semaphore** | Tracks how many of a limited resource are free — e.g. N free buffer slots. |
| **Mutex** | Binary semaphore with **ownership + priority inheritance** — protects a shared resource (e.g. UART/I²C bus). |

> **Priority Inversion:** If a low-priority task holds a mutex a high-priority task needs, the high-priority task blocks. A plain semaphore can leave this unresolved indefinitely; FreeRTOS mutexes solve it with **priority inheritance** — temporarily boosting the low-priority holder so it finishes and releases the resource quickly.

### 2.5.11 Three-Task ESP32 Example

A typical IoT node runs several FreeRTOS tasks concurrently, each pinned to a priority that reflects how time-critical it is.

| Task | Priority | Role |
|------|----------|------|
| `vSensorTask` | 2 | Reads a sensor every 100 ms, pushes value onto queue, then blocks (`vTaskDelay`). |
| `vProcessTask` | 1 | Blocks on `xQueueReceive()`; filters/averages readings when data arrives. |
| `vTxTask` | 3 (highest) | Woken by binary semaphore every transmit interval; sends data over Wi-Fi/BLE — preempts the others. |

> **Without an RTOS:** one superloop juggling timers by hand. **With FreeRTOS:** each concern is an independent task — the scheduler guarantees the transmit deadline is met even while sensing and processing keep running.

### 2.5.12 FreeRTOS Task Creation API

```c
xTaskCreate(
    blinkTask,        // 1. Function pointer
    "Blink",           // 2. Name (for debugging)
    1000,              // 3. Stack size in bytes
    NULL,              // 4. Parameters passed in (pvParameters)
    1,                 // 5. Priority (higher = more eager)
    NULL               // 6. Task handle (NULL = no reference kept)
);
```

### 2.5.13 `delay()` vs `vTaskDelay()` — Critical

| `delay(ms)` | `vTaskDelay(ms / portTICK_PERIOD_MS)` |
|-------------|----------------------------------------|
| Freezes the **entire program** — no other task runs | Pauses only the **current task** — others keep running |
| OK when nothing else needs to happen during the wait | This is what makes **true multitasking** possible on ESP32 |

### 2.5.14 Framework Comparison Table (QB Q21)

| Framework | Best For | Real-Time Capability | Footprint | Curve |
|-----------|----------|---------------------|-----------|-------|
| Arduino (IDE) | Quick prototypes, learning, huge library | None (superloop) | Small–Moderate | Gentle |
| MicroPython | Rapid scripting, education | Cooperative (asyncio) | Moderate–Large | Gentle |
| **ESP-IDF + FreeRTOS** | Production firmware, fine-grained hardware control | **Preemptive, real-time** | Small | Steep |
| Bare-metal (no OS) | Tightest resources | Manual / none | Smallest | Steepest |

### 2.5.15 MCU+RTOS vs SBC+Linux (QB Q23)

| Aspect | MCU + RTOS (ESP32/AVR with FreeRTOS) | SBC + Linux (Raspberry Pi) |
|--------|--------------------------------------|---------------------------|
| CPU class | Single/dual-core MCU, tens–hundreds of MHz | Multi-core app processor, 1+ GHz |
| RAM | KBs – low MBs | 512 MB – 8+ GB |
| Timing | **Deterministic** — bounded worst-case latency | Best-effort — not guaranteed |
| Power draw | mW – low W; sleeps deeply between events | Watts; harder to deep-sleep |
| Best fit | Direct sensor/actuator control, battery nodes | Edge gateways, local AI inference, dashboards |

---

# PYQs — MODEL ANSWERS

## 2024 PYQ (50 Marks, 2 Hours)

### Q1 [8 Marks] — Define sensor, actuator, embedded board; illustrate any 3 sensors with diagram + spec + working.

**Answer outline (write ~1 page total):**

**Definitions:**
- **Sensor:** Transducer that converts a physical quantity (temperature, pressure, light, motion, gas) into an electrical signal readable by a processor.
- **Actuator:** Transducer that converts an electrical command from the processor into a physical action (motion, switch, sound, heat, light).
- **Embedded board:** Small-form-factor computer built around an MCU/MPU with on-board GPIO, ADC, communication interfaces (I2C/SPI/UART), memory, and power regulation — designed to run a specific, dedicated task such as sensing-and-actuating in an IoT node. Examples: Arduino Uno (AVR), ESP32 DevKit, Raspberry Pi Pico, STM32 Nucleo, BeagleBone Black.

**Then illustrate 3 sensors from §1.4.4.** For each sensor give: 
- Block diagram (text-art is fine)
- Technical specification (Vcc, range, accuracy, interface)
- Working principle (3-4 lines)

### Q2 [10 Marks] — Elaborate IoT-WF standard architecture with neat labelled diagram and discussion.

**Answer outline (≈1.5 pages):**

1. **Introduction** — IoT-WF = IEEE P2413 / Cisco World Forum IoT Reference Model, a 7-layer architecture that is the de-facto industry reference, designed for cross-domain interoperability.
2. **Diagram** — Draw the 7-layer stack from §1.6.3.
3. **Layer-by-layer discussion** — For each of L1…L7 write 2-3 sentences: name, role, example technologies. Cover: Physical Devices, Connectivity, Edge Computing, Data Accumulation, Data Abstraction/Analytics, Collaboration, Application.
4. **Why it matters** — separation of concerns, vendor-neutral, cross-domain analytics, scalable from a single sensor to billions of devices.
5. **Example** — Apply to smart home: DHT11 sensor (L1) → Wi-Fi/MQTT (L2) → edge gateway RPi (L3) → DynamoDB (L4) → Rules Engine (L5) → energy+comfort optimization (L6) → mobile app (L7).

### Q3 [10 Marks] — Working principle of SPI and I2C.

Write §1.9.1 (SPI working + diagram) and §1.9.2 (I2C working + diagram) and the comparison table.

### Q4 [10 Marks] — Short notes on any 2 of {Bluetooth, Zigbee, NB-IoT, Sigfox, NFC}.

Pick the two you know best. For each, write ~½ page:
- Frequency, range, data rate, modulation
- Topology
- Working principle in 3-4 lines
- 2 applications

Recommended picks: **Zigbee + NFC** (you have full notes in §1.10.2 and §1.10.3). Alternative: **Bluetooth + Zigbee** if you've studied both.

### Q5 [12 Marks] — Design an IoT system (Problem Statement + Graphical Abstract + Framework + Virtualization + Distributed Data Computing) in one of: Smart Cities, Smart Healthcare, Smart Agriculture, Industry Automation, Smart Home.

**Recommended pick:** Smart Agriculture (well-defined, easy to score).

**Answer template:**
1. **Problem Statement** (3-4 lines) — Indian agriculture wastes ~40% of irrigation water due to blind scheduling; small farmers lack real-time soil-moisture data; yield loss due to under/over-irrigation.
2. **Graphical Abstract** — Block diagram: Soil-moisture sensor → ESP32 end-node → LoRa → Coordinator/Gateway → Cloud (AWS IoT Core) → Dashboard → Mobile app → Actuator (solenoid valve).
3. **Framework** — Use AWS IoT Core: Device Gateway + Message Broker + Rules Engine + Device Shadow + DynamoDB + Lambda for irrigation decisioning. See §2.2.3.
4. **Virtualization** — Run multiple virtual sensor profiles on one physical gateway (e.g. soil-moisture emulator + weather emulator + crop-model emulator) for what-if testing before deployment. See §2.3.
5. **Distributed Data Computing** — Edge nodes aggregate locally; gateway runs first-pass filter; cloud runs ML yield-prediction model; rules engine triggers valve actuation.
6. Map to IoT-WF 7 layers (L1 sensors → L2 LoRa → L3 gateway → L4 DynamoDB → L5 Rules Engine → L6 cross-domain → L7 app).
7. Map to IoT Level 5 (multiple end-nodes + 1 coordinator + cloud).

## 2025 PYQ (25 Marks, 1 Hour)

### Q1.A [5 Marks] — Battery-Powered Occupancy Sensor Numerical

**Given:** Battery 3.7 V, 2400 mAh Li-ion. Active: 25 mA for 1 s every 2 min. Sleep: 80 µA otherwise.

**a) Average current consumption:**
- Cycle length = 2 min = 120 s.
- Active time per cycle = 1 s; sleep time per cycle = 119 s.
- I_avg = (25 mA × 1 s + 0.080 mA × 119 s) / 120 s
- I_avg = (25 + 9.52) / 120
- I_avg = 34.52 / 120
- **I_avg ≈ 0.2877 mA**

**b) Device lifetime:**
- Lifetime = Battery capacity / I_avg
- Lifetime = 2400 mAh / 0.2877 mA ≈ **8342 hours**
- In days: 8342 / 24 ≈ **347.6 days**
- In years: 347.6 / 365 ≈ **0.952 years (≈ 11.4 months)**

**c) Battery replacements for 40 sensors over 3 years:**
- Lifetime per sensor ≈ 0.952 years.
- Number of replacements per sensor in 3 years = 3 / 0.952 ≈ 3.15 → **3 replacements** per sensor (the 4th is at the very end of year 3 — depending on rounding, state 3 or 4; with 0.952-year lifetime → 4 batteries used in 3 years → **3 replacements** i.e. initial battery + 3 swaps).
- For 40 sensors: total replacements = 40 × 3 = **120 battery replacements** over 3 years.
- (Or state: 40 × 4 = 160 batteries consumed, of which 40 are the initial set → 120 replacements.)

### Q1.B [5 Marks] — Temperature + Light Sensor Data Generation

**Given:** Temperature sensor — packet every 30 s, packet size 250 bytes. Light sensor — every 10 s, packet size 90 bytes. Day length = 86 400 s.

**Temperature sensor:**
- Packets in 24 h = 86 400 / 30 = **2880 packets**.
- Data = 2880 × 250 bytes = 720 000 bytes = **720 KB ≈ 0.703 MB**.

**Light sensor:**
- Packets in 24 h = 86 400 / 10 = **8640 packets**.
- Data = 8640 × 90 bytes = 777 600 bytes = **777.6 KB ≈ 0.760 MB**.

**Total data generated in 24 h** = 720 000 + 777 600 = 1 497 600 bytes ≈ **1.4976 MB ≈ 1.46 MB**.

### Q2 [10 Marks] — IoT-WF Level 5+ smart academic campus

**Answer outline (≈2 pages):**

1. **Problem statement:** Transform the university into an IoT-enabled smart academic campus that optimises **energy**, **space utilisation**, **mobility**, and **safety**.
2. **Architecture choice:** IoT-WF 7-Layer architecture; deploy at **Level 5** (multiple end-nodes + coordinator per building) and **Level 6** (multiple independent end-nodes + central controller aware of all nodes).
3. **Diagram (draw on paper):**
   ```
   Per building:
   [Temp/Occ/Light/Smoke sensors]──┐
                                   ├─► [Coordinator/Gateway (RPi)]
   [Smart meters, HVAC controllers]┘          │
                                              ▼
                              [Campus Wi-Fi/Ethernet backbone]
                                              │
                                              ▼
                          [Cloud: AWS IoT Core + DynamoDB + Lambda]
                                              │
                          ┌───────────────────┼───────────────────┐
                          ▼                   ▼                   ▼
                  [Energy app]        [Space util app]    [Safety app]    [Mobility app]
   ```
4. **Layer mapping (IoT-WF 7 layers):**
   - L1 Physical — DHT22, PIR, smart-meter CT clamps, smoke detectors.
   - L2 Connectivity — Wi-Fi (indoor), LoRa (outdoor), BLE (indoor positioning), Ethernet backbone.
   - L3 Edge — RPi gateway per building runs filter + local analytics + protocol conversion (MQTT broker relay).
   - L4 Data Accumulation — DynamoDB for sensor time-series, S3 for raw logs.
   - L5 Data Abstraction — AWS IoT Rules Engine routes data; aggregates per-building; analytics views in Timestream.
   - L6 Collaboration — cross-domain apps: e.g. energy app combines occupancy + HVAC setpoint + electricity tariff.
   - L7 Application — dashboards (admin), mobile app (faculty/students for room booking, parking, alerts).
5. **Optimisation goals mapped:**
   - **Energy** — smart meters per building, HVAC setpoint tuned by occupancy, lighting dimmed when PIR empty. 30% reduction target.
   - **Space** — PIR-based room-occupancy heatmap → re-allocate timetable to under-used rooms; meeting-room booking via NFC tap.
   - **Mobility** — BLE beacons for indoor navigation; parking sensors (ultrasonic) report free slots to mobile app.
   - **Safety** — smoke sensors → MQTT alert → Lambda → SMS + automated door release; CCTV with edge AI for intrusion.
6. **Mention Device Shadow** for offline-tolerant actuator commands, **OTA updates** for firmware, **X.509 certs** for security.
7. Conclude with the KPI: 30% energy savings, 25% better space utilisation, sub-2s safety alert latency.

### Q3 [5 Marks] — Mid-range IoT access technology

**Recommended pick: Zigbee** (you have full notes in §1.10.2) — or NFC if you prefer.

**Template for Zigbee:**
- **Working Principle:** Based on IEEE 802.15.4 PHY/MAC; O-QPSK DSSS modulation on 2.4 GHz ISM. Coordinator forms network and assigns 16-bit short addresses; routers extend coverage via multi-hop mesh; end devices sleep between transmissions to save battery. CSMA/CA avoids collisions; AES-128 secures frames.
- **Network Architecture:** Star / Tree / Mesh topology. Roles: Coordinator (1 per network), Router (mains-powered, forwards packets), End Device (battery, sleeps, talks only to parent).
- **Packet Structure:** IEEE 802.15.4 frame = Synchronization (preamble + SFD) + PHY header (length) + MAC header (frame control + seq no + addressing) + payload (up to 127 bytes) + FCS (2-byte CRC).
- **Key Technical Specs:** 2.4 GHz, 250 kbps, 10-100 m range, up to 65535 nodes, 128-bit AES, ~years of battery life on coin cells for end devices.

---

# NUMERICALS — FORMULA SHEET + 10 SOLVED EXAMPLES

## 3.1 Master Formula Sheet

| Concept | Formula |
|---------|---------|
| Data rate | `R = (Data size in bits) / Time` |
| Battery life | `Lifetime (h) = Battery capacity (mAh) / I_avg (mA)` |
| Avg current | `I_avg = (I_active × t_active + I_sleep × t_sleep) / Total cycle time` |
| Transmission latency | `Latency = Packet size (bits) / Bandwidth (bps)` |
| Data per day | `Packets = (86400 / interval); Data = Packets × payload_size` |
| Bandwidth utilization | `U = (Device data rate / Network BW) × 100%` |
| Energy/day | `E = Power × time; Energy/month = E × 30` |
| Samples generated | `Samples = Sampling rate × duration` |
| Packet loss rate | `Loss% = ((Sent - Received) / Sent) × 100` |
| Received signal strength | `RSSI = Tx power (dBm) − Path loss (dB)` |
| Shannon capacity | `C = B × log₂(1 + SNR)` |
| SNR (linear) from dB | `SNR_linear = 10^(SNR_dB / 10)` |
| TDMA feasibility | `Sum(t_i) ≤ T_frame` where `t_i = D_i / R_i` |

## 3.2 The 10 Numericals from the Slides (Solved)

### N1. Data rate
A sensor generates 200 bytes in 5 s. Find data rate in bps.  
- Data = 200 × 8 = 1600 bits.  
- **Rate = 1600 / 5 = 320 bps**.

### N2. Battery life with duty cycling
Active 10 mA for 2 h, sleep 0.5 mA for 22 h per day. Battery 1000 mAh.  
- I_avg per day = (10 × 2 + 0.5 × 22) / 24 = (20 + 11) / 24 = 31/24 = 1.292 mA.  
- Lifetime = 1000 / 1.292 ≈ **774 days**.  
  *(Note: An alternative reading in the slides computes daily mAh directly: 20 + 11 = 31 mAh/day → 1000/31 ≈ 32.26 days. Use whichever matches the slide's framing.)*

### N3. Transmission latency
512-byte packet over 1 Mbps link.  
- Packet = 512 × 8 = 4096 bits.  
- BW = 1 Mbps = 1 000 000 bps.  
- **Latency = 4096 / 1 000 000 = 4.096 ms ≈ 4.1 ms**.

### N4. Data stored per day
Temp sensor every 10 s, packet 100 bytes.  
- Packets/day = 86 400 / 10 = 8640.  
- **Data/day = 8640 × 100 = 864 000 bytes = 864 KB**.

### N5. Received signal strength
2.4 GHz, Tx 10 dBm, path loss 100 dB.  
- **RSSI = 10 − 100 = −90 dBm**.

### N6. Bandwidth utilization
Device 5 Mbps, network 20 Mbps.  
- **U = (5/20) × 100 = 25%**.

### N7. Energy per month
1.5 mW avg, 12 h/day, 30 days.  
- Energy/day = 1.5 mW × 12 h = 18 mWh.  
- **Energy/month = 18 × 30 = 540 mWh = 0.54 Wh**.

### N8. Samples per minute
Sampling rate 2000 Hz for 1 min.  
- **Samples = 2000 × 60 = 120 000**.

### N9. Packet loss rate
1000 sent, 920 received.  
- Loss = 1000 − 920 = 80.  
- **Loss% = (80 / 1000) × 100 = 8%**.

### N10. Mesh network total data
5 nodes, each sends 50 KB/hour to central node. Find total in 1 day.  
- Per node per day = 50 × 24 = 1200 KB.  
- Total = 1200 × 5 = 6000 KB.  
- **= 6 MB**.

## 3.3 Resource-Management Numericals (extra practice)

See §1.11.3 for the three advanced resource-management problems (TDMA allocation, duty cycling, offload vs local).

## 3.4 Quick PYQ-Style Drills (Solve Without Looking)

1. Sensor samples 100 bytes every 5 s for 1 hour. Find data rate (bps) and total data (KB).  
   *Ans: 160 bps, 72 KB.*
2. Battery 1500 mAh, I_active = 30 mA for 0.5 s/min, sleep 50 µA otherwise. Find lifetime in days.  
   *Ans: ≈ 1157 days ≈ 3.17 years.*
3. 1024-byte packet over 2 Mbps link — find latency.  
   *Ans: ≈ 4.1 ms.*
4. Sensor 100 Hz sampling, 8 bytes/sample, 1 hour. Total data?  
   *Ans: 2.88 MB.*
5. Tx power 23 dBm, path loss 90 dB — RSSI?  
   *Ans: −67 dBm.*

---

# LAST-MINUTE REVISION CHEAT-SHEET (1 page)

## Mnemonics
- **IoT 7 Characteristics:** *S*mart, *C*onnected, *I*dentified, *C*onfigured, *C*ommon-net, *I*nteroperable, *I*ntelligent.
- **IoT-WF 7 layers (top→bottom):** *App-Collab-Abstraction-Accumulation-Edge-Connect-Physical* — "**A CAME CP**" (think "a camel came for tea with the chief priest").
- **SPI 4 lines:** *S*CLK, *M*OSI, *M*ISO, *S*S — "**SMMSS**".
- **I²C 2 lines:** *S*DA, *S*CL — "**S-S**".
- **NFC 3 modes:** *R*eader, *P*2P, *C*ard-Emulation — "**RPC**".
- **FreeRTOS 4 task states:** *R*eady, *R*unning, *B*locked, *S*uspended — "**RRBS**".
- **REST verbs:** GET / POST / PUT / DELETE.
- **CoAP message types:** CON, NON, ACK, RST.

## Must-Diagram Checklist
- [ ] IoT-WF 7-layer architecture
- [ ] IoT Levels 1-6 component placement
- [ ] SPI master-slave wiring (1 slave + multi-slave)
- [ ] I²C START / STOP / ACK timing
- [ ] Zigbee star/tree/mesh + coordinator/router/end-device
- [ ] NFC inductive-coupling diagram
- [ ] FreeRTOS task states
- [ ] AWS IoT Core architecture flow
- [ ] Smart-campus architecture (for Q2 design)

## Numbers You MUST Memorise
| Item | Value |
|------|-------|
| NFC frequency | 13.56 MHz |
| NFC max rate | 424 kbps |
| NFC range | ≤ 4–10 cm |
| Bluetooth band | 2.4 GHz, 79 channels × 1 MHz |
| Bluetooth hop rate | 1600 hops/s |
| Bluetooth slot | 625 µs |
| Zigbee band | 2.4 GHz (also 868/915) |
| Zigbee rate | 250 kbps |
| Zigbee range | 10–100 m |
| Zigbee AES | 128-bit |
| I²C speeds | 100 k / 400 k / 3.4 M bps |
| SPI lines | SCLK, MOSI, MISO, SS |
| LoRa range | 15+ km |
| NB-IoT BW | 200 kHz |
| MQTT header | 2 bytes |
| CoAP header | 4 bytes |
| MQTT QoS | 0, 1, 2 (at-most / at-least / exactly once) |
| ESP32 ADC | 12-bit, 0–4095, 0–3.3 V |
| ESP32 logic | 3.3 V (not 5 V tolerant) |
| FreeRTOS footprint | 6–12 KB flash |
| Day length | 86 400 s |

## Common Mistakes To Avoid
1. Forgetting units in numericals — **always write mA, h, ms, dBm, bps, KB, etc.**
2. Drawing the IoT-WF diagram but not labeling each layer.
3. Confusing Zigbee coordinator vs router vs end-device.
4. Saying "NFC is faster than Bluetooth" — it isn't (424 kbps vs 1-2 Mbps); it's *shorter range, easier pairing*.
5. Writing only theory for design questions — the question mandates Problem Statement + Graphical Abstract + Framework + Virtualization + Distributed Computing. Skip any = lose marks.
6. For Q3 access-technology question, not covering all 4 required aspects (Working, Architecture, Packet, Specs).
7. Mixing up MQTT QoS levels: 0 = at-most-once, 1 = at-least-once, 2 = exactly-once.
8. Writing single-line answers — every section needs **3-5 sentences minimum** with examples.

## Top 12 Likely Questions for 2026 Mid-Sem

1. **Numerical** — battery-life or data-rate or transmission latency or packet loss or bandwidth util (100% probability based on 2025 pattern).
2. **IoT-WF 7-layer architecture** — explain, with diagram and Level 5+ example (smart campus, smart agriculture, smart hospital).
3. **Access technology short notes** — Zigbee / NFC / Bluetooth / NB-IoT / Sigfox.
4. **Sensors** — definition + illustrate 3 sensors with diagram, spec, working.
5. **SPI & I2C** — full working principles with diagrams + comparison.
6. **MQTT vs CoAP** — architecture, message format, QoS, comparison.
7. **IoT Frameworks** — AWS IoT Core architecture and features.
8. **RTOS** — definition, FreeRTOS architecture, tasks/scheduler/queues/semaphores.
9. **MCU vs MPU vs SBC** — comparison + selection criteria.
10. **Virtualization in IoT** — definition, benefits, use cases, challenges.
11. **6LoWPAN** — role and importance.
12. **IoT system design** — full design with framework + virtualization + distributed data computing for a chosen domain.

---

## Final Note

This prep covers every PDF, PPTX, PNG, and TXT file in the repo, cross-referenced with the 2024 and 2025 PYQs and the IoT Question Bank. Topics not in the PYQ pattern (e.g. detailed NFC layers, RTOS state-machine nuances) are still covered because the Question Bank lists them — they may appear as short-answer parts.

**Suggested study order:**
1. Read §0 (strategy) and §3.1 (formula sheet).
2. Master §1.6.3 (IoT-WF 7-layer) + §1.7 (Levels 1-6) + §1.10 (Access Tech).
3. Practice §3.2 (10 numericals) + PYQ numericals (§2025 Q1).
4. Read §1.9 (SPI/I2C) + §1.4 (sensors) for the 8-mark / 10-mark questions.
5. Skim §2 (Unit 2) for the QB-listed medium-answer questions.
6. Re-read this cheat-sheet (§4) the morning of the exam.

Good luck!
