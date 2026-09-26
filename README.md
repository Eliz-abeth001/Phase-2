# PROJECT TITLE: Meridian Technologies Infrastructure Stabilisation & Security Improvement Project.

# Phase 2: Meridian- Network Architecture & Troubleshooting

## Project Overview
This project focuses on analysing, redesigning, implementing and troubleshooting Meridian’s network infrastructure. The existing flat network was reviewed and a structured network architecture was developed to improve organisation, communication and network security.

The project covers network investigation, IP addressing and subnetting, network design, segmentation, Cisco Packet Tracer implementation, packet analysis and troubleshooting.

### Project Tasks

* Network Baseline — Investigated the existing network configuration, including IPv4 addressing, subnet mask, gateway, DHCP, DNS and connectivity.

* Browser Request Explanation — Explained the network processes involved when accessing a website, including DNS, ARP, MAC addresses, routing, NAT, TCP, TLS and HTTPS.

* IP Addressing Plan — Designed the 192.168.50.0/24 network and divided it into four /26 subnets for Corporate Users, Servers, Management and Guest Wi-Fi.

* Network Design — Developed the proposed logical network architecture and supporting design decisions.

* Segmentation Policy — Defined communication and access requirements between the different network segments.

* Packet Tracer Lab — Implemented and tested a simplified version of the proposed network using VLANs, trunking, inter-VLAN routing, DHCP, static addressing and connectivity testing.

* Wireshark Analysis — Analysed captured network traffic to understand and verify network communication.

* Network Troubleshooting — Applied structured troubleshooting methods to identify and investigate network connectivity issues.

## Network Segments

|Network |	Subnet |	Gateway |
|---|---|---|
|Corporate Users |	192.168.50.0/26 |	192.168.50.1
|Servers |	192.168.50.64/26 |	192.168.50.65
|Management |	192.168.50.128/26 |	192.168.50.129
|Guest Wi-Fi |	192.168.50.192/26 |	192.168.50.193


The diagrams/ folder contains the network diagram, while the screenshots/ folder contains supporting evidence from the configuration, testing and analysis activities.

### Conclusion
This Phase 2 project demonstrates the process of assessing a network, designing an improved architecture, implementing key networking technologies, analysing network traffic, and troubleshooting connectivity. The resulting design provides a more structured and manageable foundation for Meridian’s network.