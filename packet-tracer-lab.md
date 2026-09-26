# Task 2.5 — Cisco Packet Tracer Implementation

# Objective
A simplified version of the proposed Meridian network design was implemented using Cisco Packet Tracer. The implementation demonstrates switching, routing, IP addressing, default gateways, DHCP where appropriate, multiple network segments and communication testing. For implementation, I use a Cisco 2911 router, Cisco 2960 switch and four PCs representing the different network segments.

## 1. Switching

A Cisco 2960 switch was used to provide Layer 2 connectivity between the network devices.

I created four VLANs to separate the network into logical segments:

|VLAN	| Network Segment |	Switch Port |
|---|---|---|
|VLAN 10 |	Corporate Users |	Fa0/1
|VLAN 20 |	Servers	| Fa0/2
|VLAN 30 |	Management |	Fa0/3
|VLAN 40 |	Guest Wi-Fi	| Fa0/4 |

The PC ports were configured as access ports which means each PC belongs to one specific VLAN.

The switch port connected to the router, GigabitEthernet0/1, was configured as a trunk. A trunk is required because one physical connection between the switch and router carries traffic belonging to all four VLANs.

The VLAN configuration was verified using: show vlan brief

Evidence: screenshots/packet-tracer-vlan-brief.png

Trunk evidence: screenshots/packet-tracer-switch-trunk.png


## 2. Routing

I used Cisco 2911 router to provide communication between the different VLANs.

Router-on-a-stick was implemented using four subinterfaces on GigabitEthernet0/0:

|Subinterface |	VLAN |	Gateway |
|---|---|---|
|G0/0.10 |	10	| 192.168.50.1
|G0/0.20 |	20 	| 192.168.50.65
|G0/0.30 |	30	| 192.168.50.129
|G0/0.40 |	40	| 192.168.50.193

Each subinterface was associated with its VLAN using 802.1Q encapsulation.

This allows the router to receive traffic from one VLAN and route it to another VLAN.

I verified the interface using: show ip interface brief

The four subinterfaces showed up/up, confirming that they were operational.

The routing table was also checked using: show ip route

The router showed connected routes for all four /26 networks.

Evidence: screenshots/packet-tracer-router-interfaces.png

Routing evidence: screenshots/packet-tracer-routing-table.png

## 3. IP Addressing

The original 192.168.50.0/24 network was divided into four /26 networks.

|Segment| Network|	Subnet Mask |	Gateway |
|---|---|---|---|
|Corporate Users |	192.168.50.0/26 |	255.255.255.192 |	192.168.50.1 |
Servers	|  192.168.50.64/26 |	255.255.255.192 |	192.168.50.65 |
Management|	192.168.50.128/26 |	255.255.255.192 |	192.168.50.129 |
Guest Wi-Fi|	192.168.50.192/26 |	255.255.255.192 |	192.168.50.193 |

The /26 subnet provides 62 usable host addresses per segment while keeping the four network groups separated.

The final device addressing included:

|Device |	Segment |	Method |	IP Address |
|PC0 |	Corporate |	DHCP |	192.168.50.2 |
|PC1 |	Servers |	Static |	192.168.50.66 |
|PC2 |	Management |	DHCP |	192.168.50.139 |
|PC3|	| Guest	| DHCP |	192.168.50.203 |

## 4. Default Gateways

Each network segment was given its own default gateway on the router.

|Network |	Default Gateway |
|---|---|
|Corporate | 	192.168.50.1 |
|Servers |	192.168.50.65 |
|Management |	192.168.50.129 |
|Guest |	192.168.50.193 |

The default gateway provides the path from a device’s local network to other networks.

For example, PC0 on the Corporate network uses 192.168.50.1 as its gateway. When PC0 needs to communicate with the Server VLAN, the traffic is sent to this gateway and the router routes it to the Server network.

PC0 successfully pinged its gateway: ping 192.168.50.1

The successful replies confirmed that the Corporate PC could reach its default gateway.


## 5. DHCP Where Appropriate

