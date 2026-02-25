# intervlan

Inter-vlan Routing

In this lab I play around with configuring inter-vlan routing. This would help with forwarding traffic at the layer 3 level between vlans because devices in separate vlans cannot communicate directly. 

 <img width="747" height="461" alt="image" src="https://github.com/user-attachments/assets/64db95a0-ca68-4d07-84b3-ce12985090cc" />

Router Configuration 
En
config t
hostname Router_A
service password-encryption
enable secret cisco
int g0/1
no shut
int g0/1.1
encap dot1q 1
ip add 172.16.1.100 255.255.255.0
int g0/1.5
encap dot1q 5
ip add 172.16.5.100 255.255.255.0
int g0/1.10
encap dot1q 10
ip add 172.16.10.100 255.255.255.0
int g0/1.15
encap dot1q 15
ip add 172.16.15.100 255.255.255.0
int g0/1.20
encap dot1q 20
ip add 172.16.20.100 255.255.255.0
int g0/1.25
encap dot1q 25
ip add 172.16.25.100 255.255.255.0
end
copy run start
After I viewed my changes by using the command sh ip int brief on the router

 <img width="536" height="544" alt="image" src="https://github.com/user-attachments/assets/43c709e5-92f9-4cbb-92e7-0e66f14f60d2" />

I’m going to set up my other switches and then view the setting changes using the sh vlan command on all switches
SwitchA configurations
en
config t
hostname Switch_A
ip default-gateway 172.16.25.100
vlan 5 
name dept1
vlan 10
name dept2
vlan 15
name dept3
vlan 20
name dept4
vlan 25
name management
vlan 99
name null
int vlan 25
ip add 172.16.25.51 255.255.255.0
no shut
int f0/24
switchport trunk encap dot1q
switchport mode trunk
int f0/21
switchport trunk encap dot1q
switchport mode trunk
int f0/5
switchport mode access 
switchport access vlan 5
int f0/10
switchport mode access 
switchport access vlan 10
int f0/15
switchport mode access 
switchport access vlan 15
int f0/20
switchport mode access 
switchport access vlan 20
end
copy run start

 <img width="510" height="524" alt="image" src="https://github.com/user-attachments/assets/d7ac5657-a0d1-4746-aade-4da2e242e52c" />

SwitchB configurations
en
config t
hostname Switch_B
ip default-gateway 172.16.25.100
vlan 5 
name dept1
vlan 10
name dept2
vlan 15
name dept3
vlan 20
name dept4
vlan 25
name management
vlan 99
name null
int vlan 25
ip add 172.16.25.50 255.255.255.0
no shut
int f0/24
switchport trunk encap dot1q
switchport mode trunk
int f0/21
switchport trunk encap dot1q
switchport mode trunk
int f0/5
switchport mode access 
switchport access vlan 5
int f0/10
switchport mode access 
switchport access vlan 10
int f0/15
switchport mode access 
switchport access vlan 15
int f0/20
switchport mode access 
switchport access vlan 20
end
copy run start

 <img width="500" height="532" alt="image" src="https://github.com/user-attachments/assets/863a7bd6-bae7-4a7f-ad47-899cc59b0952" />

SwitchC configurations
en
config t
hostname Switch_C
ip default-gateway 172.16.25.100
vlan 5 
name dept1
vlan 10
name dept2
vlan 15
name dept3
vlan 20
name dept4
vlan 25
name management
vlan 99
name null
int vlan 25
ip add 172.16.25.52 255.255.255.0
no shut
int f0/24
switchport trunk encap dot1q
switchport mode trunk
int f0/22
switchport trunk encap dot1q
switchport mode trunk
int f0/5
switchport mode access 
switchport access vlan 5
int f0/10
switchport mode access 
switchport access vlan 10
int f0/15
switchport mode access 
switchport access vlan 15
int f0/20
switchport mode access 
switchport access vlan 20
end
copy run start

 <img width="476" height="543" alt="image" src="https://github.com/user-attachments/assets/92ac0695-a4c1-4898-bd07-ba609de2f8f7" />

Now using the sh trunk command I would get an overview on all the switches.
SwitchA

 <img width="611" height="463" alt="image" src="https://github.com/user-attachments/assets/88777d38-509b-426a-9771-7fef4a8ab43c" />

SwitchB

 <img width="764" height="505" alt="image" src="https://github.com/user-attachments/assets/05f9581c-2b2b-41f3-bd84-f3016d0492b2" />

SwitchC

 <img width="762" height="542" alt="image" src="https://github.com/user-attachments/assets/056811f1-6ff8-4592-8e07-eb6453c81662" />

Next I would view if the DHCP server is working by assigning Ips to the various nodes connected on the network. 

 <img width="542" height="570" alt="image" src="https://github.com/user-attachments/assets/08906f7e-83ad-4576-a5d4-e401d9fe6574" />

 <img width="616" height="607" alt="image" src="https://github.com/user-attachments/assets/73b6df67-76b4-442a-8c9d-0e513309d3a7" />

 <img width="619" height="628" alt="image" src="https://github.com/user-attachments/assets/360c3279-a0cd-4ebf-bb9d-3c5f454ad00e" />

 <img width="584" height="649" alt="image" src="https://github.com/user-attachments/assets/7217f3a4-5299-4152-85c7-7316383553aa" />

 <img width="550" height="619" alt="image" src="https://github.com/user-attachments/assets/b4adc812-f88d-47f6-941f-e2154c0af39e" />

 <img width="638" height="617" alt="image" src="https://github.com/user-attachments/assets/09a44ff8-bc5e-4ce0-ac22-860d4b00ccaa" />

<img width="572" height="576" alt="image" src="https://github.com/user-attachments/assets/481894e6-7621-41ef-b1bd-5a865ba886e4" />

Would test connectivity between 2 devices on different vlans by using the ping command. 
 
<img width="948" height="468" alt="image" src="https://github.com/user-attachments/assets/5cf0b822-114e-41a1-ad27-718baa4efae4" />

