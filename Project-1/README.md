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
- [Verification](#verification)
- [Conclusion](#conclusion)
- [Author](#author)
- [License](#license)
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

### Step - 1 : Requirements

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
-	Connect the End-devices to the Switch, which are located in the different VLANs.

<img src="SOHO Network Design.PNG" alt="SOHO Network Topology Design">

## Network Configuration 

Before configuring anything,  we must enable the Cisco Switch or Router and open the Configure Mode. 

We can enable the Cisco Switch or Router by applying these steps :

1. Click on the Switch/Router.
2. Choose the CLI - Command Line Interface option.
3. CLI Will Show - Would you like to enter the initial configuration dialog? [yes/no]: Type "No", then **Enter**.

       Switch>               (User EXEC Mode)

4. To Enable the Switch/Router, we use the "enable" command. 

       Switch> enable
       Switch#               (Privileged EXEC Mode)

5. We use the "configure terminal" command to open the Configure Mode.

       Switch# configure terminal
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

  To show VLANs using the "show vlan brief" command.

      Switch# sh vlan brief

     |VLAN | Name|                             Status|Ports |
     |---|----|----|---|
     |1   | default|                          active |Fa0/1, Fa0/2, Fa0/3, Fa0/4, Fa0/5, Fa0/6, Fa0/7, Fa0/8, Fa0/9, Fa0/10, Fa0/11, Fa0/12, Fa0/13, Fa0/14, Fa0/15, Fa0/16, Fa0/17, Fa0/18, Fa0/19, Fa0/20, Fa0/21, Fa0/22, Fa0/23, Fa0/24, Gig0/2|
     |10|   ADMIN/IT|                         active|    
     |20|   FINANCE/HR|                       active|    
     |30|   RECEPTION/CS|                     active|    
     |1002| fddi-default|                     active|    
     |1003| token-ring-default|               active|    
     |1004| fddinet-default|                  active|   
     |1005| trnet-default|                    active|    

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

  After assigning ports to the VLANs, again show VLANs using the "show vlan brief" command to check ports assigned to the VLANs or not.

      Switch# sh vlan brief

     |VLAN | Name|                             Status|Ports |
     |---|----|----|---|
     |1   | default|                          active |Fa0/10, Fa0/11, Fa0/12, Fa0/13, Fa0/14, Fa0/15, Fa0/16, Fa0/17, Fa0/18, Fa0/19, Fa0/20, Fa0/21, Fa0/22, Fa0/23, Fa0/24, Gig0/2|
     |10|   ADMIN/IT|                         active|    Fa0/1, Fa0/2, Fa0/3|
     |20|   FINANCE/HR|                       active|    Fa0/4, Fa0/5, Fa0/6|
     |30|   RECEPTION/CS|                     active|    Fa0/7, Fa0/8, Fa0/9|
     |1002| fddi-default|                     active|    
     |1003| token-ring-default|               active|    
     |1004| fddinet-default|                  active|   
     |1005| trnet-default|                    active|

### Step - 3 : Configure router for Inter-VLAN routing

Configuring Inter-VLAN routing on the Router, we must follow these things :

- Each VLAN must lie in a different subnet of a Network.

   - #### Subnetting for different VLANs

     Base Network Provided by ISP : **192.168.1.0/24** (Network Address).

         - Base Network : 192.168.1.0/24
         - Default Subnet Mask : 255.255.255.0 (in binary 11111111. 11111111. 11111111.00000000)
         - No. of Subnet Required = 3
         - No. of Subnet = 2^n
         - No. of Subnet = 2^2 = 4 Subnet (Where, n=2) 
         - New Subnet Mask : 11111111. 11111111. 11111111.11000000 (in decimal 255.255.255.192)
         - New Network : 192.168.1.0/26
         - Block Size: 64

      |No. of Subnet |For|Network ID / Prefix |Broadcast ID |Host Range|
      |---|----|----|----|---|
      |1st |VLAN 10 |192.168.1.0/26|192.168.1.63|192.168.1.1 - 192.168.1.62|
      |2nd |VLAN 20 |192.168.1.64/26|192.168.1.127|192.168.1.65 - 192.168.1.126|
      |2nd |VLAN 30 |192.168.1.128/26|192.168.1.191|192.168.1.129 - 192.168.1.190|


- One Port of the Switch should be made a Trunk Port, that port is connected to the Router. Except those port that are connected to the different VLANs.

      Switch(config)# interface gigabitEthernet0/1
      Switch(config-if)# switchport mode trunk

  To show Trunk using the "show interface trunk" command.

      Switch# show interface trunk

     |Port|        Mode|         Encapsulation|  Status|        Native vlan|
     |---|----|----|----|:---:|
     |Gig0/1|      on|           802.1q|         trunking|      1|
     
     |Port|Vlans allowed on trunk|
     |---|---|
     |Gig0/1|      1-1005|

     |Port|       Vlans allowed and active in management domain|
     |---|---|
     |Gig0/1|      1,10,20,30|

     |Port|        Vlans in spanning tree forwarding state and not pruned|
     |---|---|
     |Gig0/1|      1,10,20,30|

- We have to create the Sub-Interfaces for each VLAN and Assign the different IP addresses for each Sub-Interface.

   - Before, Create Sub-Interface, we need to enable the Router and Open Config Mode. 
    
         Router> enable
         Router# configure terminal
         Router(config)#

   - After that, we need to UP that interface of the Router, which interface is connected to the Switch by using the "no shutdown" command.  

         Router(config)# interface gigabitEthernet0/0
         Router(config-if)# no shutdown

   Now we can create Sub-Iinterfaces -
   - Sub-Interface for VLAN 10
      
         Router(config)# int gigabitEthernet0/0.10
         Router(config-subif)# encapsulation dot1q 10
         Router(config-subif)# ip address 192.168.1.1 255.255.255.192

   - Sub-Interface for VLAN 20
      
         Router(config)# int gigabitEthernet0/0.20
         Router(config-subif)# encapsulation dot1q 20
         Router(config-subif)# ip address 192.168.1.65 255.255.255.192

   - Sub-Interface for VLAN 30
      
         Router(config)# int gigabitEthernet0/0.30
         Router(config-subif)# encapsulation dot1q 30
         Router(config-subif)# ip address 192.168.1.129 255.255.255.192

     To show Sub-Interfaces using "show ip interface brief" command.

         Router# sh ip int brief

     |Interface|              IP-Address|      OK? Method Status|                Protocol|
     |---|----|----|---| 
     |GigabitEthernet0/0|     unassigned|      YES unset  up|                    up| 
     |GigabitEthernet0/0.10|  192.168.1.1|     YES manual up|                    up| 
     |GigabitEthernet0/0.20|  192.168.1.65|    YES manual up|                    up| 
     |GigabitEthernet0/0.30|  192.168.1.129|   YES manual up|                    up| 
     |GigabitEthernet0/1|     unassigned|      YES unset  administratively down| down| 
     |GigabitEthernet0/2|     unassigned|      YES unset  administratively down| down| 
     |Vlan1|

-  Each End Device in the different VLANs must use the same IP address as a Gateway-IP, which is already assigned to the respective Sub-Interfaces. So that every VLAN can communicate with each other by applying Inter-VLAN Routing Protocol.

    - For VLAN 10

       Every End-Device in the VLAN 10 must use **192.168.1.1** as a Default Gateway-IP.

    - For VLAN 20

       Every End-Device in the VLAN 20 must use **192.168.1.65** as a Default Gateway-IP.

    - For VLAN 30

       Every End-Device in the VLAN 30 must use **192.168.1.129** as a Default Gateway-IP.

Now Inter-VLAN Routing process is completed.

To show Inter-VLAN Routing using "show ip route" command.

    Router# sh ip route


Codes: 

      L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
      D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
      N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
      E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
      i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
      * - candidate default, U - per-user static route, o - ODR
      P - periodic downloaded static route

      Gateway of last resort is not set

      192.168.1.0/24 is variably subnetted, 6 subnets, 2 masks
      C       192.168.1.0/26 is directly connected, GigabitEthernet0/0.10
      L       192.168.1.1/32 is directly connected, GigabitEthernet0/0.10
      C       192.168.1.64/26 is directly connected, GigabitEthernet0/0.20
      L       192.168.1.65/32 is directly connected, GigabitEthernet0/0.20
      C       192.168.1.128/26 is directly connected, GigabitEthernet0/0.30
      L       192.168.1.129/32 is directly connected, GigabitEthernet0/0.30

### Step - 4 : Set up DHCP for Automatic IP assignment for every End-Device of the Departments.

  - For Admin/IT Department

        Router(config)# ip dhcp pool Admin-Pool
        Router(config-dhcp)# network 192.168.1.0 255.255.255.192
        Router(config-dhcp)# default-router 192.168.1.1
        Router(config-dhcp)# dns-server 192.168.1.1
        Router(config-dhcp)# domain-name Admin.com

  - For Finance/HR Department

        Router(config)# ip dhcp pool Finance-Pool
        Router(config-dhcp)# network 192.168.1.64 255.255.255.192
        Router(config-dhcp)# default-router 192.168.1.65
        Router(config-dhcp)# dns-server 192.168.1.65
        Router(config-dhcp)# domain-name Finance.com

  - For Reception/CS Department

        Router(config)# ip dhcp pool Reception-Pool
        Router(config-dhcp)# network 192.168.1.128 255.255.255.192
        Router(config-dhcp)# default-router 192.168.1.129
        Router(config-dhcp)# dns-server 192.168.1.129
        Router(config-dhcp)# domain-name Reception.com

### Step - 5 : Configure wireless SSIDs with WPA2-PSK for each Department.
Configure Wireless so that each Host/End-Device can connect their Devices through Wireless Media. Where each Host can put the SSIDs(Wifi-Name) with WPA2-PSK(Wifi-Password) in their Devices to get an Internet Connection through Wireless.  

  - For Admin/IT Department

    SSID : Admin-WiFi (Mapped to VLAN 10)

    WPA2-PSK : Admin@123

  - For Finance/HR Department

    SSID : Finance-WiFi (Mapped to VLAN 20)

    WPA2-PSK : Finance@123

  - For Reception/CS Department

    SSID : Reception-WiFi (Mapped to VLAN 30)

    WPA2-PSK : Reception@123

## Verification
 
### Verify Communication across VLANs using ping

- Ping **Laptop0** of VLAN 10 to **PC1** of VLAN 20

      Cisco Packet Tracer PC Command Line 1.0
      C:\>ping 192.168.1.67
      
      Pinging 192.168.1.67 with 32 bytes of data:
      
      Reply from 192.168.1.67: bytes=32 time=32ms TTL=127
      Reply from 192.168.1.67: bytes=32 time=31ms TTL=127
      Reply from 192.168.1.67: bytes=32 time=36ms TTL=127
      
      Ping statistics for 192.168.1.67:
          Packets: Sent = 4, Received = 3, Lost = 1 (25% loss),
      Approximate round trip times in milli-seconds:
          Minimum = 26ms, Maximum = 48ms, Average = 37ms

- Ping **Laptop0** of VLAN 10 to **Laptop2** of VLAN 30

      Cisco Packet Tracer PC Command Line 1.0
      C:\>ping 192.168.1.132
      
      Pinging 192.168.1.132 with 32 bytes of data:
      
      Reply from 192.168.1.132: bytes=32 time=38ms TTL=127
      Reply from 192.168.1.132: bytes=32 time=66ms TTL=127
      Reply from 192.168.1.132: bytes=32 time=62ms TTL=127
      
      Ping statistics for 192.168.1.132:
          Packets: Sent = 4, Received = 3, Lost = 1 (25% loss),
      Approximate round trip times in milli-seconds:
          Minimum = 38ms, Maximum = 66ms, Average = 55ms

- Ping **Laptop1** of VLAN 20 to **PC0** of VLAN 10

      Cisco Packet Tracer PC Command Line 1.0
      C:\>ping 192.168.1.3
      
      Pinging 192.168.1.3 with 32 bytes of data:
      
      Reply from 192.168.1.3: bytes=32 time=46ms TTL=127
      Reply from 192.168.1.3: bytes=32 time=32ms TTL=127
      Reply from 192.168.1.3: bytes=32 time=32ms TTL=127
      
      Ping statistics for 192.168.1.3:
          Packets: Sent = 4, Received = 3, Lost = 1 (25% loss),
      Approximate round trip times in milli-seconds:
          Minimum = 32ms, Maximum = 46ms, Average = 36ms

- Ping **Laptop1** of VLAN 20 to **PC2** of VLAN 30

      Cisco Packet Tracer PC Command Line 1.0
      C:\>ping 192.168.1.130
      
      Pinging 192.168.1.130 with 32 bytes of data:
      
      Reply from 192.168.1.130: bytes=32 time=73ms TTL=127
      Reply from 192.168.1.130: bytes=32 time=32ms TTL=127
      Reply from 192.168.1.130: bytes=32 time=33ms TTL=127
      
      Ping statistics for 192.168.1.130:
          Packets: Sent = 4, Received = 3, Lost = 1 (25% loss),
      Approximate round trip times in milli-seconds:
          Minimum = 32ms, Maximum = 73ms, Average = 46ms

- Ping **Laptop2** of VLAN 30 to **Smartphone0** of VLAN 10

      Cisco Packet Tracer PC Command Line 1.0
      C:\>ping 192.168.1.4
      
      Pinging 192.168.1.4 with 32 bytes of data:
      
      Reply from 192.168.1.4: bytes=32 time=61ms TTL=127
      Reply from 192.168.1.4: bytes=32 time=46ms TTL=127
      Reply from 192.168.1.4: bytes=32 time=73ms TTL=127
      
      Ping statistics for 192.168.1.4:
          Packets: Sent = 4, Received = 3, Lost = 1 (25% loss),
      Approximate round trip times in milli-seconds:
          Minimum = 46ms, Maximum = 73ms, Average = 60ms

- Ping **Laptop2** of VLAN 30 to **Printer1** of VLAN 20

      Cisco Packet Tracer PC Command Line 1.0
      C:\>ping 192.168.1.66
      
      Pinging 192.168.1.66 with 32 bytes of data:
      
      Reply from 192.168.1.66: bytes=32 time=25ms TTL=127
      Reply from 192.168.1.66: bytes=32 time=8ms TTL=127
      Reply from 192.168.1.66: bytes=32 time=16ms TTL=127
      Reply from 192.168.1.66: bytes=32 time=40ms TTL=127
      
      Ping statistics for 192.168.1.66:
          Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
      Approximate round trip times in milli-seconds:
          Minimum = 8ms, Maximum = 40ms, Average = 22ms

## Conclusion

This project successfully sets up a small business network with VLANs, wireless connectivity, DHCP, and inter-VLAN communication. The network is scalable and can be expanded with additional features as needed.

## Author

[Suajit Sen](https://github.com/ss-invention)

## License

[MIT](https://choosealicense.com/licenses/mit/)

## Contributing

Feel free to contribute to this project by creating pull requests or reporting issues.

