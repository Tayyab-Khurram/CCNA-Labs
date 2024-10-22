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
```

### 5. Configure IP Address on GigabitEthernet 0/0
```bash
R1(config)#int gig0/0
R1(config-if)#ip add 1.1.1.222 255.0.0.0
R1(config-if)#no shut
R1(config-if)#Ctrl + C
```

### 6. Save the Configuration
```bash
R1#wr
```

### 7. Configure Telnet Access (VTY Lines)
```bash
R1#conf t
R1(config)#line vty 0 5
R1(config-line)#password 123
R1(config-line)#login
```

## **Switch Configuration (SW-A)**

### 1. Basic Configurations
```bash
Switch>en
Switch#conf t
Switch(config)#hostname SW-A
SW-A(config)#enable password cisco
```

### 5. Configure IP Address on VLAN 1

Typically, Layer 2 switches don’t have an IP address because they operate using MAC addresses for forwarding traffic. However, managed switches, which offer additional features like remote management, monitoring, and VLAN configuration, usually have an IP address assigned for administrative purposes. This IP allows network administrators to access the switch's interface for configuration and management. Right?

```bash
SW-A(config)#int vlan 1
SW-A(config-if)#ip add 1.1.1.1 255.0.0.0
SW-A(config-if)#no shut
SW-A(config-if)#exit
```

### 6. Configure Telnet Access (VTY Lines)
```bash
SW-A(config)#line vty 0 5
SW-A(config-line)#password cisco
SW-A(config-line)#login
SW-A(config-line)#exit
```

---

### **Usage Instructions**

- After setting up the configurations on both the **Router (R1)** and **Switch (SW-A)**, you can test Telnet connectivity by accessing the devices from a PC or server in the network.
  
- Telnet can be initiated by using the command:
```bash
telnet 1.1.1.1
```

This will allow you to remotely manage the switch using the configured Telnet password.
