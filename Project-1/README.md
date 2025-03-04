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
- [Network Configuration](#network-configuration)
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
-	Connect the End-devices with the Switch, which are located in the different VLAN's.

<img src="SOHO Network Design.PNG" alt="SOHO Network Topology Design">

## Network Configuration 

Before Configuring anything - First, We need to Enable the Cisco Switch or Router and Open the Configure Mode. 

We can Enable the Cisco Switch or Router by applying these steps :

1. Click on the Switch/Router.
2. Choose the CLI - Command Line Interface option.
3. CLI Will Show - Would you like to enter the initial configuration dialog? [yes/no] : Type "No", then **Enter**.

       Switch>               (User EXEC Mode)

4. To Enable the Switch/Router, We use enable command. 

       Switch> enable
       Switch#               (Privileged EXEC Mode)

5. To Open the Configure Mode, We use config terminal command.

       Switch# config terminal
       Switch(config)#       (Global Configuration Mode)

### Step - 1 : Create VLANs on the Switch  

- For VLAN 10

      Switch(config)# vlan 10
      Switch(config-vlan)# name Admin/IT

- For VLAN 20

      Switch(config)# vlan 20
      Switch(config-vlan)# name Finance/HR 

- For VLAN 30  

      Switch(config)# vlan 30
      Switch(config-vlan)# name Reception/CS

### Step - 2 : Assign ports to VLANs

- For VLAN 10

      Switch(config)# vlan 10
      Switch(config-vlan)# interface range f0/1-3
      Switch(config-if-range)# switchport mode access
      Switch(config-if-range)# switchport access vlan 10

- For VLAN 20

      Switch(config)# vlan 20
      Switch(config-vlan)# interface range f0/4-6
      Switch(config-if-range)# switchport mode access
      Switch(config-if-range)# switchport access vlan 20

- For VLAN 30

      Switch(config)# vlan 30
      Switch(config-vlan)# interface range f0/7-9
      Switch(config-if-range)# switchport mode access
      Switch(config-if-range)# switchport access vlan 30

### Step - 3 : Configure router for Inter-VLAN routing

Configuring Inter-VLAN routing on the Router, We must be follow these things :

1. Each VLAN must be lie in different Subnets of a Network.

   - #### Subnetting for different VLAN's

     Base Network Provided by ISP : **192.168.1.0/24** (Network Address).

         - Base Network : 192.168.1.0/24
         - Default Subnet Mask : 255.255.255.0 (in binary 11111111. 11111111. 11111111.00000000)
         - No. of Subnet Required = 3
         - No. of Subnet = 2^n
         - No. of Subnet = 2^2 = 4 Subnet (Where, n=2) 
         - New Subnet Mask : 11111111. 11111111. 11111111.11000000 (in decimal 255.255.255.192)
         - New Network : 192.168.1.0/26
         - Block Size: 64

      |No. of Subnet |For|Network ID |Broadcast ID|Host Range|
      |:---| :----: | :----: | :----: |---:|
      |1st |VLAN 10 |192.168.1.0|192.168.1.63|192.168.1.1 - 192.168.1.62|
      |2nd |VLAN 20 |192.168.1.64|192.168.1.127|192.168.1.65 - 192.168.1.126|
      |2nd |VLAN 30 |192.168.1.128|192.168.1.191|192.168.1.129 - 192.168.1.190|
