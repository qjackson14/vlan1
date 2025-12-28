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
<b>Step 1:</b> Configure IP Addressing on PCs

Default gateway = last usable address in each subnet

VLAN 10 – Engineering (10.0.0.0/26)

- PC1

IP Address: 10.0.0.1

Subnet Mask: 255.255.255.192

Default Gateway: 10.0.0.62

- PC2

IP Address: 10.0.0.2

Subnet Mask: 255.255.255.192

Default Gateway: 10.0.0.62

VLAN 20 – HR (10.0.0.64/26)

- PC3

IP Address: 10.0.0.65

Subnet Mask: 255.255.255.192

Default Gateway: 10.0.0.126

- PC4

IP Address: 10.0.0.66

Subnet Mask: 255.255.255.192

Default Gateway: 10.0.0.126

VLAN 30 – Sales (10.0.0.128/26)

- PC5

IP Address: 10.0.0.129

Subnet Mask: 255.255.255.192

Default Gateway: 10.0.0.190

- PC6

IP Address: 10.0.0.130

Subnet Mask: 255.255.255.192

Default Gateway: 10.0.0.190

<b>Step 2:</b> Connect and Configure Router R1
Physical Connections (Straight-Through)

SW1 G0/1 → R1 G0/0 (VLAN 10)

SW1 G1/1 → R1 G0/1 (VLAN 20)

SW1 G2/1 → R1 G0/2 (VLAN 30)

R1 Configuration
enable
configure terminal

interface g0/0
 ip address 10.0.0.62 255.255.255.192
 no shutdown

interface g0/1
 ip address 10.0.0.126 255.255.255.192
 no shutdown

interface g0/2
 ip address 10.0.0.190 255.255.255.192
 no shutdown

do show ip interface brief

Step 3: Configure VLANs and Access Ports on SW1
Access Switch CLI
enable
configure terminal

VLAN 10 – Engineering
interface range g0/1, f3/1, f4/1
 switchport mode access
 switchport access vlan 10

VLAN 20 – HR
interface range g1/1, f5/1, f6/1
 switchport mode access
 switchport access vlan 20

VLAN 30 – Sales
interface range g2/1, f7/1, f8/1
 switchport mode access
 switchport access vlan 30

Name VLANs
vlan 10
 name ENGINEERING

vlan 20
 name HR

vlan 30
 name SALES

Verify VLAN Configuration
do show vlan brief

Step 4: Test Connectivity
Inter-VLAN Ping Tests (from PC1)
ping 10.0.0.65
ping 10.0.0.129

Broadcast Test (VLAN 10)
ping 10.0.0.63


Broadcast traffic stays within VLAN 10


<h2>Video Demonstration</h2>

- ### [YouTube: Day 17 VLAN Pt. 2](https://www.youtube.com/watch?v=vp2hg0X9zEY&t=301s)

<h2>Environments and Technologies Used</h2>

- Jeremy's IT Lab Youtube Channel
- Cisco Packet Tracer
  

  
<h2>Operating Systems Used </h2>

- Cisco IOS


<h2>Step-by-Step</h2>
<b>Step 1:</b> 
- Plan the VLANs

- VLAN 10 → Engineering

- VLAN 20 → HR

- VLAN 30 → Sales

Decide:

Which VLANs exist on each switch

Which VLANs must cross trunk links

Step 2: Create VLANs on the Switches

Perform on each switch that needs the VLANs.

enable
configure terminal

vlan 10
 name ENGINEERING

vlan 20
 name HR

vlan 30
 name SALES


Verify:

show vlan brief

Step 3: Configure Access Ports

Assign end-device ports to the correct VLAN.

Example (VLAN 10)
interface range f0/1, f0/2
 switchport mode access
 switchport access vlan 10


Repeat for VLAN 20 and VLAN 30 as needed.

Step 4: Configure Trunk Ports Between Switches
4.1 Enter Interface Configuration
interface g0/0

4.2 (If Required) Set Encapsulation

Only required on switches that support both ISL and 802.1Q

switchport trunk encapsulation dot1q

4.3 Enable Trunking
switchport mode trunk

Step 5: Limit Allowed VLANs on the Trunk

Allow only required VLANs for security and performance.

switchport trunk allowed vlan 10,30


Verify:

show interfaces trunk

Step 6: Change the Native VLAN (Best Practice)

Use an unused VLAN

Must match on both ends of the trunk

switchport trunk native vlan 1001

Step 7: Configure the Switch Port Connected to the Router

The switch port connected to the router must be a trunk.

interface g0/1
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30
 switchport trunk native vlan 1001


Verify:

show interfaces trunk

Step 8: Enable the Router Interface

Router interfaces are shutdown by default.

enable
configure terminal

interface g0/0
 no shutdown

Step 9: Configure Router-on-a-Stick Subinterfaces

Create one subinterface per VLAN.

VLAN 10
interface g0/0.10
 encapsulation dot1q 10
 ip address <VLAN10-Gateway-IP> <Subnet-Mask>

VLAN 20
interface g0/0.20
 encapsulation dot1q 20
 ip address <VLAN20-Gateway-IP> <Subnet-Mask>

VLAN 30
interface g0/0.30
 encapsulation dot1q 30
 ip address <VLAN30-Gateway-IP> <Subnet-Mask>


💡 Best practice: match subinterface number to VLAN number

Step 10: Verify Router Configuration
show ip interface brief
show ip route


Confirm:

Subinterfaces are up

Routes are connected (C) and local (L)

Step 11: Configure End Devices

On each PC:

Assign IP address

Assign subnet mask

Set default gateway to the router subinterface IP for that VLAN

Step 12: Test Connectivity

From a PC:

ping <same-VLAN-host>
ping <different-VLAN-host>


Expected:

Same VLAN → works

Different VLAN → works via router

Step 13: Final Verification Checklist

 VLANs exist on switches

 Access ports assigned correctly

 Trunk ports enabled

 Allowed VLANs restricted

 Native VLAN matches

<h2>Video Demonstration</h2>

- ### [YouTube: Day 18 VLAN Pt. 3 Multilayer Switches](https://www.youtube.com/watch?v=7qTupC6ACH4)

<h2>Environments and Technologies Used</h2>

- Jeremy's IT Lab Youtube Channel
- Cisco Packet Tracer
  

  
<h2>Operating Systems Used </h2>

- Cisco IOS


<h2>Step-by-Step</h2>
