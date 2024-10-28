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
