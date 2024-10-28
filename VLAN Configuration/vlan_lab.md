# VLAN Configuration Lab

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
![Screenshot-9](https://github.com/user-attachments/assets/1b93a80a-a7f8-4509-8a93-cf5a1c39a869)
![Screenshot-10](https://github.com/user-attachments/assets/ffee27c6-a0b2-475b-9bdb-097981a4e9ac)
