%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#e1f5fe', 'edgeLabelBackground':'#ffffff', 'tertiaryColor': '#fff'}}}%%
graph TD
    %% 先定义子图和节点，确保它们乖乖待在框内
    subgraph Subnet_0 [Bell Network: 192.168.0.0/24]
        direction TB
        BellRouter["Bell Home Hub<br/>(Main Router)<br/>IP: 192.168.0.1"]
        
        %% 无线 Wi-Fi 连接
        DaughterMBA["Daughter's<br/>MacBook Air<br/>IP: 192.168.0.10"]
        DaughteriPad["Daughter's<br/>iPad<br/>IP: 192.168.0.11"]
        DaughterWatch["Daughter's<br/>Watch<br/>IP: 192.168.0.12"]
        
        BellRouter -.->|"Wi-Fi"| DaughterMBA
        BellRouter -.->|"Wi-Fi"| DaughteriPad
        BellRouter -.->|"Wi-Fi"| DaughterWatch
    end

    subgraph Subnet_1 [TP-Link Network: 192.168.1.0/24]
        direction TB
        TPLinkRouter["TP-Link Router<br/>(Secondary Router)<br/>IP: 192.168.1.1"]
        
        %% 用户设备连接
        MyMBP["My<br/>MacBook Pro<br/>IP: 192.168.1.10"]
        MyiPhone["My<br/>iPhone 13 mini<br/>IP: 192.168.1.11"]
        MyLenovo["My<br/>Lenovo Laptop<br/>IP: 192.168.1.12"]
        MyKindle["My<br/>Kindle<br/>IP: 192.168.1.13"]

        TPLinkRouter -.->|"Wi-Fi/Wired"| MyMBP
        TPLinkRouter -.->|"Wi-Fi"| MyiPhone
        TPLinkRouter -.->|"Wi-Fi"| MyLenovo
        TPLinkRouter -.->|"Wi-Fi"| MyKindle
    end

    %% 定义完子图后，再进行跨区域的连接
    Internet(("Internet<br/>ISP: Bell 1Gbps")) --- BellRouter

    %% 跨公寓的长网线连接 (修复了粗实线带文字的语法)
    BellRouter == "Long Ethernet Cable<br/>(Cross Apartment)" === TPLinkRouter

    %% 样式美化
    classDef router fill:#b3e5fc,stroke:#01579b,stroke-width:2px;
    classDef device fill:#fff,stroke:#333,stroke-width:1px,stroke-dasharray: 5 5;
    classDef internet fill:#f44336,stroke:#b71c1c,stroke-width:2px,color:#fff;
    
    class BellRouter,TPLinkRouter router;
    class DaughterMBA,DaughteriPad,DaughterWatch,MyMBP,MyiPhone,MyLenovo,MyKindle device;
    class Internet internet;
