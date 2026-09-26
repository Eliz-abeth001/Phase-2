# Task 2.1 — Current Network Investigation
This document records the current network configuration of my authorised home Windows system using my Windows host computer. The investigation identifies the system’s IP addressing, subnet, gateway, DHCP, DNS, MAC address and loopback configuration.

I used Windows command prompt:
 ``` bash
ipconfig/all
```
 to identify everything listed below;

## 1. IP address
An IP address identifies a device on a network. In my command prompt, I received 192.168.222.36 as my IPv4 Address which is the private address assigned to my computer on the local network.

## 2. subnet mask or CIDR prefix
A subnet is a smaller section of a larger network where devices can communicate directly with each other while subnet mask also help to understand which part represents the network and which part represents the host(device)

The subnet mask 255.255.255.0 is equivalent to a /24 CIDR prefix. The network is therefore: 192.168.222.0/24

This provides 256 total IPv4 addresses with 254 normally usable for hosts.

## 3. default gateway
The gateway is the device the computer uses when it needs to communicate outside its own subnet. The default gateway in my computer identified, 192.168.222.165. 

For example, when the computer needs to communicate with an Internet server, it forwards the traffic to the default gateway.

## 4. DHCP configuration
My computer received its network configuration through DHCP (Dynamic Host Configuration Protocol).

The DHCP server identified during the investigation was: 192.168.222.165

DHCP allows a device to obtain network configuration automatically instead of requiring the user to manually configure every setting.

The configuration supplied to the computer includes the IPv4 address, subnet mask, default gateway and DNS server.

## 5. DNS server
The DNS server identified was: 192.168.222.165

DNS (Domain Name System) translates human-readable domain names, such as example.com, into IP addresses that computers can use for communication.

## 6. MAC address
The network interface MAC address identified: 70-18-8B-22-02-ED

A MAC address is a hardware-level identifier associated with a network interface. It is used for communication within the local network.

## 7. loopback address
 A loopback is an IP address a computer use to communicate with itself. The loopback address is normally 127.0.0.1 then I used command prompt (ping) to perform a test against 127.0.0.1.

The result was:

* Packets sent: 4
* Packets received: 4
* Packets lost: 0
* Packet loss: 0%

## 8. private IP address
My computer’s private IP address is identified as; 192.168.222.36

Addresses in the 192.168.0.0/16 range are private IPv4 addresses. Private addresses are intended for use within local networks and are not directly routable across the public Internet.

## 9. public IP concept.
A public IP address is an Internet-routable address associated with a network’s connection to the Internet.

The computer’s private address, 192.168.222.36, is different from the public IP address used by the network when communicating with external Internet services.

Network Address Translation (NAT) can allow devices using private addresses to communicate with the Internet by translating private addresses into a public address.

## 10. How my computer receive its network configuration. 
My computer was configured automatically using DHCP. 

When the computer connects to the network, it can request network configuration from a DHCP server. The DHCP server at 192.168.222.165 provided the computer with its network settings.

The observed configuration included:

* IP address: 192.168.222.36
* Subnet mask: 255.255.255.0
* Default gateway: 192.168.222.165
* DNS server: 192.168.222.165

This automatic configuration allows the computer to communicate with devices on the local network and reach external networks through the default gateway.
