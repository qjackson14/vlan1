<p align="center">

</p>


<h2>Video Demonstration</h2>

- ### [YouTube: Day 16 VLAN Pt. 1](https://www.youtube.com/watch?v=hv-Vmasq_xE&t=7s)

<h2>Environments and Technologies Used</h2>

- Jeremy's IT Lab Youtube Channel
- Cisco Packet Tracer
  

  
<h2>Operating Systems Used </h2>

- Cisco IOS


<h2>Step-by-Step</h2>
Step 1: Configure IP Addressing on All PCs

Configure each PC with an IP address, subnet mask, and default gateway.
The default gateway is the last usable address of each subnet.

VLAN 10 – Engineering (10.0.0.0 /26)

Subnet mask: 255.255.255.192

PC1

Open PC1 → Config

Set Default Gateway: 10.0.0.62

Select FastEthernet0

Set IP Address: 10.0.0.1

Set Subnet Mask: 255.255.255.192

PC2

Open PC2 → Config

Set Default Gateway: 10.0.0.62

Set IP Address: 10.0.0.2

Set Subnet Mask: 255.255.255.192

VLAN 20 – HR (10.0.0.64 /26)

PC3

Open PC3 → Config

Set Default Gateway: 10.0.0.126

Set IP Address: 10.0.0.65

Set Subnet Mask: 255.255.255.192

PC4

Open PC4 → Config

Set Default Gateway: 10.0.0.126

Set IP Address: 10.0.0.66

Set Subnet Mask: 255.255.255.192

VLAN 30 – Sales (10.0.0.128 /26)

PC5

Open PC5 → Config

Set Default Gateway: 10.0.0.190

Set IP Address: 10.0.0.129

Set Subnet Mask: 255.255.255.192

PC6

Open PC6 → Config

Set Default Gateway: 10.0.0.190

Set IP Address: 10.0.0.130

Set Subnet Mask: 255.255.255.192

✅ Step 1 complete

Step 2: Connect and Configure Router R1
2.1 Make Physical Connections (Straight-Through Cables)

SW1 G0/1 → R1 G0/0 (VLAN 10)

SW1 G1/1 → R1 G0/1 (VLAN 20)

SW1 G2/1 → R1 G0/2 (VLAN 30)

2.2 Configure R1 Interfaces

Open R1 → CLI

Enter privileged EXEC mode:

enable


Enter global configuration mode:

configure terminal

Configure VLAN 10 Interface
interface g0/0
ip address 10.0.0.62 255.255.255.192
no shutdown

Configure VLAN 20 Interface
interface g0/1
ip address 10.0.0.126 255.255.255.192
no shutdown

Configure VLAN 30 Interface
interface g0/2
ip address 10.0.0.190 255.255.255.192
no shutdown

Verify Configuration
do show ip interface brief


✅ Confirm all three interfaces are up/up

Step 3: Configure VLANs and Access Ports on SW1
3.1 Access the Switch CLI
enable
configure terminal

3.2 Configure Access Ports for VLAN 10
interface range g0/1, f3/1, f4/1
switchport mode access
switchport access vlan 10

3.3 Configure Access Ports for VLAN 20
interface range g1/1, f5/1, f6/1
switchport mode access
switchport access vlan 20

3.4 Configure Access Ports for VLAN 30
interface range g2/1, f7/1, f8/1
switchport mode access
switchport access vlan 30

3.5 Verify VLAN Assignment
do show vlan brief

3.6 Name the VLANs
vlan 10
name ENGINEERING

vlan 20
name HR

vlan 30
name SALES

Verify Again
do show vlan brief


✅ Step 3 complete

Step 4: Test Connectivity
4.1 Ping Between VLANs from PC1

Open PC1 → CLI

Ping PC3 (VLAN 20):

ping 10.0.0.65


Ping PC5 (VLAN 30):

ping 10.0.0.129

4.2 Observe Traffic Flow (Simulation Mode)

Packet path:

PC → SW1 → R1 → SW1 → Destination PC

Confirms inter-VLAN routing via R1

4.3 Test Broadcast Containment

From PC1, ping VLAN 10 broadcast address:

ping 10.0.0.63


Confirm the broadcast reaches only VLAN 10 devices

✅ Lab Complete


<h2>Video Demonstration</h2>

- ### [YouTube: Day 17 VLAN Pt. 2](https://www.youtube.com/watch?v=vp2hg0X9zEY&t=301s)

<h2>Environments and Technologies Used</h2>

- Jeremy's IT Lab Youtube Channel
- Cisco Packet Tracer
  

  
<h2>Operating Systems Used </h2>

- Cisco IOS


<h2>Step-by-Step</h2>


<h2>Video Demonstration</h2>

- ### [YouTube: Day 18 VLAN Pt. 3 Multilayer Switches](https://www.youtube.com/watch?v=7qTupC6ACH4)

<h2>Environments and Technologies Used</h2>

- Jeremy's IT Lab Youtube Channel
- Cisco Packet Tracer
  

  
<h2>Operating Systems Used </h2>

- Cisco IOS


<h2>Step-by-Step</h2>
