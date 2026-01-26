# Introduction to LAN

## Local Area Network (LAN) Topologies

When we refer to the term **topology**, we are referring to the design or layout of a network.

### **Star Topology**

The main premise of a star topology is that all devices are connected to a central
networking device, such as a **switch** or a **hub**.
This topology is the most commonly used today due to its reliability and scalability.

Any data sent between devices in this topology must pass through the central device
to which they are connected.

**Advantages:**
- Highly scalable: new devices can be added easily as network demand increases
- Easier to manage and monitor compared to other topologies
- Centralized management allows for better security control
- Improved performance, as each device has a dedicated connection to the central device

**Disadvantages:**
- More expensive: requires additional cabling and dedicated networking equipment
- Increased maintenance as the network grows
- If the centralized device fails, all connected devices lose the ability
  to send or receive data

### **Bus Topology**

This type of topology relies on a single central cable,
commonly referred to as the **backbone cable**.

Bus topology is often compared to the branches of a tree,
where devices connect to the backbone cable in a linear fashion.

**Advantages:**
- Cost-effective, as it requires less cabling and no dedicated networking equipment
- Simple to set up for small networks

**Disadvantages:**
- All data travels along the same cable, which can easily lead to congestion
  and performance bottlenecks when multiple devices communicate at the same time
- Troubleshooting is difficult, as it can be hard to identify which device
  is causing network issues
- If the backbone cable fails, all devices on the network lose the ability
  to send or receive data


### **Ring Topology**

The ring topology (also known as a token topology) connects devices directly to each other
in a circular loop.

Each device forwards data to the next one until it reaches its destination.
This design requires less cabling and less dedicated networking hardware
compared to a star topology.

**Advantages:**
- Less cabling is required compared to star topology
- No central networking device is needed
- Easier to troubleshoot due to unidirectional data flow
- Less prone to congestion than bus topology, as data is transmitted in an orderly manner

**Disadvantages:**
- Data may need to pass through multiple devices before reaching its destination, making communication less efficient
- If a single device fails, it can disrupt the entire network
- A broken or cut cable can cause the whole network to stop functioning
- Adding or removing devices can interrupt network communication


## What is a switch?

A switch is a dedicated networking device designed to connect multiple
network-capable devices using Ethernet.

Devices such as computers, printers, and servers connect to a switch through
physical ports.
Switches are commonly found in larger networks, such as businesses and schools,
and are available with varying numbers of ports, including 4, 8, 16, 24, 32,
and 64 ports.

Switches are significantly more efficient than their simpler counterparts,
such as hubs or repeaters.
A switch keeps track of which device is connected to each port.
When a packet is received, the switch forwards it only to the intended destination
instead of broadcasting it to all ports, which helps reduce unnecessary network traffic.

They can also be connected to routers.
This interconnection improves network redundancy and reliability by providing
multiple paths for data to travel.
If one path becomes unavailable, another path can be used.

## What is a Router?

A router is responsible for connecting different networks
and forwarding data between them.
It performs this task by using a process known as **routing**.

Routing is the process by which data is transmitted across networks.
It involves determining the most appropriate path for data to travel
so that it can be successfully delivered to its destination.


## Switch vs Router

Although switches and routers are both networking devices,
they serve different purposes within a network.

### Switch
- Operates within a **local network (LAN)**
- Connects multiple devices inside the same network
- Forwards data based on **MAC addresses**
- Reduces network traffic by sending data only to the intended device
- Commonly used to connect devices such as computers and printers

### Router
- Connects **different networks** together
- Routes data between local networks and external networks, such as the Internet
- Forwards data based on **IP addresses**
- Determines the best path for data to travel across networks
- Commonly used to connect a LAN to the Internet

Basically, a switch connects devices within the same network, while a router connects different networks together.

## Subnetting

Subnetting is the term given to splitting up a network into a smaller, miniature networks within itself.

Network administrators use subnetting to categorise and assign specific parts of a network to send information to the correct destination.

Subnetting is achieved by splitting up the number of hosts that can fit within the network, represented by a number called a subnet mask.


    192.168.1.1
    │   │   │ │
    │   │   │ └── Octet 4 (0–255)
    │   │   └──── Octet 3 (0–255)
    │   └──────── Octet 2 (0–255)
    └──────────── Octet 1 (0–255)


IP address is made up of four sections called octets. The same goes for a subnet mask which is also represented as a number of four bytes (32 bits), ranging from 0 to 255 (0-255).

Subnets use IP Adresses in three different ways:
- Identify the network address
- Identify the host adress
- identify the default gateway 

| Type            | Purpose                                                                 | Explanation                                                                                                                                       | Example        |
|-----------------|-------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|----------------|
| Network Address | This address identifies the start of the actual network and is used to identify a network's existence. | For example, a device with the IP address of 192.168.1.100 will be on the network identified by 192.168.1.0                                      | 192.168.1.0    |
| Host Address    | An IP address used to identify a device on the subnet.                  | For example, a device will have a host address such as 192.168.1.100                                                                              | 192.168.1.100  |
| Default Gateway | A special address assigned to a device on the network that can send information to another network. | Any data that needs to go to a device not on the same network will be sent to this device. Commonly the first or last host address is used (.1 or .254). | 192.168.1.254  |

Subnetting provides a range of benefits, including:
- Efficiency
- Security
- Full control

## ARP (Address Resolution Protocol)

The Address Resolution Protocol or ARP for short, is the technology that is responsible for allowing devices to identify themselves on a network.

Simply, ARP allow devices to associate its MAC address with an IP adress on the network. Each device on a network will keep a log of the MAC Addresses associated with other devices.

When devices wish to communicate with another, they will send a broadcast to the entire network searching for the specific device. Devices can use ARP to find the MAC Address of a devide in communication

### How ARP works?

Each device within a network maintains a table known as the ARP cache, which temporarily stores mappings between IP addresses and MAC addresses of other devices on the local network.

To resolve an IP address to a MAC address, ARP uses two types of messages: **ARP Request** and **ARP Reply**.

When an **ARP Request** is sent, it is broadcast to all devices on the local network, asking which device owns a specific IP address. Only the device that owns that IP address responds, sending an **ARP Reply directly** (unicast) to the requester with its MAC address.

The requesting device then stores this mapping in its ARP cache for future communication.

## DHCP (Dynamic Host Configuration Protocol)

IP addresses can be assigned either manually, by configuring them directly on a device, or automatically through a **DHCP (Dynamic Host Configuration Protocol)** server.  

This automatic process is commonly known as **DORA**:

**Discover → Offer → Request → Acknowledge**

When a device connects to a network and does not have a manually configured IP address, it sends a **DHCP Discover** message to identify available DHCP servers on the network.

A DHCP server responds with a **DHCP Offer**, proposing an IP address and related network configuration.  
The device then replies with a **DHCP Request**, indicating that it wants to use the offered IP address.

Finally, the DHCP server sends a **DHCP ACK**, confirming the assignment.  The device can then begin communicating on the network using the assigned IP address.

DHCP automates network configuration and avoids IP address duplication.
