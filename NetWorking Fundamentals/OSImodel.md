# The OSI Model (Open Systems Interconnection Model)

This model provides a frameworks dictating how all networks devices will send, receive and interpret data.

One of the main benefits of OSI Model is that devices can have different functions and designs on a network while communicating with other devices. Data sent across a network that follows the uniformity of the OSI Model can be understood by other devices

The OSI Model consists of seven layers:

1. **Physical** 
2. **Data Link** 
3. **Network** 
4. **Transport** 
5. **Session**
6. **Presentation** 
7. **Application** 

## **Layer 1 – Physical**

This is one of the easiest layers to understand.  

The **Physical layer** refers to the physical components of networking hardware and is the **lowest layer** of the OSI model.

It is responsible for the transmission of raw data as **electrical, optical, or radio signals**. Devices use electrical signals to transfer data between each other in a binary numbering system (1's and 0's).

Examples: Ethernet Cable, Fiber optics, connectors and pins.

## **Layer 2 – Data Link**

The **Data Link layer** focuses on the **physical addressing** of data transmission within a local network.  
It receives data from the **Network layer** and encapsulates it into **frames**, adding the **destination MAC (Media Access Control) address**.

Every network-enabled device contains a **Network Interface Card (NIC)**, which has a **unique MAC address** used to identify it on the local network.

MAC addresses are typically assigned by the manufacturer. When data is transmitted across a local network, it is the **MAC address**, not the IP address, that is used to determine where the data should be delivered.

Additionally, the Data Link layer is responsible for **framing**, **error detection**, and preparing data in a format suitable for transmission over the Physical layer.

## **Layer 3 – Network**

At this layer, **routing** determines the most optimal path that data packets should take to reach their destination across different networks.

Some protocols at this layer are responsible for calculating what the “optimal” path is. Examples of routing protocols include **OSPF (Open Shortest Path First)** and **RIP (Routing Information Protocol)**.

The route chosen is based on several factors, such as:
- **Shortest path** – the route with the fewest intermediate devices (hops).
- **Reliability** – whether packets are frequently lost on a particular path.
- **Link speed** – whether a path uses slower connections (e.g., copper) or faster ones (e.g., fiber).

At the Network layer, communication is handled using **IP addresses**, such as `192.168.1.100`.

Devices that forward packets based on IP addresses, such as **routers**, are known as **Layer 3 devices**, because they operate at the third layer of the OSI model.

## **Layer 4 – Transport**

The **Transport layer** plays a vital role in transmitting data across a network and can be slightly difficult to understand at first.  
When data is sent between devices, it uses one of two main protocols, chosen based on the requirements of the communication:

- TCP
- UDP


### TCP (Transmission Control Protocol)

TCP is designed with **reliability and accuracy** in mind. It establishes a **connection-oriented** session between two devices that remains active for the duration of the data transfer.

TCP includes **error checking, sequencing, and acknowledgment mechanisms**, which ensure that data is received **completely and in the correct order**.

#### Advantages:
- Guarantees accurate and ordered data delivery
- Prevents devices from overwhelming each other using flow control
- Highly reliable due to extensive error handling

#### Disadvantages:
- Requires a stable connection between devices
- If a packet is lost, retransmission is required, which can delay communication
- Slower than UDP due to additional processing and overhead

TCP is commonly used for services such as **file transfers, web browsing, and email**, where data accuracy and completeness are critical.


### UDP (User Datagram Protocol)

UDP is a **connectionless** protocol that prioritizes **speed over reliability**.  
It does not perform error checking, sequencing, or acknowledgments.

Data sent using UDP is transmitted without any guarantee that it will arrive or arrive in order.

Although this may seem disadvantageous, UDP is well suited for scenarios where speed is more important than accuracy.

#### Advantages:
- Much faster than TCP
- No connection setup or maintenance
- Leaves flow control decisions to the application layer

#### Disadvantages:
- No guarantee that data will be received
- No retransmission of lost packets
- Poor performance on unstable connections

UDP is commonly used in applications that transmit **small or time-sensitive data**, such as **video streaming, online gaming, VoIP, and device discovery protocols**.

## **Layer 5 – Session**

The Session Layer is responsible for creating and maintaining the connection with another computer where the data is destined, after the data has been properly handled by Layer 4.

This layer also handles closing the connection if it has been idle for too long or if the connection is lost. Additionally, a session can include **checkpoints**. If data loss occurs, only the most recent pieces of data need to be resent, which helps save bandwidth.

It is important to note that sessions are **unique**. Data does not move between different sessions; instead, it travels only within its own session.

A "session" is the technical term used to describe a successfully established connection between two communicating systems.

## **Layer 6 – Presentation**

At this layer, standardization begins to take place. All data must be handled in a consistent way, regardless of how the software itself works.

This layer acts as a translator for data moving to and from the Application Layer. The receiving computer can understand data sent in one format and convert it into another format if necessary.

Security features such as data encryption (for example, HTTPS when visiting a secure website) also operate at this layer.

## **Layer 7 – Application**

The layer which we are familiar with. The application layer is the layer in which protocols and rules are in place to determine how the user should interact with data sent or received

Everyday applications such as email clients, browsers, or file server browsing software such as FileZilla provide a friendly, Graphical User Interface (GUI) for users to interact with data sent or received. Other protocols include DNS (Domain Name System), which is how website addresses are translated into IP addresses.