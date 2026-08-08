# Day 15 - TCP, UDP & network testing utilities

## Day 15 Overview

Today I continued learning computer networking and focused on **TCP and
UDP, port numbers, and basic network troubleshooting commands**. I also
practiced these concepts using **Cisco Packet Tracer**.

The Packet Tracer activities helped me understand how network
communication can be tested from a device and how IP configuration
information can be checked using command-line utilities.

------------------------------------------------------------------------

# 1. TCP and UDP

TCP and UDP are two important **Transport Layer (Layer 4)** protocols.

## TCP - Transmission Control Protocol

TCP is a **connection-oriented and reliable** protocol.

It makes sure that data reaches the destination correctly and in the
proper order.

### Main characteristics of TCP

-   Connection-oriented
-   Reliable delivery
-   Uses acknowledgments
-   Uses sequence numbers
-   Retransmits lost data
-   Maintains the order of data
-   Provides flow and congestion control

TCP divides a message into smaller pieces called **segments**. Each
segment is assigned a sequence number.

If a segment is lost and the sender does not receive an acknowledgment
within the expected time, TCP retransmits the missing segment rather
than sending the complete message again.

### Examples of TCP applications

-   HTTP/HTTPS
-   FTP
-   SSH
-   Email protocols such as SMTP

### Simple example

When downloading an important file, losing a few bytes of data could
corrupt the file. TCP helps ensure that the missing data is
retransmitted.

------------------------------------------------------------------------

## UDP - User Datagram Protocol

UDP is a **connectionless and best-effort** protocol.

It does not require an acknowledgment for every packet and does not
retransmit lost packets.

### Main characteristics of UDP

-   Connectionless
-   Faster and lightweight
-   No delivery guarantee
-   No acknowledgment
-   No retransmission
-   Does not guarantee packet order
-   Lower overhead than TCP

UDP is useful when **speed is more important than perfect delivery**.

### Examples of UDP applications

-   Video streaming
-   Audio streaming
-   VoIP
-   Online gaming
-   DNS

### Simple example

During a live video call, losing a small amount of data is usually
better than waiting for retransmission because retransmission can cause
noticeable delay.

------------------------------------------------------------------------

## TCP vs UDP

  Feature           TCP                   UDP
  ----------------- --------------------- ----------------------
  Connection        Connection-oriented   Connectionless
  Reliability       Reliable              Best effort
  Acknowledgments   Yes                   No
  Retransmission    Yes                   No
  Ordering          Maintains order       No guarantee
  Speed             Generally slower      Generally faster
  Overhead          Higher                Lower
  Example           HTTPS, FTP, SSH       DNS, VoIP, streaming

### What I understood

**TCP = reliability first**

**UDP = speed and low overhead first**

------------------------------------------------------------------------

# 2. Port Numbers

A **port number** is a numerical identifier used by TCP or UDP to
identify a particular service or application on a device.

An IP address identifies the **host**, while a port number helps
identify the **service running on that host**.

For example:

``` text
192.168.1.10:80
```

Here:

-   `192.168.1.10` = IP address of the host
-   `80` = port number
-   Port 80 is commonly associated with HTTP

Port numbers range from **0 to 65535**.

## Categories of port numbers

### 1. Well-Known Ports

Range:

``` text
0 - 1023
```

These are associated with common network services.

Examples:

     Port Service
  ------- ---------
    20/21 FTP
       22 SSH
       23 Telnet
       25 SMTP
       53 DNS
       80 HTTP
      443 HTTPS

### 2. Registered Ports

Range:

``` text
1024 - 49151
```

These ports can be registered for particular applications and services.

### 3. Private / Dynamic Ports

Range:

``` text
49152 - 65535
```

These are commonly used as temporary source ports for client-side
connections.

------------------------------------------------------------------------

## Source Port and Destination Port

When a client communicates with a server, a TCP or UDP segment contains
both a **source port** and a **destination port**.

