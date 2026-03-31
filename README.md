# Home Network Documentation 🏠

This repository documents the network architecture, devices, and configurations of my home network.

## 🌐 Network Topology

Below is the visual representation of our current network setup, spanning across the apartment and divided into two main subnets.

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#e1f5fe', 'edgeLabelBackground':'#ffffff', 'tertiaryColor': '#fff'}}}%%
graph TD
    %% 子网 0 (Bell - Main Network)
    subgraph Subnet_0 [Bell Network: 192.168.0.0/24]
        direction TB
        BellRouter["Bell Home Hub<br/>(Main Router)<br/>IP: 192.168.0.1"]
        
        %% Daughter's Devices
        DaughterMBA["Daughter's<br/>MacBook Air<br/>IP: 192.168.0.10"]
        DaughteriPad["Daughter's<br/>iPad<br/>IP: 192.168.0.11"]
        DaughterWatch["Daughter's<br/>Watch<br/>IP: 192.168.0.12"]
        
        BellRouter -.->|"Wi-Fi"| DaughterMBA
        BellRouter -.->|"Wi-Fi"| DaughteriPad
        BellRouter -.->|"Wi-Fi"| DaughterWatch
    end

    %% 子网 1 (TP-Link - Secondary Network)
    subgraph Subnet_1 [TP-Link Network: 192.168.1.0/24]
        direction TB
        TPLinkRouter["TP-Link Router<br/>(Secondary Router)<br/>IP: 192.168.1.1"]
        
        %% My Devices
        MyMBP["My<br/>MacBook Pro<br/>IP: 192.168.1.10"]
        MyiPhone["My<br/>iPhone 13 mini<br/>IP: 192.168.1.11"]
        MyLenovo["My<br/>Lenovo Laptop<br/>IP: 192.168.1.12"]
        MyKindle["My<br/>Kindle<br/>IP: 192.168.1.13"]

        TPLinkRouter -.->|"Wi-Fi/Wired"| MyMBP
        TPLinkRouter -.->|"Wi-Fi"| MyiPhone
        TPLinkRouter -.->|"Wi-Fi"| MyLenovo
        TPLinkRouter -.->|"Wi-Fi"| MyKindle
    end

    %% 互联网与主干连接
    Internet(("Internet<br/>ISP: Bell 1Gbps")) --- BellRouter

    %% 跨房间物理连接
    BellRouter == "Long Ethernet Cable<br/>(Cross Apartment)" === TPLinkRouter

    %% 样式美化
    classDef router fill:#b3e5fc,stroke:#01579b,stroke-width:2px;
    classDef device fill:#fff,stroke:#333,stroke-width:1px,stroke-dasharray: 5 5;
    classDef internet fill:#f44336,stroke:#b71c1c,stroke-width:2px,color:#fff;
    
    class BellRouter,TPLinkRouter router;
    class DaughterMBA,DaughteriPad,DaughterWatch,MyMBP,MyiPhone,MyLenovo,MyKindle device;
    class Internet internet;
```

## 📝 Device Directory

| Owner | Device | IP Address | Connection |
| :--- | :--- | :--- | :--- |
| **Network** | Bell Home Hub (Main) | `192.168.0.1` | WAN |
| **Network** | TP-Link Router (Secondary) | `192.168.1.1` | Ethernet to Main |
| **Daughter** | MacBook Air | `192.168.0.10` | Wi-Fi (Bell) |
| **Daughter** | iPad | `192.168.0.11` | Wi-Fi (Bell) |
| **Daughter** | Apple Watch | `192.168.0.12` | Wi-Fi (Bell) |
| **Mine** | MacBook Pro | `192.168.1.10` | Wi-Fi/Wired (TP-Link) |
| **Mine** | iPhone 13 mini | `192.168.1.11` | Wi-Fi (TP-Link) |
| **Mine** | Lenovo Laptop | `192.168.1.12` | Wi-Fi (TP-Link) |
| **Mine** | Kindle | `192.168.1.13` | Wi-Fi (TP-Link) |
