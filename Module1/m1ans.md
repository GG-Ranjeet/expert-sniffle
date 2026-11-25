### 1. Two Advantages of Computer Networking

* **Resource Sharing:** Multiple devices can share expensive hardware (such as printers, scanners, and storage servers) and software or data without needing duplicate copies on every machine.
* **Communication and Collaboration:** Users can exchange messages, transfer files, and collaborate in real time across local or remote systems via email, messaging apps, and shared workspaces.

---

### 2. Two Examples of Network Applications

* **Web Browsing (HTTP/HTTPS):** Accessing websites and web services hosted on remote servers through a browser.
* **Electronic Mail (SMTP/IMAP/POP3):** Sending, receiving, and managing digital messages across networks.

---

### 3. Wide Area Network (WAN)

A **Wide Area Network (WAN)** is a telecommunications network that spans a large geographical area—such as a country, continent, or the entire globe—connecting multiple smaller networks like LANs and MANs. It typically relies on leased lines, fiber-optic backbones, cellular networks, or satellite links. The public Internet is the largest example of a WAN.

---

### 4. Bus Topology vs. Star Topology

| Feature | Bus Topology | Star Topology |
| --- | --- | --- |
| **Layout** | All nodes connect to a single central cable (the bus/backbone) with terminators at both ends. | All nodes connect individually to a central device (a switch or hub). |
| **Fault Tolerance** | A break in the main cable or a missing terminator can disrupt the entire network. | A single node or cable failure affects only that node; the rest of the network keeps running. |
| **Troubleshooting & Scalability** | Harder to isolate faults and less convenient to expand without interrupting service. | Easier to isolate faults and add/remove devices without taking down the whole network. |

---

### 5. Hub vs. Switch

* **Hub:** Operates at the physical layer (Layer 1) and broadcasts incoming frames out of **all** ports except the incoming port, regardless of the destination address. All connected ports share a single collision domain.
* **Switch:** Operates primarily at the data link layer (Layer 2) and uses **MAC address tables** to forward frames only to the specific port mapped to the destination MAC address. Each port forms a separate collision domain, reducing collisions and improving bandwidth efficiency.

---

### 6. Full Duplex Transmission Mode

**Full duplex** is a communication mode in which data can be transmitted in **both directions simultaneously** over the link. Each station can send and receive data at the same time (for example, a standard telephone conversation or modern switched Ethernet), doubling effective bidirectional throughput compared to half duplex.

---

### 7. Transmission Media

Transmission media are the physical paths or channels over which signals travel from a sender to a receiver, divided into two broad categories:

* **Guided (Wired) Media:** Twisted-pair cable (UTP/STP), coaxial cable, and optical fiber.
* **Unguided (Wireless) Media:** Radio waves, microwaves, and infrared waves.

---

### 8. Guided Media vs. Unguided Media

| Feature | Guided Media | Unguided Media |
| --- | --- | --- |
| **Signal Path** | Signals are confined within physical cables or fibers. | Signals propagate freely through air, space, or vacuum without a physical guide. |
| **Installation & Mobility** | Higher physical installation effort; devices are tethered by cabling. | Easier to deploy across wide/hard-to-reach areas; supports mobile devices. |
| **Interference & Security** | Generally less prone to external radio interference and easier to physically secure. | More susceptible to environmental interference, attenuation, and eavesdropping without encryption. |

---

### 9. Capacity of a Noisy Channel ($\text{SNR} = 0$, $B = 3000\text{ Hz}$)

By the **Shannon–Hartley theorem**, the maximum channel capacity $C$ (in bits per second) is:

$$C = B \log_2(1 + \text{SNR})$$

Substitute $B = 3000\text{ Hz}$ and $\text{SNR} = 0$:

$$C = 3000 \times \log_2(1 + 0) = 3000 \times \log_2(1) = 3000 \times 0 = 0\text{ bps}$$

The channel capacity is **$0\text{ bps}$** (no information can be reliably transmitted when the signal-to-noise ratio is $0$).

---

### 10. FDMA (Frequency Division Multiple Access)

**FDMA** is a channelization/multiple-access technique in which the total available frequency bandwidth is divided into **non-overlapping frequency sub-bands (channels)**. Each user or signal is assigned a dedicated frequency band for the duration of its transmission, allowing multiple users to transmit simultaneously without interfering with one another's frequency slots.

---

### 11. Switching

**Switching** is the process of forwarding data packets, frames, or circuits from an incoming interface to an appropriate outgoing interface through intermediate network nodes (such as switches or routers) so data reaches its destination across a multi-node network. Common types include **circuit switching**, **packet switching** (datagram and virtual circuit), and **message switching**.

---

### 12. ISDN (Integrated Services Digital Network)

**ISDN** is a set of circuit-switched digital communication standards that transmit voice, video, data, and other network services digitally over traditional public switched telephone network (PSTN) copper lines (or digital trunks). Common interfaces include **Basic Rate Interface (BRI)** and **Primary Rate Interface (PRI)**.