Example:

``` text
Client: 192.168.1.10:50000
        |
        | HTTP request
        v
Server: 192.168.1.20:80
```

Here:

-   `50000` = temporary source port
-   `80` = destination port for HTTP

The source port helps the client keep track of different simultaneous
conversations.

------------------------------------------------------------------------

## Why Port Numbers Are Important

Port numbers allow a computer to run multiple network services at the
same time.

For example, one server could simultaneously provide:

``` text
Web service  -> Port 80
HTTPS        -> Port 443
SSH          -> Port 22
DNS          -> Port 53
```

Without port numbers, the receiving device would have difficulty
determining which application should receive incoming data.

------------------------------------------------------------------------

# 3. Network Troubleshooting Commands

Today I learned several commands that can be used to identify and
troubleshoot network problems.

## 3.1 ipconfig

The `ipconfig` command displays basic IP configuration information.

Example:

``` text
ipconfig
```

It can show:

-   IPv4 address
-   Subnet mask
-   Default gateway

------------------------------------------------------------------------

## 3.2 ipconfig /all

The `ipconfig /all` command displays more detailed network configuration
information.

Example:

``` text
ipconfig /all
```

It can show:

-   Host information
-   MAC address
-   IPv4 address
-   Subnet mask
-   Default gateway
-   DHCP server
-   DNS server
-   DHCP lease information

This is useful when checking whether a device has received the correct
network configuration.

------------------------------------------------------------------------

## 3.3 ping

The `ping` command checks whether another IP-enabled device can be
reached across the network.

Example:

``` text
ping 192.15.2.10
```

A ping sends an **ICMP Echo Request** to the destination. If the
destination responds, it sends an **ICMP Echo Reply**.

A successful ping helps confirm basic network connectivity.

The output can also show:

-   Number of packets sent
-   Number of packets received
-   Packet loss
-   Approximate round-trip time

------------------------------------------------------------------------

## 3.4 netstat

`netstat` displays network connections and related information.

It can be used to inspect:

-   Active connections
-   Local addresses and ports
-   Foreign addresses and ports
-   Connection states
-   Protocols in use

It is useful when investigating unexpected or unexplained network
connections.

------------------------------------------------------------------------

## 3.5 tracert

`tracert` displays the path taken by packets from the source to the
destination.

Example:

``` text
tracert 8.8.8.8
```

It can help identify where communication is failing along a route.

------------------------------------------------------------------------

## 3.6 nslookup

`nslookup` is used to query DNS information.

Example:

``` text
nslookup google.com
```

It helps check whether a domain name can be resolved to an IP address.

------------------------------------------------------------------------

# Packet Tracer Activities

## Activity 1 - Testing Connectivity with Ping

### Objective

To test connectivity between a PC and different IP addresses using the
`ping` command.

### Topology

The activity used a PC connected through a network containing a wireless
router and an Internet connection.

![User management](images/day15_act1topology)
![User management](images/day15_act1ping)

### Commands Performed

I opened the PC command prompt and tested connectivity using:

``` text
ping 192.15.2.10
```

and

``` text
ping 192.15.2.5
```

### Result

Both destinations returned **Reply** messages.

The packet statistics showed:

``` text
Packets: Sent = 4, Received = 4, Lost = 0
```

This means there was **0% packet loss** in the tests.

### What the activity demonstrated

The activity showed how `ping` can be used to verify whether a
destination is reachable.

A successful ping means that the device was able to send an ICMP Echo
Request and receive an ICMP Echo Reply.

It also demonstrated that ping provides useful information about
response time.

------------------------------------------------------------------------

# Activity 2 - Checking Wireless PC Configuration

### Objective

To inspect the network configuration of a PC connected to a wireless
router.

### Topology

The Packet Tracer topology contained:

``` text
PCs
 |
 | Wireless
 v
Wireless Router
 |
 v
Internet
```

