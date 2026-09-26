# Task 2.2 — Explain the Communication Process

This is what happens when a Meridian employee enters:
``` bash
https://www.example.com into a browser.
```

## 1. Application -The Web Browser
The process begins at the application layer when the employee enters: https://www.example.com into a web browser such as Microsoft Edge, Google Chrome or Mozilla Firefox.

The browser interprets the URL(Uniform Resource Locator) and determines that HTTPS is being used. HTTPS indicates that the communication should be protected using TLS.

The browser needs to discover the IP address associated with www.example.com before it can communicate with the web server.

## 2. DNS- Finding the IP Address
The computer sends a DNS query to its configured DNS server asking for the IP address associated with: www.example.com. 

DNS or Domain Name System, translates human-readable domain names into IP addresses.

For example:
``` text
www.example.com
       ↓
DNS lookup
       ↓
IP address
```

The exact IP address returned can vary because large websites may use multiple servers, load balancing or content delivery networks.

## 3. IP
Once the browser has the destination IP address then the computer can determine where the traffic needs to go.

The employee’s computer has its own private IP address while the web server has an Internet-routable IP address.

The computer compares the destination IP address with its own subnet to determine whether the destination is on the local network.

Because the web server is normally outside the employee’s local subnet, the traffic needs to be sent to the default gateway.

## 4. Address Resolution Protocol (ARP)
Before sending the Ethernet frame to the default gateway, the computer needs the gateway’s MAC address.

If the MAC address is not already stored in the computer’s ARP cache, the computer uses ARP (Address Resolution Protocol) to ask:

Who has this IP address?

The device using the gateway IP responds with its MAC address.

The computer can then create an Ethernet frame addressed to the gateway’s MAC address.

## 5. MAC addressing
MAC addresses are used for local network communication.

The computer’s IP address identifies it at the IP layer while MAC addresses are used to deliver Ethernet frames across the local network.

The destination MAC address for the first local hop is normally the MAC address of the default gateway not the MAC address of the distant web server.

## 6. Switching
The computer sends the Ethernet frame to the network switch.

The switch examines the destination MAC address and forwards the frame through the appropriate port toward the default gateway.

This is called switching.

A switch primarily operates using MAC addresses to move frames within a local network.

## 7. Default gateway
The default gateway receives the traffic because the destination is outside the employee’s local subnet.

The gateway is normally a router or firewall.

## 8. Routing
The router examines the destination IP address and uses its routing information to determine where the packet should be forwarded next.

Routers connect different networks and use IP addresses to make forwarding decisions.

The packet may pass through several routers across the Internet before reaching the destination network.

## 9. NAT- Network Address Translation

The employee’s computer may use a private IP address that is not directly routable across the public Internet.

At the organization’s router or firewall, Network Address Translation (NAT) can translate the private source IP address into a public IP address.

For example:
```
Private IP
192.168.x.x
     ↓
NAT on router/firewall
     ↓
Public IP
     ↓
Internet
```
NAT allows multiple internal devices to share a public Internet connection while keeping their private addresses inside the organization’s network.

## 10. Transmission Control Protocol(TCP) & Ports
Before HTTPS application data can be exchanged, a reliable TCP connection is established.

The client normally uses a temporary source port, while HTTPS uses destination port 443.

TCP establishes a connection between the client and server using the three-way handshake:

Client → Server: SYN
Client ← Server: SYN-ACK
Client → Server: ACK

TCP also provides mechanisms for reliable delivery, sequencing and retransmission of data when necessary.

## 11. TLS
Because the URL uses HTTPS, TLS (Transport Layer Security) is used to protect the communication.

During the TLS process, the browser and server negotiate security parameters and establish cryptographic keys.

The browser also verifies the server’s digital certificate to help confirm that it is communicating with the intended website.

After the secure TLS session is established, application data can be exchanged securely.

## 12. HTTP/HTTPS
HTTP is the application-layer protocol used for communication between a web browser and a web server.

HTTPS is essentially HTTP protected by TLS.

The browser can then send an HTTP request through the encrypted HTTPS connection to request the webpage.

Conceptually:
```
Browser
   ↓
HTTPS request
   ↓
TLS encryption
   ↓
TCP
   ↓
IP
   ↓
Network
```

## 13. Encapsulation
Before the data travels across the network, it is encapsulated as it moves down the networking layers.

A simplified view is:
```
Application data
       ↓
TCP segment
       ↓
IP packet
       ↓
Ethernet frame
       ↓
Bits/signals
```
Each layer adds information needed for communication.

For example:

* TCP adds source and destination port information.
* IP adds source and destination IP addresses.
* Ethernet adds source and destination MAC addresses.

At the receiving side, the process is reversed through decapsulation.

## 14. Routing Across the internet
The packet travels through routers between the Meridian network and the network hosting the website.

Each router examines the destination IP address and forwards the packet toward the appropriate next network.

The exact route can vary depending on routing protocols, network conditions and Internet topology.

## 14. The Web Server Receives the Request

The destination server receives the traffic.

The server processes the HTTPS request and determines what content should be returned to the browser.

The response is then sent back toward the employee’s computer.

## 15. Return Traffic

The response travels back through the network.

 NAT was used, the organization’s router/firewall uses its NAT state to determine which internal computer initiated the connection and translates the traffic back toward that computer’s private IP address.

The traffic then travels through the local network to the employee’s computer.

The computer receives the packets, processes the TCP and TLS information and passes the protected application data to the browser.

The browser decrypts the TLS-protected data and renders the webpage for the employee.

## Overall Communication Flow

The complete process can be summarized as:
``` 
Employee enters https://www.example.com
                ↓
          Web Browser
                ↓
             DNS
                ↓
       Destination IP found
                ↓
       TCP connection / 443
                ↓
          TLS negotiation
                ↓
        HTTPS request
                ↓
       IP packet created
                ↓
     ARP finds gateway MAC
                ↓
             Switch
                ↓
        Default Gateway
                ↓
            Routing
                ↓
              NAT
                ↓
           Internet
                ↓
         Web Server
                ↓
        HTTPS Response
                ↓
            Routing
                ↓
              NAT
                ↓
        Default Gateway
                ↓
             Switch
                ↓
       Employee's computer
                ↓
      Browser displays page
```

This process demonstrates how multiple networking technologies work together. The browser operates at the application level, DNS resolves the domain name, TCP provides reliable transport, TLS protects the communication, IP provides logical addressing and routing, MAC addresses provide local delivery, ARP discovers local MAC addresses, switches forward frames, routers forward packets between networks, and NAT translates private and public addresses where required.