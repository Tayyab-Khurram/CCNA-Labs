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
