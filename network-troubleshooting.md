# NET-001 — Workstation Cannot Access the Internet
Incident

A workstation has:
* IP address: 192.168.50.25
* Default gateway: 192.168.50.1

The workstation can communicate with nearby systems but cannot access the Internet.

# Troubleshooting Approach

 1. Check the IP Configuration

Run: ipconfig and confirm that the workstation has:
* IP address: 192.168.50.25
* Subnet mask: 255.255.255.192
* Default gateway: 192.168.50.1
* A valid DNS server

The IP address and gateway are correct for the Corporate Users network.

 2. Test the Local Network

Ping another device on the same network:
``` ping 192.168.50.x ```

If this succeeds, local network communication is working.

3. Test the Default Gateway

Run: ping 192.168.50.1

If this succeeds, the workstation can reach the router/firewall.

If it fails, i would investigate the workstation’s connection, switch port, VLAN configuration, or gateway interface.

4. Test an Internet IP Address

Try:
``` ping 8.8.8.8 ```

If the gateway responds but 8.8.8.8 does not, i will investigate the router/firewall’s Internet connection, routing, NAT or ISP connection.

5. Test DNS

Try:
```  nslookup example.com ```

If 8.8.8.8 is reachable but the domain name cannot be resolved, i would investigate the DNS configuration.

6. Check the Router/Firewall

If the workstation can reach the gateway but cannot reach the Internet, check:

* WAN/ISP connection
* Default route
* NAT configuration
* Firewall rules
* DNS forwarding

7. Verify the Result

After making any required correction, test:
``` bash
ping 192.168.50.1
ping 8.8.8.8
nslookup example.com
```

Then open a website in the browser to confirm that Internet access has been restored.

Likely Fault Area

Because the workstation can communicate with nearby systems and has a valid Corporate Users IP address and gateway, the problem is less likely to be the local workstation connection. If the gateway is reachable but Internet IP addresses are not, the investigation should focus on the router/firewall, NAT, routing or ISP connection. If Internet IP connectivity works but domain names fail, DNS is the likely area to investigate.

## NET-002 — Websites Do Not Load by Name

Incident

A user reports: I can successfully reach 8.8.8.8, but websites do not load when I type their names.

## Troubleshooting Approach

1. Confirm Internet Connectivity

First, test:
``` ping 8.8.8.8 ```



If the ping succeeds, the device has working connectivity to an Internet IP address.

2. Check DNS Configuration

Run:
``` ipconfig /all ```

Check which DNS server the computer is using.

The DNS server should be reachable and correctly configured.

3. Test DNS Resolution

Run: 
``` nslookup example.com ```

If the command fails or returns no IP address, DNS name resolution is likely the problem.

DNS is responsible for translating a website name such as example.com into an IP address that the computer can connect to.

4. Check DNS Server Availability

Test whether the configured DNS server can be reached.

If the DNS server is unavailable, i would investigate the local router, DNS service, DHCP configuration, or network connection to the DNS server.

5. Clear the DNS Cache

A corrupted or outdated local DNS cache can sometimes cause resolution problems.

On Windows, run:
``` ipconfig /flushdns ```

Then test the website again.

6. Check Browser and DNS Settings

If DNS resolution works from the command line but websites still do not load, investigate:

* Browser DNS settings
* Proxy settings
* Firewall rules
* Browser cache
* HTTPS/TLS connectivity

7. Verify the Result

Run:
```  nslookup example.com ```

Then try opening the website in the browser.

Likely Fault Area

Because 8.8.8.8 is reachable but website names cannot be used successfully, the most likely area to investigate is DNS name resolution rather than the basic Internet connection.

## NET-003 — Workstation Assigns Itself a 169.254.x.x Address

Incident

A workstation assigns itself an IP address beginning with: 169.254.x.x

## Troubleshooting Approach

1. Identify the Address

An address beginning with 169.254.x.x is an APIPA (Automatic Private IP Addressing) address.

Windows can assign this type of address when it cannot obtain an IP address from a DHCP server.

2. Check the IP Configuration

Run: ``` ipconfig /all ```

Check:

* IPv4 address
* Subnet mask
* DHCP enabled status
* DHCP server
* Default gateway
* DNS server

A missing DHCP server or missing default gateway would support the possibility of a DHCP problem.

3. Check the Physical or Wireless Connection

Confirm that the workstation is properly connected to the network.

For a wired connection, i would check:

* Ethernet cable
* Switch port
* Link status

For a wireless connection, check:

* Wi-Fi connection
* Correct wireless network
* Access point availability

4. Test DHCP

