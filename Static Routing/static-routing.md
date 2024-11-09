# Static Routing Lab
In this lab, we have configured static routing between three routers (R1, R2, and R3)

to enable communication between different networks.

## Topology Setup
![Screenshot 1](https://github.com/user-attachments/assets/b3448e09-3042-4a0d-b292-beb0ecad118c)
![Screenshot 2](https://github.com/user-attachments/assets/5f8c26f2-cbb5-467f-b06c-b4f3747b4b64)

The syntax for static routing used is:
```bash
ip route DestinationNetwork SubnetMask NextHopAddress
```
# Router Configurations
## Router 1
```bash
Router>en
Router#conf t
Router(config)#hostname R1
R1(config)#int gig0/0
R1(config-if)#ip add 192.168.42.1 255.255.255.0
R1(config-if)#no shut
```
## Router 2
```bash
Router>en
Router#conf t
Router(config)#hostname R2
R2(config)#int gig0/0
R2(config-if)#ip add 172.168.32.1 255.255.0.0
R2(config-if)#no shut
```
## Router 3
```bash
Router>en
Router#conf t
Router(config)#hostname R3
R3(config)#int gig0/0
R3(config-if)#ip add 150.168.22.1 255.255.0.0
R3(config-if)#no shut
```
![Screenshot 3](https://github.com/user-attachments/assets/96aeadaa-e600-40ad-9e70-bd69e865c900)
## Static Routing for R1
```bash
R1(config)#ip route 172.168.0.0 255.255.0.0 10.0.0.2
R1(config)#ip route 150.168.0.0 255.255.0.0 12.0.0.2
R1(config)#ip route 12.0.0.0 255.0.0.0 10.0.0.2
```
## Static Routing for R2
```bash
R2(config)#ip route 192.168.42.0 255.255.255.0 10.0.0.1
R2(config)#ip route 150.168.0.0 255.255.0.0 12.0.0.2
```
## Static Routing for R3
```bash
R3(config)#ip route 10.0.0.0 255.0.0.0 12.0.0.1
R3(config)#ip route 172.168.0.0 255.255.0.0 12.0.0.1
R3(config)#ip route 192.168.42.0 255.255.255.0 10.0.0.1
```
**Again the syntax used for static routing is:**
```bash
ip route DestinationNetwork SubnetMask NextHopAddress
```
## After Configuring all the routers
![Screenshot 4](https://github.com/user-attachments/assets/fc672934-8879-40ae-b837-669a45c2e303)
