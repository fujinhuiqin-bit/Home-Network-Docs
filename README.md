%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#e1f5fe', 'edgeLabelBackground':'#ffffff', 'tertiaryColor': '#fff'}}}%%
graph TD
    %% 互联网接入
    Internet((Internet<br/>ISP: Bell 1Gbps)) --- BellRouter

    %% Bell 主路由区域 (192.168.0.0/24 Subnet)
    subgraph Subnet_0 [Bell Network: 192.168.0.0/24]
        direction TB
        BellRouter[Bell Home Hub<br/>(Main Router)<br/>IP: 192.168.0.1]
        
        %% 无线连接
        BellRouter -.->|Wi-Fi| DaughterMBA[Daughter's<br/>MacBook Air<br/>IP: 192.168.0.10]
        BellRouter -.->|Wi-Fi| DaughteriPad[Daughter's<br/>iPad<br/>IP: 192.168.0.11]
        BellRouter -.->|Wi-Fi| DaughterWatch[Daughter's<br/>Watch<br/>IP: 192.168.0.12]
    end

    %% 跨房间有线连接
    BellRouter ===|Long Ethernet Cable<br/>(Cross Apartment)| TPLinkRouter

    %% TP-Link 二级路由区域 (192.168.1.0/24 Subnet)
    subgraph Subnet_1 [TP-Link Network: 192.168.1.0/24]
        direction TB
        TPLinkRouter[TP-Link Router<br/>(Secondary Router)<br/>IP: 192.168.1.1]
        
        %% 无线/有线连接
        TPLinkRouter -.->|Wi-Fi/Wired| MyMBP[My<br/>MacBook Pro<br/>IP: 192.168.1.10]
        TPLinkRouter -.->|Wi-Fi| MyiPhone[My<br/>iPhone 13 mini<br/>IP: 192.168.1.11]
        TPLinkRouter -.->|Wi-Fi| MyLenovo[My<br/>Lenovo Laptop<br/>IP: 192.168.1.12]
        TPLinkRouter -.->|Wi-Fi| MyKindle[My<br/>Kindle<br/>IP: 192.168.1.13]
    end

    %% 样式定义
    classDef router fill:#b3e5fc,stroke:#01579b,stroke-width:2px;
    classDef device fill:#fff,stroke:#333,stroke-width:1px,stroke-dasharray: 5 5;
    classDef internet fill:#f44336,stroke:#b71c1c,stroke-width:2px,color:#fff;
    
    class BellRouter,TPLinkRouter router;
    class DaughterMBA,DaughteriPad,DaughterWatch,MyMBP,MyiPhone,MyLenovo,MyKindle device;
    class Internet internet;
