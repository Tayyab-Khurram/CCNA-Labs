# DHCP Lab Configuration
This document covers the DHCP configuration commands used in our lab.

Below is a structured list of the commands along with explanations to help you understand the setup process.

## Topology Setup
![screenshot 1](https://github.com/user-attachments/assets/8cc31cce-c099-46ac-a3b1-251c4f933508)
![Screenshot-2](https://github.com/user-attachments/assets/451420cd-f609-43fe-a5da-a591416e6101)

## Router Configuration
```bash
Router> en
Router# conf t
Router(config)# int gig0/0
Router(config-if)# ip add 192.168.23.1 255.255.255.0
Router(config-if)# no shut
Router(config-if)# exit
```
##  Setting Up the DHCP Pool
```bash
Router(config)# ip dhcp pool MY_HOME_NETWORK
Router(dhcp-config)# default-router 192.168.23.1 
Router(dhcp-config)# network 192.168.23.0 255.255.255.0
```
**Explanation: Creates a DHCP pool named MY_HOME_NETWORK:**

Sets the default gateway for DHCP clients to 192.168.23.1.

Configures the network range (192.168.23.0/24) that will be assigned to DHCP clients.
  
## DHCP Enabled on the Router
![Screenshot-3](https://github.com/user-attachments/assets/8ad200bf-ee9b-4c61-94b8-c0fb00e4d988)
![Screenshot-4](https://github.com/user-attachments/assets/8f9094b3-eb7b-4ea8-b333-78736b79b68e)
![Screenshot-5](https://github.com/user-attachments/assets/9aa7c9b8-e072-4d84-a0f8-4b03909af139)

### All the devices are able to ping each other
![Screenshot-6](https://github.com/user-attachments/assets/cf09866b-bbb5-4b7a-9bad-984b240c94d2)
![Screenshot-7](https://github.com/user-attachments/assets/4910a0fe-a21a-4f57-b7ca-8671bcd8d168)