Renew the DHCP lease: ipconfig /release  ipconfig /renew

Then check the address again:

``` ipconfig ```

If the workstation receives a valid address from the expected subnet, DHCP is working again.

5. Investigate the DHCP Server

If the workstation continues to receive a 169.254.x.x address, investigate:

* Whether the DHCP server is running
* Whether the DHCP scope has available addresses
* Whether the workstation is connected to the correct VLAN
* Whether DHCP traffic is being blocked
* Whether a DHCP relay is required between networks

6. Verify the Result

After correcting the problem, confirm that the workstation receives an appropriate address from the network.

For example, a Corporate Users workstation should receive an address from:

192.168.50.1 – 192.168.50.62

Then test the default gateway:``` ping 192.168.50.1 ```

Likely Fault Area

The 169.254.x.x address strongly suggests that the workstation could not obtain an IP address from DHCP. The investigation should therefore focus on the workstation’s network connection, VLAN, DHCP server, DHCP scope and any network equipment between the workstation and DHCP server.

## NET-004 — Two Employees Intermittently Lose Network Access

Incident

Two employees intermittently lose network access after both arriving at the office.

## Troubleshooting Approach
The fact that two employees experience the problem around the same time suggests that they may share a network component, wireless access point, VLAN or other network service.

Hypothesis 1 — Wireless Access Point Problem

Both employees may connect through the same wireless access point, which could be overloaded, unstable or experiencing interference.

How to investigate:

* Identify which access point both employees are connected to.
* Check whether other users connected to the same access point experience the problem.
* Check access point logs and connection status.
* Test the users from a different access point.

If the problem disappears when they use another access point, the original access point becomes a likely fault area.

Hypothesis 2 — DHCP Address Pool Exhaustion

The arrival of additional employees may cause more devices to request DHCP addresses. If the DHCP scope is too small, new devices may fail to obtain valid addresses.

How to investigate:

Run: ``` ipconfig /all ```

Check the assigned IP addresses and DHCP server.

Check the DHCP scope for:

* Available addresses
* Leases
* Expired leases
* Scope exhaustion

If affected devices receive 169.254.x.x addresses, DHCP failure becomes more likely.

Hypothesis 3 — Network Congestion

A large number of devices becoming active could increase network traffic and cause performance problems.

How to investigate:

* Monitor switch and access point utilisation.
* Check network latency and packet loss.
* Compare network performance before and after employees arrive.
* Check whether other users experience similar problems.

If packet loss or high utilisation increases when more users arrive, congestion may be contributing to the issue.

Hypothesis 4 — Duplicate IP Addresses

Two devices could accidentally be using the same IP address, causing intermittent connectivity.

How to investigate:

* Compare the IP addresses of affected devices.
* Check DHCP leases.
* Use arp -a to examine IP-to-MAC mappings.
* Check network logs for duplicate-address warnings.

If two devices are using the same address, correcting the addressing conflict should eliminate the problem.

Hypothesis 5 — Switch Port or VLAN Problem

If both employees are connected to the same switch or VLAN, a configuration or connectivity problem could affect both users.

How to investigate:

* Identify the switch ports used by the affected devices.
* Check whether the ports are up.
* Verify the VLAN assignment.
* Test the users from different switch ports or another VLAN where appropriate.
* Check switch logs for errors.

If moving a device to a correctly configured port resolves the problem, the original port or VLAN configuration should be investigated further.

Hypothesis 6 — Authentication or Network Access Control

The network may have authentication or access-control systems that behave differently when users arrive and connect their devices.

How to investigate:

* Check authentication logs.
* Check whether both users are being denied or disconnected.
* Compare successful and failed authentication attempts.
* Test with an authorised device known to work.

Conclusion

Because two employees experience intermittent network loss around the same time, I would first investigate shared infrastructure such as the wireless access point, DHCP service, switch/VLAN configuration and network utilisation.

Each hypothesis should be tested with evidence rather than assuming a single cause. The fault can be narrowed down by identifying what the two employees have in common and comparing their network behaviour with users who are not experiencing the problem.

## NET-005 — Guest Wi-Fi Can Access Internal Server

The network segmentation and firewall rules should be investigated.

The Guest Wi-Fi network should be isolated from the Server network.

Check:

* Guest VLAN configuration
* Firewall/ACL rules between Guest and Server networks
* Router inter-network routing rules
* Server firewall rules

A test should be performed by attempting to reach the server from a Guest device. The configuration should then be checked to ensure that Guest traffic to the Server network is denied, while Guest Internet access remains allowed.

Expected result: Guest devices should not be able to access internal company servers.
