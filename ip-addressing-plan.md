# Task 2.3 — Meridian Network Redesign
# 1. Allocated Network

Meridian has been allocated: 192.168.50.0/24

The /24 means that the first 24 bits are used for the network portion, leaving 8 bits for hosts.

The subnet mask is: 255.255.255.0

A /24 network contains: 2⁸ = 256 total addresses

However, two addresses are normally reserved:
* One for the network address
* One for the broadcast address

Therefore: 256 − 2 = 254 usable host addresses

# 2. Requirement for Four Networks

Meridian needs four separate logical networks:

- Corporate Users
- Servers
- Management
- Guest Wi-Fi

I need to divide the original /24 network into 4 smaller networks.

To create 4 subnets, I would borrow 2 bits: 2bits

2² = 4 subnets

Therefore:

/24 + 2 bits = /26

The new subnet mask is: 255.255.255.192 because the last octet in binary is: 192 = 11000000

Therefore, the /26 mask is: 11111111.11111111.11111111.11000000

There are 26 network bits and 6 host bits.

# 3. Number of Addresses Per Network

With /26, we have 6 host bits remaining.

Therefore: 2⁶ = 64 total addresses per subnet

Two addresses are reserved:
* Network address
* Broadcast address

So: 64 − 2 = 62 usable host addresses per network. This gives each Meridian network 62 usable addresses

## Why /26 Was Chosen

The original network was: 192.168.50.0/24

Meridian needs four logical networks.

Borrowing two host bits creates four /26 subnets:

2² = 4

Each /26 provides: 64 total addresses and: 62 usable host addresses

Using /26 makes configuration and troubleshooting easier because every network uses the same subnet size and subnet mask.

# 4. Addressing Plan

|Network |	Network Address |	Usable Range |	Gateway |	Broadcast |	Devices	| Method |
|---|---|---|---|---|---|---|
|Corporate |	192.168.50.0/26 |	.1 - .62 |	.1 |	.63 |	40 |	DHCP |
|Servers |	192.168.50.64/26 |	 .65 - .126 |	 65 |  .127 |	10 |   Static |
|Management |	192.168.50.128/26 |	.129 - .190	| .129 |	.191 |	10 |	DHCP |
|Guest Wi-Fi |	192.168.50.192/26 |	.193 - .254	| .193 |	.255 |	30 |	DHCP |

- Subnet Mask: 255.255.255.192
- Usable Addresses per Subnet: 62

  The expected device numbers are based on Meridian’s current infrastructure and planned growth. The Corporate network allows for the 28 Windows computers currently listed, with additional capacity for employee devices. The Servers network allows for the 2 existing Ubuntu servers and future servers. The Management network covers the router, managed switch, wireless access points, and future management devices. Guest Wi-Fi is allocated additional capacity for visitors and temporary devices.

Each /26 subnet provides 62 usable addresses, allowing room for future growth.

# 5. Corporate Users Network

Network assigned: 192.168.50.0/26

## Address information
* Network address: 192.168.50.0
* CIDR: /26
* Subnet mask: 255.255.255.192
* Usable range: 192.168.50.1 – 192.168.50.62
* Default gateway: 192.168.50.1
* Broadcast: 192.168.50.63
* Usable addresses: 62
* Expected devices: approximately 40

## Addressing decision
DHCP will be used for Corporate Users. Corporate computers can change frequently as employees join, leave or move between workstations. DHCP automatically provides the required IP configuration and reduces manual configuration.

## Growth capacity
There are 62 usable addresses and approximately 40 expected devices.

Therefore: 62 − 40 = 22 addresses available for growth. This means the Corporate network can accommodate approximately 22 additional devices before the subnet reaches its normal usable capacity.

# 6. Servers Network
Network: 192.168.50.64/26

