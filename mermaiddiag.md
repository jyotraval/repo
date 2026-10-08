flowchart TD

    A["Incoming Request"] --> B{"Request Type"}

    B -->|"eMBB / 1"| C["Load eMBB Weights"]
    B -->|"URLLC / 2"| D["Load URLLC Weights"]
    B -->|"mMTC / 3"| E["Load mMTC Weights"]

    C --> F["Server Data"]
    D --> F
    E --> F

    F --> G["Read Server Parameters"]

    G --> G1["CPU"]
    G --> G2["Memory"]
    G --> G3["Bandwidth"]
    G --> G4["Latency"]
    G --> G5["Active Connections"]
    G --> G6["Packet Loss"]

    G1 --> H["Normalize Parameters"]
    G2 --> H
    G3 --> H
    G4 --> H
    G5 --> H
    G6 --> H

    H --> I["Benefit Normalization"]
    H --> J["Cost Normalization"]

    I --> I1["Bandwidth: Higher = Better"]
    J --> J1["CPU: Lower = Better"]
    J --> J2["Memory: Lower = Better"]
    J --> J3["Latency: Lower = Better"]
    J --> J4["Connections: Lower = Better"]
    J --> J5["Packet Loss: Lower = Better"]

    I1 --> K["Weighted Score"]
    J1 --> K
    J2 --> K
    J3 --> K
    J4 --> K
    J5 --> K

    K --> L["Calculate Score for Every Server"]

    L --> M{"Highest Score?"}

    M --> N["Selected Server ID"]

    N --> O["Forward Request to Selected Server"]
