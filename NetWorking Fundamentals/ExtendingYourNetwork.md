# Network Extension

## Introduction to Port Forwarding

Port forwarding is an essential component in connecting applications and services to the internet. Without port forwarding, applications and services such as web servers are only available to devices within the same local network.

Port forwarding is configured on the router of a network. The router acts as a gateway between the private local network and the public internet.

When data arrives at the router from the internet, the router needs to know which device inside the local network should receive it. Port forwarding creates a rule that tells the router where to send that traffic.

For example, a rule might say that any traffic arriving on port 80 should be forwarded to a specific internal IP address, such as 192.168.1.10, where a web server is running.

This allows external users to access services hosted inside a private network by using the network’s public IP address and the correct port number.

However, port forwarding should be configured carefully, as opening ports to the internet can expose devices and services to security risks.

## Firewalls 101

A firewall is a device within a network responsible for determining what traffic is allowed to enter and exit. An administrator can configure a firewall to **permit** or **deny** traffic based on numerous factors such as:

- Where is the traffic coming from? (Has the firewall been told to accept/deny traffic from a specific network or IP address?)
- Where is the traffic going to? (Has the firewall been told to accept/deny traffic destined for a specific network or device?)
- What port is the traffic for? (Has the firewall been told to accept/deny traffic destined for port 80 only?)
- What protocol is the traffic using? (Has the firewall been told to accept/deny traffic that is UDP, TCP, or both?)

Firewalls perform packet inspection to determine the answers to these questions.

There are two primary categories of firewalls in the table below:

| Firewall Category | Description |
|-------------------|-------------|
| **Stateful** | This type of firewall uses information about the entire connection. Rather than inspecting each packet individually, it tracks the state of active connections and makes decisions based on the context of the traffic.<br><br>This firewall type consumes more resources compared to stateless firewalls because the decision-making process is dynamic. For example, a firewall may allow the early stages of a TCP handshake but later block the connection if it appears suspicious.<br><br>If a connection from a host is determined to be malicious, the firewall may block further traffic from that device. |
| **Stateless** | This firewall type uses a static set of rules to determine whether or not individual packets are acceptable. Each packet is inspected independently, without awareness of previous traffic.<br><br>While these firewalls use fewer resources than stateful alternatives, they are less intelligent. They are only as effective as the rules defined within them. If traffic does not exactly match a rule, it may be incorrectly allowed or denied.<br><br>However, these firewalls can be effective when handling very large volumes of traffic from many hosts (such as during a Distributed Denial-of-Service attack). |



## VPN Basics

A VPN (Virtual Private Network) is a technology that allows devices on separate networks to communicate securely by creating a dedicated path between them over the internet (known as a tunnel). Devices connected within this tunnel form their own private network.

For example, normally only devices within the same local network (such as within a business) can communicate directly. However, a VPN allows two offices in different locations to be securely connected as if they were on the same network.

There are also other benefits offered by a VPN, shown in the table below:

| Benefit | Description |
|---------|-------------|
| **Allows networks in different geographical locations to be connected** | For example, a business with multiple offices will find VPNs beneficial, as it means that resources like servers and infrastructure can be accessed from another office. |
| **Offers privacy** | VPN technology uses encryption to protect data. This means that it can only be understood by the device it was sent from and the device it is destined for, meaning the data isn't vulnerable to sniffing.<br><br>This encryption is useful in places with public WiFi, where no encryption is provided by the network. You can use a VPN to protect your traffic from being viewed by other people. |
| **Offers anonymity** | Journalists and activists depend on VPNs to safely report on global issues in countries where freedom of speech is restricted.<br><br>Usually, your traffic can be viewed by your ISP and other intermediaries and, therefore, tracked.<br><br>The level of anonymity a VPN provides depends on how the VPN provider handles your data. For example, a VPN that logs all of your data/history is essentially the same as not using a VPN in this regard. |

And then, we have some VPN technologies:

| VPN Technology | Description |
|----------------|-------------|
| **PPP** | The Point-to-Point Protocol (PPP) is used by tunneling protocols like PPTP to provide authentication and encapsulation of data. It can also support encryption features. However, PPP itself cannot travel across the internet alone (it is non-routable). |
| **PPTP** | The Point-to-Point Tunneling Protocol (PPTP) is the technology that allows PPP traffic to be tunneled across the internet.<br><br>PPTP is very easy to set up and is supported by most devices. However, it uses weak encryption compared to modern alternatives and is no longer considered secure. |
| **IPSec** | Internet Protocol Security (IPSec) encrypts data using the existing Internet Protocol (IP) framework.<br><br>IPSec is more complex to set up compared to alternatives; however, it provides strong encryption and is widely supported on many devices and in enterprise VPN solutions. |






