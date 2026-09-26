# Task 2.6 — Network Segmentation Policy

## 1. Why Meridian Should Not Keep All Devices on One Network
Meridian should use network segmentation instead of placing all devices on one network. The network is divided into four logical segments: Corporate Users, Servers, Management, and Guest Wi-Fi.

## 1. Network Segmentation
Segmentation separates different types of devices into different networks. Meridian uses four /26 networks:
* Corporate Users — 192.168.50.0/26
* Servers — 192.168.50.64/26
* Management — 192.168.50.128/26
* Guest Wi-Fi — 192.168.50.192/26

The router/firewall controls traffic between these networks.

## 2. Security
Segmentation limits how far a security incident can spread. For example, a guest device should not have direct access to Meridian’s internal servers or management interfaces. Traffic between networks should therefore be controlled using firewall rules or access control lists (ACLs).

## 3. Performance
Separating the network reduces unnecessary broadcast traffic within each network. It also makes it easier to identify and troubleshoot network problems because different groups of devices are separated into their own segments.

## 4. Administrative Separation
Management devices such as the router, managed switch, and wireless access points should be placed in the Management network. This prevents ordinary users and guests from directly accessing network administration interfaces.

## 5. Guest Access
Guest Wi-Fi users should have Internet access without having access to Meridian’s internal resources. This protects corporate computers, servers, and management devices from unauthorized guest access.

## 6. Server Protection
Servers contain services and data that are important to the organization. Corporate users should only be allowed to access the server services they require. Servers should not be allowed to initiate unnecessary connections to employee computers.

## 7. Management Interfaces
Only authorized management systems should be able to access network administration interfaces. Corporate and guest devices may use the router as their default gateway for permitted network traffice but they dhould not have access to router's management interfaces.

## 8. Traffic Policy
The router/firewall will route traffic between the four network segments. Access between segments will be controlled according to business requirements and security needs.

|Source |	Destination |	Decision |	Justification |
|---|---|---|---|
|Guest Wi-Fi |	Servers |	Deny |	Guest devices should not access internal servers or company data. |
|Guest Wi-Fi |	Corporate |	Deny |	Prevent guest devices from accessing employee systems. |
|Guest Wi-Fi |	Management interfaces |	Deny |	Guests should not be able to administer network devices. |
|Guest Wi-Fi |	Internet |	Allow |	Guests require normal Internet access. |
|Corporate Users |	Servers |	Allow | required services	Employees need access to approved company services hosted on servers. |
|Corporate Users |	Management interfaces |	Deny |	Normal users do not need to administer network infrastructure.|
|Management |	Servers |	Allow |	Authorized administrators need to manage and maintain servers.|
|Management |	Network devices |	Allow |	Required for administration of routers, switches, and wireless access points. |
|Servers |	Corporate Users |	Deny  by default	Servers should not initiate unnecessary connections to employee devices.| Required responses or approved services remain allowed. |
|Servers |	Management |	Allow  required management traffic |	Required for monitoring and administration.|

## Gateway Access
Corporate and Guest devices will continue to use the router as their default gateway, as configured in Packet Tracer. This allows them to send traffic to permitted destinations and, where appropriate, the Internet. However, using the router as a gateway is different from having permission to access its management interface. Management access should be restricted to authorized devices in the Management network.

## Overall Policy
The general principle is allow required business traffic and deny unnecessary access. This keeps the network functional while limiting unnecessary communication between Corporate, Servers, Management, and Guest networks.


## 9. Recommendation
Meridian should keep the four logical network segments rather than placing all devices on one network. The router/firewall should enforce the traffic policy between the segments. Access should be based on what each device or user needs to perform their role, with unnecessary communication denied by default.

This approach provides better security, administrative control, and network organization while still allowing legitimate business communication.