The activity included multiple PCs connected to the wireless router.

### Command Used

On PC1, I used:

``` text
ipconfig /all

```

![User management](images/day15_act2)

### Important information observed

The PC received network configuration including:

``` text
IPv4 Address     : 192.168.1.198
Subnet Mask      : 255.255.255.0
Default Gateway  : 192.168.1.1
DHCP Server      : 192.168.1.1
DNS Server       : 192.15.2.5
```

The PC also displayed its physical/MAC address and other configuration
information.

### What this demonstrated

This activity showed how a PC connected to a network can obtain its
configuration automatically through **DHCP**.

The important relationship is:

``` text
PC
 |
 | requests network configuration
 v
DHCP Server / Wireless Router
 |
 +--> IP Address
 +--> Subnet Mask
 +--> Default Gateway
 +--> DNS Server
```

The default gateway `192.168.1.1` provides the route for communication
outside the local network.

The DNS server allows the device to resolve domain names into IP
addresses.

------------------------------------------------------------------------

# What I Learned from the Packet Tracer Simulations

The simulations made the theoretical concepts easier to understand.

### 1. I learned how ping works

I understood that `ping` is not simply checking whether a device is
"on". It tests network reachability by sending ICMP Echo Requests and
waiting for Echo Replies.

### 2. I learned how to interpret ping statistics

I learned that:

``` text
Sent = 4
Received = 4
Lost = 0
```

means the test had **0% packet loss**.

The response time also gives an idea of how quickly the destination
responded.

### 3. I learned how to check IP configuration

Using:

``` text
ipconfig /all
```

I could see much more information than with a normal `ipconfig` command.

### 4. I understood DHCP more clearly

The simulation showed that a PC can automatically receive important
network settings such as:

-   IP address
-   Subnet mask
-   Default gateway
-   DNS server

This helped me understand the practical purpose of DHCP.

### 5. I connected IP addresses with gateways

The activity helped me understand that a PC uses its **default gateway**
when it needs to communicate outside its local network.

### 6. I understood the purpose of DNS

The DNS server shown in the PC configuration is responsible for helping
translate domain names into IP addresses.

### 7. I connected theory with practical networking

Instead of only reading about commands, I actually used them in Packet
Tracer and observed the results.

------------------------------------------------------------------------

# Important Commands Learned Today

  Command                 Purpose
  ----------------------- ------------------------------------------------
  `ipconfig`              Displays basic IP configuration
  `ipconfig /all`         Displays detailed IP and network configuration
  `ping <IP>`             Tests connectivity to a destination
  `netstat`               Displays network connections and ports
  `tracert <IP/domain>`   Shows the route/path to a destination
  `nslookup <domain>`     Queries DNS information

------------------------------------------------------------------------

# Key Takeaways

-   **TCP** provides reliable and ordered communication.
-   **UDP** provides faster, lightweight, best-effort communication.
-   **Port numbers** identify services/applications on a host.
-   Port numbers range from **0 to 65535**.
-   `ipconfig` is useful for checking IP configuration.
-   `ipconfig /all` provides detailed configuration information.
-   `ping` is used to test network reachability.
-   `netstat` helps inspect network connections and ports.
-   `tracert` helps identify the route taken to a destination.
-   `nslookup` is useful for troubleshooting DNS.
-   **DHCP** can automatically provide IP configuration to a device.
-   The **default gateway** is used to reach networks outside the local
    network.
-   Packet Tracer helped me connect networking theory with actual
    network behavior.

------------------------------------------------------------------------

# Day 15 Summary

Today I learned about **TCP and UDP, port numbers, and network
troubleshooting commands**. I practiced `ping` and `ipconfig /all` in
Cisco Packet Tracer.

The most useful part of today's learning was seeing the concepts in
action. The simulations helped me understand how devices receive IP
configuration, how connectivity is tested, and how different
troubleshooting commands provide information about a network.

**Day 15 completed.**
