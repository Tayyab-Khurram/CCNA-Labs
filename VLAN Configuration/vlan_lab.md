# VLAN Configuration Lab

**What is  a VLAN?**
A VLAN is the process of creating virtual groups on a switch; Basically, it is just like making separate classrooms in a school. What would happen if there were no separate classrooms for each class students?
I hope you understood the concept!

This document contains the step-by-step VLAN configurations for Switch 1 and Switch 2, along with screenshots from the lab.

## Topology Overview
![Screenshot-1](https://github.com/user-attachments/assets/faed5cda-3371-4958-b502-1129564ffcb9)

## Step 1: Switch 1 Configuration
```bash
Switch>en
Switch#conf t
Switch(config)#hostname SW-A
SW-A(config)#exit
```

## Step 2: Check VTP Status and Configure VTP
![Screenshot-2](https://github.com/user-attachments/assets/bd370f0d-3c76-410d-8937-e43bc90dcfac)

```bash
SW-A#sh vtp status 
SW-A#conf t
SW-A(config)#vtp domain HOME
SW-A(config)#vtp mode Server 
SW-A(config)#exit
SW-A#sh vtp status
```
### VTP Status configured to domain HOME and Server mode
![Screenshot-3](https://github.com/user-attachments/assets/a0ad287b-ad24-4160-9003-8325aad3f6f1)

### Before making the VLANS, the devices are able to ping each other
![Screenshot-4](https://github.com/user-attachments/assets/6067e76c-f524-41fc-a00a-3dece37da02f)
![Screenshot-5](https://github.com/user-attachments/assets/ffe9d6a0-e6ec-4675-971f-ee081bb6027a)

## Step 3: Configure VLANs
```bash
SW-A#sh vlan brief
SW-A#conf t
SW-A(config)#vlan 2
SW-A(config-vlan)#name HR-Department
SW-A(config-vlan)#vlan 3
SW-A(config-vlan)#name Testing-Department
SW-A(config-vlan)#exit
```
![Screenshot-6](https://github.com/user-attachments/assets/61f90d19-9045-46d8-bcbd-89698aa14383)

## Step 4: Assign VLANs to Interfaces
```bash
SW-A#sh vlan brief
SW-A#conf t
SW-A(config)#int fa0/1
SW-A(config-if)#switchport access vlan 2
SW-A(config-if)#exit
SW-A(config)#int fa0/2
SW-A(config-if)#switchport access vlan 2
SW-A(config-if)#exit
SW-A(config)#int fa0/3
SW-A(config-if)#switchport access vlan 2
SW-A(config-if)#exit
SW-A(config)#int fa0/4
SW-A(config-if)#switchport access vlan 3
SW-A(config)#int fa0/5
SW-A(config-if)#switchport access vlan 3
SW-A(config)#int fa0/6
SW-A(config-if)#switchport access vlan 3
SW-A(config-if)#exit
SW-A(config)#exit
SW-A#sh vlan brief
```
![Screenshot-7](https://github.com/user-attachments/assets/88b1ed78-0cbe-4cb2-b65e-89da960b4835)
### After making the VLANS, the devices are not able to ping each other
![Screenshot-8](https://github.com/user-attachments/assets/5ee6e845-6bfb-46c9-b65f-48ff99349c7e)
![Screenshot-10](https://github.com/user-attachments/assets/ffee27c6-a0b2-475b-9bdb-097981a4e9ac)
### The devices within the same VLAN can ping each other but not from different VLANS
![Screenshot-9](https://github.com/user-attachments/assets/1b93a80a-a7f8-4509-8a93-cf5a1c39a869)
![Screenshot-11](https://github.com/user-attachments/assets/dd3cdc24-3ffb-481f-88a6-496b8e93eed8)

#### Suppose all the ports on the switch are assigned to some VLANs, and more devices arrive for HR and Testing Department, so we add another switch and connect the devices to them
![Screenshot 12](https://github.com/user-attachments/assets/5c71cd15-3dec-4d62-9fdb-61fdc36963b0)
![Screenshot-13](https://github.com/user-attachments/assets/ade7f77f-4af4-424e-8429-412b1a13b31f)

## Step 5: Switch 2 Configuration
```bash
Switch>en
Switch#conf t
Switch(config)#hostname SW-B
SW-A(config)#exit
```
## Step 6: Check VTP Status and Configure VTP
```bash
SW-B#sh vtp status
SW-B#conf t
SW-B(config)#vtp domain HOME
SW-B(config)#exit
SW-B#sh vtp status 
```
## Step 7: Configure VLANs
```bash
SW-B#conf t
SW-B(config)#vlan 2
SW-B(config-vlan)#name HR-Department
SW-B(config-vlan)#exit
SW-B(config)#vlan 3
SW-B(config-vlan)#name Testing-Department
SW-B(config-vlan)#exit
SW-B(config)#exit
SW-B#sh vlan brief 
```
## Step 8: Assign VLANs to Interfaces
```bash
SW-B#conf t
SW-B(config)#int fa0/1
SW-B(config-if)#switchport access vlan 2
SW-B(config-if)#exit
SW-B(config)#int fa0/2
SW-B(config-if)#switchport access vlan 2
SW-B(config-if)#exit
SW-B(config)#int fa0/3
SW-B(config-if)#switchport access vlan 3
SW-B(config-if)#exit
SW-B(config)#int fa0/4
SW-B(config-if)#switchport access vlan 3
SW-B(config-if)#exit
SW-B(config)#exit
SW-B#sh vlan brief 
```
![Screenshot-14](https://github.com/user-attachments/assets/ffc250de-680a-4221-9e6c-acda68638b4f)

### When the switches are attached to each other and the VLANs are assigned, the HR Department devices should be able to communicate with the newly added devices
![Screenshot-15](https://github.com/user-attachments/assets/d1366652-3046-453c-a7f3-ec7cb2aad6aa)
### We see that the devices are not pinging each other, But Why?
Because, The default mode for a switch port is access mode; A switch port in access mode is designed to carry traffic for only one VLAN, typically used when connecting individual devices like desktops to the network.
**We need to configure the switch port mode of the SW-A as Trunk Mode!** Now what is this Trunk Mode?
A switch port in trunk mode can carry traffic for multiple VLANs, allowing communication between different VLANs on a single link. It is used to connect devices that need to access multiple VLANs. Right?
So let's configure the switchport mode of the SW-A as trunk mode.
## Step 9: Configure Trunk Port
```bash
SW-A>en
SW-A#conf t
SW-A(config)#int fa0/7
SW-A(config-if)#switchport mode trunk
```
### After configuring the mode as trunk, the devices from different VLANS are now able to ping each other 
![Screenshot-16](https://github.com/user-attachments/assets/e492e788-d468-4a78-9b05-68d8df92c44c)
## Notes
