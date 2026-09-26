# Task 2.4 Meridian Network Design

1. Network Structure

The proposed Meridian network separates users, servers, management systems and guest devices into different logical networks. This provides better control over communication between network segments and supports the addressing plan developed in Task 2.3.
```
                         INTERNET
                            │
                           ISP
                            │
                            ▼
                   ┌──────────────────┐
                   │ Router / Firewall │
                   └────────┬─────────┘
                            │
                            ▼
                       ┌─────────┐
                       │  Switch │
                       └────┬────┘
          ┌─────────────────┼─────────────────┬─────────────────┐
          │                 │                 │                 │
          ▼                 ▼                 ▼                 ▼
     CORPORATE           SERVERS          MANAGEMENT        GUEST WI-FI
       USERS               /26                /26               /26
       /26              .64/26             .128/26           .192/26
      .0/26                │                 │                 │
          │                │                 │                 │
     Windows          Linux Servers       Network Devices       Wireless AP
     Systems
     |
     Printer
    ```

2. Network Components

The proposed network contains the following major components:

* Internet — provides external connectivity.
* ISP connection — connects Meridian to the Internet service provider.
* Router/Firewall — provides routing between networks and controls traffic according to security rules.
* Core Switch — connects wired devices and logical network segments.
* Wireless Access Point — provides wireless access for guest devices.
* Corporate Users network — contains employee Windows systems and the printer.
* Server network — contains Linux servers.
* Management network — contains authorised administration systems.
* Guest Wi-Fi network — provides Internet access to guest devices.

3. Logical Network Structure

Corporate Users

* Network: 192.168.50.0/26
* Gateway: 192.168.50.1
* Purpose: Employee Windows systems and printer
* Addressing: DHCP

Servers

* Network: 192.168.50.128/26
* Gateway: 192.168.50.65
* Purpose: Linux servers
* Addressing: Static

Management

* Network: 192.168.50.160/26
* Gateway: 192.168.50.129
* Purpose: Authorised management, network devices and administration systems
* Addressing: DHCP

Guest Wi-Fi

* Network: 192.168.50.64/26
* Gateway: 192.168.50.193
* Purpose: Guest devices and wireless access 
* Addressing: DHCP

4.  Design Rationale

The networks are separated according to their function. This design separates users, servers, management devices, and guest devices into different logical networks while allowing the router/firewall to control communication between them.
