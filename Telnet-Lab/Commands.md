## Topology Overview

This topology consists of:
- A **Router (R1)** with IP address: 1.1.1.222 on GigabitEthernet 0/0.
- A **Switch (SW-A)** with IP address: 1.1.1.1 on VLAN 1.
- PCs and a server for testing Telnet access.

## **Router Configuration (R1)**

### 1. Basic Configurations
```bash
Router>en
Router#conf t
Router(config)#hostname R1
R1(config)#enable password cisco

### 2. Configure IP Address on GigabitEthernet 0/0

R1(config)#int gig0/0
R1(config-if)#ip add 1.1.1.222 255.0.0.0
R1(config-if)#no shut
