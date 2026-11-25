# Q13. Write short notes on LAN Protocols and ISDN.

---

## Part 1: LAN Protocols
**LAN (Local Area Network) Protocols** are standardized rules operating primarily at the **Physical Layer (Layer 1)** and **Data Link Layer (Layer 2)** of the OSI model. They govern how devices within a local area (office, building, or campus) share a communication medium, format frames, and address hardware using **MAC addresses**.

The **IEEE 802** committee standardized the major LAN protocols, splitting the Data Link Layer into two sublayers:
* **LLC (Logical Link Control — IEEE 802.2):** Provides framing, flow control, and error control to upper layers.
* **MAC (Medium Access Control):** Controls physical channel access and hardware addressing.

### Major LAN Protocols
1. **Ethernet (IEEE 802.3):**
   * The most widely used wired LAN standard.
   * Uses **Bus** (legacy coaxial) or **Star** (modern twisted-pair/fiber with switches) topology.
   * Employs **CSMA/CD** (Carrier Sense Multiple Access with Collision Detection) on shared media.
   * Supports speeds from **10 Mbps** up to **10 Gbps / 100+ Gbps**.
2. **Wireless LAN / Wi-Fi (IEEE 802.11):**
   * Uses radio waves (2.4 GHz, 5 GHz, 6 GHz) for wireless local networking.
   * Employs **CSMA/CA** (Collision Avoidance) with RTS/CTS and ACKs to handle hidden nodes.
3. **Token Ring (IEEE 802.5):**
   * Uses a **physical Star** (via MAU) and **logical Ring** topology.
   * Access is controlled by a circulating **token**—only the station holding the token can transmit, preventing collisions entirely (4 Mbps / 16 Mbps).
4. **FDDI (Fiber Distributed Data Interface):**
   * High-speed (**100 Mbps**) optical fiber LAN/backbone standard using a **dual-ring** architecture (primary + secondary backup ring) with token passing for high fault tolerance.

---

## Part 2: ISDN (Integrated Services Digital Network)
**ISDN** is a set of international digital communication standards developed by **ITU-T** that enables **simultaneous end-to-end digital transmission of voice, data, text, and video** over traditional Public Switched Telephone Network (PSTN) copper lines.

### Key Channels in ISDN
* **B-Channel (Bearer Channel — 64 kbps):** Carries user data, digitized voice, or video.
* **D-Channel (Data/Signaling Channel — 16 kbps or 64 kbps):** Carries out-of-band control/signaling information (call setup, routing, teardown) and low-speed packet data.
* **H-Channel (Hybrid Channel):** High-speed channels (e.g., H0 = 384 kbps, H11 = 1536 kbps) for high-bandwidth applications like videoconferencing.

### ISDN User-Network Interfaces
1. **BRI (Basic Rate Interface):**
   * Designed for homes and small offices.
   * Consists of **$2\text{B} + 1\text{D}$** channels: two 64 kbps B-channels + one 16 kbps D-channel = **144 kbps** total user/signaling rate (128 kbps usable data).
2. **PRI (Primary Rate Interface):**
   * Designed for large enterprises and PBXs.
   * **North America / Japan (T1-based):** **$23\text{B} + 1\text{D}$** (64 kbps D-channel) = **1.544 Mbps**.
   * **Europe / International (E1-based):** **$30\text{B} + 1\text{D}$** (64 kbps D-channel) = **2.048 Mbps**.

```
ISDN BRI (2B + D):  [ 64 kbps B ] + [ 64 kbps B ] + [ 16 kbps D (Signaling) ] = 144 kbps
ISDN PRI (23B + D): [ 23 x 64 kbps B ] + [ 64 kbps D (Signaling) ]            = 1.544 Mbps
```

### Services & Advantages of ISDN
* **Integrated Services:** Single digital line carries voice, fax, internet data, and video simultaneously.
* **Fast Call Setup:** Out-of-band D-channel signaling sets up calls in ~1–2 seconds.
* **Clear Digital Quality:** Eliminates analog noise and modem handshaking delays.

---

## References & Study Hints
* **Tutorial References:**
  * [GeeksforGeeks – LAN Full Form & Overview](https://www.geeksforgeeks.org/computer-networks/lan-full-form/)
  * [GeeksforGeeks – Difference between Token Ring and Ethernet](https://www.geeksforgeeks.org/computer-networks/difference-between-token-ring-and-ethernet/)
  * [GeeksforGeeks – ISDN Protocol Architecture](https://www.geeksforgeeks.org/computer-networks/isdn-protocol-architecture/)
* **Video Lecture:** [Neso Academy – Computer Networks Playlist (YouTube)](https://www.youtube.com/hashtag/computernetworksbyneso)
* **Exam Study Hints:**
  * For **LAN Protocols**, mention **IEEE 802.3 (Ethernet), 802.5 (Token Ring), 802.11 (Wi-Fi), and FDDI** along with their access methods.
  * For **ISDN**, always write the exact **B and D channel** bit rates and **BRI ($2\text{B}+\text{D}$) vs. PRI ($23\text{B}+\text{D}$ / $30\text{B}+\text{D}$)** formulas.
