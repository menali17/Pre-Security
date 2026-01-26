

# What is networking

A network is a group of devices connected together so they can communicate and share data with each other.

Networking enables devices to exchange information using defined communication rules.
 
# What is internet

First, we understand what a network is.  
Then, we have the Internet, which is a giant network made up of many smaller networks.

These smaller networks are called private networks, such as home or corporate networks.

When multiple private networks are interconnected, they allow data to be routed between devices worldwide and form public networks, commonly known as the **Internet**.

# Identifying Devices on a Network

To communicate with each other, devices must be both identified and identifiable on a network.

Devices have two means of identification, with one being changeable. These are:
- An IP address
- A Media Access Control (MAC) address

The IP address can change depending on the network, while the MAC address is usually fixed to the device hardware.

## IP Address

An IP address (Internet Protocol address) is used to identify a host on a network for a period of time.
It can later be reassigned to another device without the address itself changing.

An IP address is a set of numbers divided into four octets.  
The combined value of these octets represents the address of a device on a network.

    192.168.1.1
    │   │   │ │
    │   │   │ └── Octet 4 (0–255)
    │   │   └──── Octet 3 (0–255)
    │   └──────── Octet 2 (0–255)
    └──────────── Octet 1 (0–255)

This structure is defined through techniques known as IP addressing and subnetting.

An IP address can change over time, but it **cannot** be assigned to more than one device
simultaneously within the same network.

A public IP address is used to identify a device on the Internet,
while a private IP address is used to identify a device within a local network.

Devices within the same private network can communicate using their private IP addresses.
However, when data is sent to the Internet, it is identified using a shared public IP address,
which is assigned by the Internet Service Provider (ISP).


## MAC Address

Every device on a network has a physical network interface,
which is a hardware component responsible for network communication.
This network interface is assigned a unique address at the factory where it is built,
known as a MAC (Media Access Control) address.

A MAC address is a twelve-character hexadecimal value
(a base-16 numbering system commonly used in computing),
split into pairs and separated by colons.

                                    a4:c3:f0:85:ac:2d

- The **first half** identifies the vendor (manufacturer) of the network interface  
- The **second half** uniquely identifies the device itself

A MAC address can be falsified or **spoofed** in a process known as **MAC spoofing**.
Spoofing occurs when a device pretends to identify as another by changing its MAC address.
This can break poorly implemented security designs that assume devices on a network are trustworthy.


## Ping (ICMP)

Ping uses **ICMP** (Internet Control Message Protocol) packets to test the connectivity and performance between devices, such as verifying whether a connection exists
and how responsive it is.

The time taken for ICMP packets to travel between devices is measured by the ping command,
usually referred to as latency.

Ping can be performed against devices on a local network,
such as a home network, or against remote resources like websites.
This tool is widely available and comes preinstalled on operating systems
such as Linux and Windows.

The basic syntax for a ping command is:

                            ping <IP address or website URL>