DHCP was configured on the router for the Corporate, Management and Guest networks.

DHCP automatically provides devices with an IP address, subnet mask, default gateway and DNS server.

Corporate

PC0 received:
* IP Address: 192.168.50.2
* Gateway:    192.168.50.1
* DNS:        8.8.8.8

Management

PC2 received:

* IP Address: 192.168.50.139
* Gateway:    192.168.50.129
* DNS:        8.8.8.8

Addresses 192.168.50.129–192.168.50.138 were excluded from the Management DHCP range.

Guest

PC3 received:

* IP Address: 192.168.50.203
* Gateway:    192.168.50.193
* DNS:        8.8.8.8

Addresses 192.168.50.193–192.168.50.202 were excluded from the Guest DHCP range.

Server

The Server VLAN was given a static address instead of DHCP because servers generally benefit from predictable addresses.

PC1 was configured with:

* IP Address: 192.168.50.66
* Subnet Mask: 255.255.255.192
* Gateway: 192.168.50.65
* DNS: 8.8.8.8

Evidence: screenshots/packet-tracer-server-ip.png

DHCP evidence: screenshots/packet-tracer-dhcp-management.png and screenshots/packet-tracer-dhcp-guest.png


## 6. Multiple Network Segments

The network was divided into four separate segments:

* VLAN 10 — Corporate Users
* VLAN 20 — Servers
* VLAN 30 — Management
* VLAN 40 — Guest Wi-Fi

Each VLAN has its own /26 subnet and default gateway.

This segmentation prevents the entire network from operating as one flat Layer 2 network. It also provides a foundation for applying different security policies to different groups of devices.

For example, Guest devices can later be restricted from accessing sensitive Server or Management resources, while Management devices can be given administrative access where required.

The four VLANs were verified using; show vlan brief

Evidence: screenshots/packet-tracer-vlan-brief.png


## 7. Communication Testing

Communication was tested using the ping command.

Corporate → Gateway

PC0 successfully pinged: ``` ping 192.168.50.1 ```

This confirmed connectivity between the Corporate PC and its default gateway.

Corporate → Server

PC0 successfully pinged:``` ping 192.168.50.66 ```

The successful replies demonstrated communication between the Corporate VLAN and Server VLAN through the router.

Evidence: screenshots/packet-tracer-ping-corporate-to-server.png

Corporate → Management

PC0 successfully pinged:``` ping 192.168.50.139 ```

Four successful replies were received, demonstrating communication between the Corporate and Management VLANs.

Evidence: screenshots/packet-tracer-ping-corporate-to-management.png

Corporate → Guest

PC0 also successfully pinged:``` ping 192.168.50.203 ```

This demonstrated communication between the Corporate and Guest VLANs through the router.

These tests provide evidence that the addressing, gateways, VLAN configuration, trunk connection and inter-VLAN routing are functioning correctly.


## Evidence Summary

The Packet Tracer implementation is supported by the following evidence:

|Evidence |	What it demonstrates |
|---|---|
|packet-tracer-topology.png	| Overall network design |
|packet-tracer-vlan-brief.png |	VLAN segmentation and switching |
|packet-tracer-switch-trunk.png | Trunk connection |
|packet-tracer-router-interfaces.png |	Router subinterfaces and gateways |
|packet-tracer-routing-table.png |	Routing table and connected networks |
|packet-tracer-server-ip.png |	Static server addressing |
|packet-tracer-dhcp-management.png |	DHCP addressing |
|packet-tracer-dhcp-guest.png |	DHCP addressing |
|packet-tracer-ping-corporate-to-server.png |	Inter-VLAN communication |
|packet-tracer-ping-corporate-to-management.png |	Inter-VLAN communication |

## Conclusion

The Cisco Packet Tracer implementation demonstrates all the required elements of Task 2.5: switching, routing, IP addressing, default gateways, DHCP where appropriate, multiple network segments and communication testing.

The successful IP addressing and ping tests provide evidence that the simplified Meridian network design is functioning as intended in the Packet Tracer environment.