### 1. Methods Used in Framing

Framing divides a bit stream from the physical layer into discrete frames at the data link layer. Common methods include:

* **Character Count:** A header field specifies the total number of characters (or bytes) in the frame.
* **Byte Stuffing (Character Stuffing):** Special flag bytes mark frame boundaries; if the flag or escape byte appears inside the payload, an escape byte (`ESC`) precedes it.
* **Bit Stuffing:** A distinctive bit pattern (such as `01111110`) delimits frames; the sender inserts a `0` after every five consecutive `1`s in the data, and the receiver removes it.
* **Physical Layer Coding Violations:** Uses invalid signal transitions (such as high-high or low-low in Manchester encoding) that cannot occur in valid payload data to mark frame boundaries.

---

### 2. Data Units in the TCP/IP Suite

* **(a) Network Layer:** **Packet** (often called a **datagram** in connectionless IP).
* **(b) Data Link Layer:** **Frame**.

---

### 3. Error Detection and Two Methods

**Error detection** is the process of adding redundant bits to transmitted data so the receiver can determine whether bits were altered or lost during transmission (without necessarily correcting them directly).

Two common methods:

1. **Parity Check** (single-bit or two-dimensional parity).
2. **Cyclic Redundancy Check (CRC)** or **Checksum**.

---

### 4. Cyclic Redundancy Check (CRC)

**Cyclic Redundancy Check (CRC)** is an error-detection technique that treats a data block as a polynomial over $\text{GF}(2)$ (binary arithmetic without carries/borrows). The sender divides the augmented message bits by a predetermined **generator polynomial** (divisor), appends the resulting remainder (CRC bits) to the frame, and the receiver divides the received frame by the same generator—a non-zero remainder indicates a transmission error. CRC is especially effective at catching burst errors.

---

### 5. Block Coding and Its Purpose

**Block coding** divides a stream of data bits into fixed-size blocks of $k$ bits (called **datawords**) and maps each block to a longer block of $n$ bits (called **codewords**), where $n > k$ (often written as $n\text{B}/m\text{B}$ or $k\text{B}/n\text{B}$ depending on convention).

Its main purposes are:

* **Error Detection (and sometimes correction):** Out of $2^n$ possible codewords, only $2^k$ are valid; landing on an invalid codeword signals an error.
* **Synchronization and Signal Balance:** Ensures enough bit transitions for clock recovery and limits long runs of `0`s or `1`s or DC offset on the line.

---

### 6. Sliding Window Protocol

A **sliding window protocol** is a flow-control and error-control mechanism at the data link (and transport) layer in which the sender can transmit multiple frames/packets before requiring acknowledgments, up to a defined **window size**. Both sender and receiver maintain logical windows of sequence numbers that advance ("slide") as frames are sent, acknowledged, or received in order, improving link utilization over stop-and-wait protocols.

---

### 7. IP Address vs. MAC Address

| Feature | IP Address | MAC Address |
| --- | --- | --- |
| **OSI / TCP-IP Layer** | Network Layer (Layer 3). | Data Link Layer (Layer 2). |
| **Address Nature** | Logical address; can change when moving across networks or reconfigured via DHCP. | Physical (hardware) address; typically burned into the Network Interface Card (NIC). |
| **Scope & Routing** | Identifies a host across different networks and guides end-to-end routing. | Identifies a device on the local network segment / link hop. |
| **Typical Format** | IPv4: 32-bit dotted decimal (e.g., `192.168.1.10`); IPv6: 128-bit hexadecimal. | Usually 48-bit (6-byte) hexadecimal (e.g., `00:1A:2B:3C:4D:5E`). |

---

### 8. Static Routing vs. Dynamic Routing

* **Static Routing:** Routes are manually configured and updated by a network administrator. It has low CPU/bandwidth overhead and predictable paths, but does not automatically adapt to link failures or topology changes.
* **Dynamic Routing:** Routers automatically discover networks, exchange topology/metric updates using routing protocols (such as OSPF, BGP, or RIP), and update routes when links go down or congestion changes, at the cost of extra control traffic and computation.

---

### 9. Purpose and Location of the Routing Table

* **Purpose:** A routing table stores forwarding rules (destination network/prefix, next-hop address or outgoing interface, and metric/cost) so a router or host can decide the best outgoing path for each incoming packet.
* **Where It Is Maintained:** Maintained in the memory (RAM/forwarding tables) of **routers** and **network hosts/end systems** (including layer-3 capable devices).

---

### 10. Congestion Control

**Congestion control** refers to techniques and algorithms used to prevent or relieve network congestion—a state where too many packets enter the network or a queue faster than routers/links can process or forward them, leading to dropped packets, high delay, and retransmissions.

---

### 11. One Congestion Control Technique

**Leaky Bucket** (or **Token Bucket** at the traffic-shaping/policing level, or **TCP Congestion Control** mechanisms such as Slow Start and Congestion Avoidance).