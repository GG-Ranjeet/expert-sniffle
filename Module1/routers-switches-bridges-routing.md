# Q4. Differentiate between: (i) Routers, Switches, Bridges, and (ii) Static and Dynamic Routing.

---

## Part (i): Difference Between Routers, Switches, and Bridges

**Bridges**, **Switches**, and **Routers** are intermediate networking devices used to connect network segments and forward traffic, operating at different layers of the OSI model.

### Brief Overview
* **Bridge:** A Layer 2 device that connects two separate LAN segments and filters traffic using MAC addresses to reduce collisions.
* **Switch:** A multiport Layer 2 device (often called a *multiport bridge*) that uses hardware ASICs and a MAC address table to create dedicated point-to-point frame forwarding paths within a LAN.
* **Router:** A Layer 3 device that connects **different** networks (e.g., LAN to WAN/Internet) and determines the optimal path for packets using IP addresses and routing tables.

### Detailed Comparison Table

| Feature | Bridge | Switch | Router |
| :--- | :--- | :--- | :--- |
| **OSI Layer** | Data Link Layer (Layer 2) | Data Link Layer (Layer 2) *(Layer 3 switches also exist)* | Network Layer (Layer 3) |
| **Primary Function** | Connects two LAN segments into one logical LAN | Connects multiple devices within a single LAN | Connects multiple distinct networks (LANs / WANs) |
| **Addressing Used** | Physical (MAC) Address | Physical (MAC) Address | Logical (IP) Address |
| **Data Unit (PDU)** | Frame | Frame | Packet |
| **Number of Ports** | Typically 2 ports | Multiport (commonly 4 to 48+ ports) | Multiport (connects different network interfaces) |
| **Forwarding Method** | Software-based MAC table lookup | Hardware-based (ASICs) MAC address table | Routing table + routing algorithms (OSPF, BGP, etc.) |
| **Collision Domain** | Divides collision domains (1 per port) | Divides collision domains (1 per port) | Divides collision domains |
| **Broadcast Domain** | Single broadcast domain (forwards broadcasts) | Single broadcast domain *(unless VLANs are used)* | **Divides broadcast domains** (blocks Layer 2 broadcasts) |
| **Speed & Cost** | Slower, largely legacy | Very fast, moderate cost | More complex processing, higher cost |

---

## Part (ii): Difference Between Static and Dynamic Routing

**Routing** is the Layer 3 process by which a router selects the best path to forward packets from source to destination across interconnected networks.

### Brief Overview
* **Static Routing (Non-Adaptive):** Routes are manually configured and entered into the routing table by a network administrator. They do not change unless manually updated.
* **Dynamic Routing (Adaptive):** Routers automatically discover networks, exchange routing updates, and recalculate optimal paths using routing protocols (such as **RIP, OSPF, EIGRP, BGP**).

### Detailed Comparison Table

| Feature | Static Routing | Dynamic Routing |
| :--- | :--- | :--- |
| **Other Name** | Non-adaptive routing | Adaptive routing |
| **Configuration** | Manually configured by the network administrator | Automatically configured and updated via routing protocols |
| **Adaptability to Topology Changes** | Rigid; cannot automatically reroute if a link fails | Flexible; automatically detects link failures and recalculates paths |
| **CPU & Memory Overhead** | Very low (no routing algorithms running) | Higher (requires CPU/RAM to process updates and compute paths) |
| **Bandwidth Consumption** | None (no routing protocol update packets sent) | Consumes bandwidth for periodic/triggered routing updates |
| **Security** | Higher (paths are fixed and explicitly controlled by admin) | Lower (vulnerable to route spoofing/attacks if not authenticated) |
| **Scalability** | Poor; tedious to manage in large networks | High; ideal for large, complex enterprise and ISP networks |
| **Algorithms / Protocols Used** | Manual entries / default routes | Distance Vector (RIP), Link State (OSPF), Path Vector (BGP) |
| **Best Use Case** | Small, stable networks or stub networks | Large, dynamic networks with redundant paths |

---

## References & Study Hints
* **Tutorial References:**
  * [GeeksforGeeks – Difference between Bridge and Router](https://www.geeksforgeeks.org/computer-networks/difference-between-bridge-and-router/)
  * [GeeksforGeeks – Difference between Switch and Bridge](https://www.geeksforgeeks.org/computer-networks/difference-between-switch-and-bridge/)
  * [GeeksforGeeks – Difference between Router and Switch](https://www.geeksforgeeks.org/computer-networks/difference-between-router-and-switch/)
  * [GeeksforGeeks – Difference between Static and Dynamic Routing](https://www.geeksforgeeks.org/computer-networks/difference-between-static-and-dynamic-routing/)
* **Video Lecture:** [Neso Academy – Computer Networks Playlist (YouTube)](https://www.youtube.com/hashtag/computernetworksbyneso)
* **Exam Study Hints:**
  * For **Part (i)**, highlight **OSI Layer**, **Addressing (MAC vs. IP)**, **Collision vs. Broadcast domains**, and **PDU (Frame vs. Packet)**.
  * For **Part (ii)**, remember the alternative names (**Non-adaptive** vs. **Adaptive**) and give protocol examples (**RIP, OSPF, BGP**) for dynamic routing.
