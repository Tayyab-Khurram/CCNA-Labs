# Access Control Lists (ACL) Lab

ACLs are used to filter the network traffic by allowing a user to permit or deny IP packets from a specified interfaces.   
Just imagine you come to a fair and see the guardian checking tickets.  
He only allows people with suitable tickets to enter. Well, an access list’s function is same as that guardian.  

This document contains the step-by-step ACL configurations between Network1 and Network2, along with screenshots from the lab.
## Topology Overview

![Screenshot 1](https://github.com/user-attachments/assets/9c88ce48-b215-4539-8bd2-07dd653aaec1)

## Step 1: Router1 Configuration
```bash
Router>en
Router#conf t
Router(config)#hostname R1
R1(config)#int fa0/0
R1(config-if)#ip add 150.1.0.1 255.255.0.0
R1(config-if)#no shut
R1(config-if)#Ctrl^C
R1#conf t
R1(config)#int se0/2/0
R1(config-if)#ip add 100.0.0.1 255.0.0.0
R1(config-if)#no shut
```
## Step 2: Router2 Configuration
```bash
Router>en
Router#conf t
Router(config)#int fa0/0
Router(config-if)#ip add 192.168.0.1 255.255.255.0
Router(config-if)#no shut
Router(config-if)#Ctrl^C
Router#conf t
Router(config)#hostname R2
R2(config)#int se0/2/0
R2(config-if)#ip add 100.0.0.2 255.0.0.0
R2(config-if)#no shut
```
#### I hope you know how to assign IPs on the PCs and Laptops!
#### Every device inside its own network can now ping other devices after assigning IP addresses

![Screenshot 2](https://github.com/user-attachments/assets/fddbf33d-a65a-426d-b44e-12d72eb8f08c)

## Step 3: Enabling Routing between the networks
**What is OSPF?**  
OSPF, or Open Shortest Path First, is a Link-State routing protocol used in IP networks.  
It helps routers determine the best path for data to travel within a network. Here's a quick rundown:
```bash
R1(config)#router ospf 111
R1(config-router)#network 150.1.0.0 0.0.255.255 area 0
R1(config-router)#network 100.0.0.0 0.255.255.255 area 0
```
```bash
R2(config)#router ospf 111
R2(config-router)#network 192.168.0.0 0.0.0.255 area 0
R2(config-router)#network 100.0.0.0 0.255.255.255 area 0
R2(config-router)# 00:33:53: %OSPF-5-ADJCHG: Process 111, Nbr 150.1.0.1 on Serial0/2/0 from LOADING to FULL, Loading Done
```
#### After Enabling the routing, every device outside its own network can ping other devices.

![Screenshot 3](https://github.com/user-attachments/assets/1071b68e-b63a-4b23-b3ed-bbbd1cf63700)

## Step 4: Denying the Intruder
An intruder has gained access to our network and is able to communicate with each device since routing has been done already.

![Screenshot 4](https://github.com/user-attachments/assets/30ebcbce-fda2-43ec-aaa7-56ca645fae4b)

#### Now we will apply Standard ACL on the Router2 to block this device
A "standard ACL" is a network security feature that filters traffic based only on the source IP address.
```bash
R2(config)#access-list  ?
  <1-99>     IP standard access list
  <100-199>  IP extended access list
  # Defining the ACL
R2(config)#access-list 33 deny host 192.168.0.9
R2(config)#access-list 33 permit any
	# Applying the ACL
R2(config)#int fa0/0
R2(config-if)#ip access-group 33 in
R2(config-if)#int se0/2/0
R2(config-if)#ip access-group 33 out
```
## After Applying the ACL:

![Screenshot 5](https://github.com/user-attachments/assets/17989ec8-03d0-48b8-a2d0-9cc6c4b8d5be)

### Now this device cannot communicate with the devices on the other network!   
Due to the use of the source IP address only, this solution is not as good as it filters traffic based on only the source IP address, so the intruder can change its IP address and again gain access to the network.  

## To solve this problem we use Extended ACLs