Address information
* Network address: 192.168.50.64
* CIDR: /26
* Subnet mask: 255.255.255.192
* Usable range: 192.168.50.65 – 192.168.50.126
* Default gateway: 192.168.50.65
* Broadcast: 192.168.50.127
* Usable addresses: 62
* Expected devices: approximately 10

## Addressing decision
Static addressing will be used for servers.

Servers should have predictable IP addresses because users, applications and administrators may need to reach them consistently.

## Growth capacity
There are 62 usable addresses and approximately 10 expected devices.

Therefore: 62 − 10 = 52 addresses available for growth. This gives the server network considerable room for additional servers and infrastructure without immediately requiring a new subnet.


# 7. Management Network
Network: 192.168.50.128/26

## Address information
* Network address: 192.168.50.128
* CIDR: /26
* Subnet mask: 255.255.255.192
* Usable range: 192.168.50.129 – 192.168.50.190
* Default gateway: 192.168.50.129
* Broadcast: 192.168.50.191
* Usable addresses: 62
* Expected devices: approximately 10

## Addressing decision
Management devices will use DHCP to automatically receive their IP addresses, subnet mask, default gateway, and DNS settings. This simplifies address management for devices such as the router, switch, and wireless access points.

## Growth capacity
There are 62 usable addresses and approximately 10 expected devices.

Therefore: 62 − 10 = 52 addresses available for growth

This provides substantial room for additional network-management devices.

# 8. Guest Wi-Fi Network

Network: 192.168.50.192/26

## Address information
* Network address: 192.168.50.192
* CIDR: /26
* Subnet mask: 255.255.255.192
* Usable range: 192.168.50.193 – 192.168.50.254
* Default gateway: 192.168.50.193
* Broadcast: 192.168.50.255
* Usable addresses: 62
* Expected devices: approximately 30

## Addressing decision
DHCP will be used for Guest Wi-Fi.

Guest devices are temporary and can frequently connect and disconnect. DHCP allows guest devices to receive IP addresses automatically without requiring manual configuration.

## Growth capacity
There are 62 usable addresses and approximately 30 expected devices.

Therefore: 62 − 30 = 32 addresses available for growth. This allows the guest network to accommodate additional visitors and devices.

# 9. Growth Capacity
The design provides reasonable capacity for growth because each network has 62 usable host addresses, while the expected device counts are lower.

|Network |	Usable Addresses |	Expected Devices |	Remaining Capacity |
|---|---|---|---|
|Corporate Users |	62 |	~40	| 22 |
|Servers |	62 |	~15 |	47 |
|Management |	62 |	~10 |	52 |
|Guest Wi-Fi |	62 |	~30 |	32 |

Therefore, the networks are not being filled to their current limits.

For example, the Corporate network is expected to have around 40 devices but can support up to 62 usable addresses. This leaves space for approximately 22 additional devices.

The same principle applies to the other networks.

This means Meridian can add devices in the future without immediately redesigning or expanding the subnets.


# 10. Complete Addressing Summary
Allocated Network:
192.168.50.0/24
```
                    192.168.50.0/24
                           │
             ┌─────────────┴─────────────┐
             │                           │
          /26                          /26
             │                           │
   Corporate Users                 Servers
   192.168.50.0/26                192.168.50.64/26
   Gateway: .1                    Gateway: .65
   62 usable hosts                62 usable hosts
             │                           │
             └─────────────┬─────────────┘
                           │
             ┌─────────────┴─────────────┐
             │                           │
          /26                          /26
             │                           │
       Management                    Guest Wi-Fi
   192.168.50.128/26             192.168.50.192/26
   Gateway: .129                 Gateway: .193
   62 usable hosts               62 usable hosts
```
### Final Justification
The /26 subnet was selected because Meridian requires four separate logical networks from the allocated /24 address space. Borrowing two bits creates exactly four subnets, with each subnet providing 62 usable host addresses. The expected device counts are below the available capacity in every segment, leaving room for future growth. DHCP is used for dynamic user and guest devices, while static addressing is used for servers that require predictable addresses. 