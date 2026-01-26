
# What are Packets and Frames?

**Packets** are pieces of data at Layer 3 (Network Layer) of the OSI Model. They contain information such as the IP header and the payload. Packets allow data to be communicated efficiently across networked devices because the information is broken into small pieces. This reduces the chance of network bottlenecks compared to sending large amounts of data at once.

Packets have different structures depending on the type of packet being sent. Networking relies on many standards and protocols that define rules for how packets are handled by devices. With billions of devices connected to the internet, communication would quickly break down without this standardization.

**Frames** operate at Layer 2 (Data Link Layer). A frame encapsulates a packet and adds additional information, such as MAC addresses, which are used to deliver data within a local network.

## TCP/IP (The Three-Way Handshake)

The TCP/IP model consists of four layers and is often considered a simplified version of the OSI model. These layers are:

- Application  
- Transport  
- Internet  
- Network Interface  

One defining feature of TCP is that it is **connection-oriented**, meaning TCP must establish a connection between a client and a server before data is sent. Because of this, TCP provides reliable delivery of data. This connection process is called the **Three-Way Handshake**.

TCP packets contain various sections of information known as **headers**, which are added during encapsulation.

---

### TCP Header Fields

| Header | Description |
|--------|-------------|
| **Source Port** | This value is the port opened by the sender to send the TCP packet from. It is chosen randomly (from available ports between 0–65535 that are not already in use). |
| **Destination Port** | This value is the port number that an application or service is running on at the remote host (the one receiving data); for example, a web server running on port 80. Unlike the source port, this value is not random. |
| **Source IP** | This is the IP address of the device that is sending the packet. |
| **Destination IP** | This is the IP address of the device that the packet is destined for. |
| **Sequence Number** | When a connection begins, the first piece of data transmitted is assigned a random number. This helps track the order of data. |
| **Acknowledgement Number** | After data is assigned a sequence number, the acknowledgement number indicates the next sequence number the sender expects to receive. |
| **Checksum** | This value provides TCP integrity. A mathematical calculation is performed and stored. When the receiving device performs the same calculation, the data is considered corrupted if the result differs from the original. |
| **Data** | This field contains the actual data being transmitted, such as the bytes of a file. |
| **Flags** | This field determines how the packet should be handled during the TCP communication process. Specific flags control behaviors, especially during connection setup and termination. |

---

The **Three-Way Handshake** is the process used to establish a connection between two devices. It uses special control messages, as shown below:

### TCP Communication Process

| Step | Message | Description |
|------|---------|-------------|
| 1 | **SYN** | A SYN message is the initial packet sent by a client during the handshake. It is used to initiate a connection and synchronize the two devices. |
| 2 | **SYN/ACK** | This packet is sent by the receiving device (server) to acknowledge the synchronization attempt from the client and provide its own synchronization number. |
| 3 | **ACK** | The acknowledgement packet confirms that both devices are ready to start sending data. |
| 4 | **DATA** | Once a connection has been established, data (such as file bytes) is sent in TCP segments. |
| 5 | **FIN** | This packet is used to cleanly (properly) close the connection after communication has been completed. |
| — | **RST** | This packet abruptly ends communication. It is used as a last resort and indicates a problem during the process, such as an application error or lack of system resources. |

---

Any data sent is assigned a **sequence number** and is reconstructed using this number sequence in order. Both computers must agree on their starting sequence numbers so data can be delivered in the correct order. This agreement happens during the three steps:

1. **SYN (Client → Server)**  
   “Here is my Initial Sequence Number (ISN) to synchronize with.”

2. **SYN/ACK (Server → Client)**  
   “Here is my Initial Sequence Number (ISN) to synchronize with , and I acknowledge your sequence number.”

3. **ACK (Client → Server)**  
   “I acknowledge your Initial Sequence Number (ISN), and the connection is now established.”


## UDP/IP

UDP (User Datagram Protocol) is a stateless protocol that doesn't require a constant connection between two devices for data to be sent. A synchronisation between two devices does not happen.

UDP packets are much simpler than TCP packets and have fewer headers. However, when data is transmitted, the packet includes headers from both the IP layer and the UDP layer. These are what are annotated in the table below:

| Header | Description |
|--------|-------------|
| **Time to Live (TTL)** | An IP header field that sets an expiry timer for the packet. Each router reduces the value by 1, and if it reaches 0, the packet is dropped. This prevents packets from looping forever on the network. |
| **Source Address** | An IP header field. The IP address of the device sending the packet, so the receiver knows where to reply. |
| **Destination Address** | An IP header field. The IP address of the device the packet is being sent to, so the network knows where to deliver it. |
| **Source Port** | A UDP header field. The port opened by the sending application to send the UDP packet. This is usually randomly chosen from available ephemeral ports. |
| **Destination Port** | A UDP header field. The port number on the remote host where the receiving application or service is running (for example, DNS on port 53). This is not random. |
| **Length** | A UDP header field. Specifies the total length of the UDP header plus its data. |
| **Checksum** | A UDP header field used for error detection to ensure the header and data were not corrupted during transmission. |
| **Data** | The payload of the packet, the actual bytes being transmitted (file data, voice, video, DNS request, etc.). 

## PORTS 101

Ports are essential points through which data can be exchanged.

Networking devices use ports to enforce rules when communicating with one another. When a connection has been established, any data sent or received by a device is sent through these ports. Ports are numerical values between 0 and 65535.

Because ports can range anywhere between 0–65535, there is a risk of losing track of which application is using which port. Thankfully, we associate applications, software, and behaviors with a standard set of port numbers. For example, by convention, web browser data is typically sent over port 80.

While the standard rule for web data is port 80, many other protocols have also been assigned standard ports. Any port within the range 0–1023 is known as a **well-known port**. Some of these protocols are listed below:

| Protocol | Port Number | Description |
|----------|-------------|-------------|
| **File Transfer Protocol (FTP)** | 21 | This protocol is used by a file-sharing application built on a client-server model, meaning you can download files from a central location. |
| **Secure Shell (SSH)** | 22 | This protocol is used to securely log in to systems via a text-based interface for management. |
| **HyperText Transfer Protocol (HTTP)** | 80 | This protocol powers the World Wide Web (WWW). Your browser uses this to download text, images, and videos from web pages. |
| **HyperText Transfer Protocol Secure (HTTPS)** | 443 | This protocol does the same as HTTP; however, it uses encryption to secure the communication. |
| **Server Message Block (SMB)** | 445 | This protocol is similar to the File Transfer Protocol (FTP); however, in addition to files, SMB allows you to share devices like printers. |
| **Remote Desktop Protocol (RDP)** | 3389 | This protocol is a secure method of logging in to a system using a graphical desktop interface (as opposed to the text-based interface used by SSH). 









