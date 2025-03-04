## Project Tittle and Description : SOHO (Small Office Home Office) Network Design and Configuration on Cisco Paket Tracer.

This Project involves Designing and Implementing a Small Network for a Company using CISCO products. The network is structured to meet the following requirements:

    1. One router and one switch to be used (all CISCO products).

    2. 3 departments (Admin/IT, Finance/HR and Reception/CS). 

    3. Each department is required to be in different VLANS. 

    4. Each department is required to have wireless network for the users. 

    5. Host devices in the network are required to obtain IPv4 address automatically. 

    6. Devices in all the departments are required to communicate with each other. 

**Note:** Assume the ISP gave out a base network of **192.168.1.0**, you as the young network engineer who has been hired, design and implement a network considering the above requirements.


## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [Network Design](#network-design)
- [Implementation](#implementation)
- [Author](#author)
- [License](#license)
- [Conclusion](#conclusion)
- [Contributing](#contributing)

## Installation
To run this file ([ SOHO Network Design Project.pkt ](SOHO%20Network%20Design%20Project.pkt)), We need a Network Simulation Software Tool - **Cisco Packet Tracer**. 

Click [here](https://archive.org/download/cpt822/CiscoPacketTracer822_64bit_setup_signed.exe) to download the **Cisco Packet Tracer** software tool (for Windows OS).

Click [here](https://archive.org/download/cpt822/CiscoPacketTracer822_amd64_signed.deb) to download the **Cisco Packet Tracer** software tool (for Linux OS).

Click [here](https://archive.org/download/cpt822/CiscoPacketTracer822_setup_mac_signed.dmg) to download the **Cisco Packet Tracer** software tool (for Mac OS).

## Usage
This network is designed for:
-	Efficient department segmentation using VLANs
-	Seamless inter-department communication
-	Secure wireless connectivity for users
-	Automatic IP allocation through DHCP

## Network Design / Topology Design

### Step - 1 : Reruirements

-	Cisco Router (1 unit)
-   Cisco Switch (1 unit)
-   Access Points (APs) for wireless networks
-   Computers and mobile devices
-   Ethernet cables


### Step - 2 : Set Up
-	Connect the Router to the Switch.
-   Create VLANs for 3 departments.
    - VLAN 10 (for Admin/IT)
    - VLAN 20 (for Finance/HR)
    - VLAN 30 (for Reception/CS)
-	Connect the End-devices with the Switch, which are under the different VLAN's.

<img src="SOHO Network Design.PNG" alt="SOHO Network Topology Design">

## Network Connectivity

### Step - 1 : Subnetting for different VLAN's

Base Network Provided by ISP : **192.168.1.0/24** (Network Address).

    - Base Network : 192.168.1.0
    - Default Subnet Mask : 255.255.255.0 (in binary 11111111. 11111111. 11111111.00000000)
    - No. of Subnet Required = 3
    - No. of Subnet = 2^n
    - No. of Subnet = 2^2 = 4 Subnet (Where, n=2) 
    - New Subnet Mask : 11111111. 11111111. 11111111.11000000 (in decimal 255.255.255.192)
    - Block Size: 64


- **1st Subnet for VLAN 10 (depertment - Admin/IT)**
    - Network-Id : 192.168.1.0/26
    - Broadcast-Id : 192.168.1.63
    - Host-Range : 192.168.1.1 - 192.168.1.62

- **2nd Subnet for VLAN 20 (depertment - Finance/HR)**
    - Network-Id : 192.168.1.64/26
    - Broadcast-Id : 192.168.1.127
    - Host-Range : 192.168.1.65 - 192.168.1.126
    
- **3rd Subnet for VLAN 30 (depertment - Reception/CS)**
    - Network-Id : 192.168.1.128/26
    - Broadcast-Id : 192.168.1.191
    - Host-Range : 192.168.1.129 - 192.168.1.190
