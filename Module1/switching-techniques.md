# Q12. Compare Circuit, Packet, and Message switching techniques with proper diagrams.

## 1. Introduction
**Switching** is the mechanism by which intermediate network nodes (switches/routers) forward data from a source to a destination across a multi-node network without requiring a direct physical cable between every pair of devices.

The three primary switching techniques are:
1. **Circuit Switching**
2. **Packet Switching** (Datagram & Virtual Circuit)
3. **Message Switching**

---

## 2. Circuit Switching
In **Circuit Switching**, a **dedicated physical end-to-end communication path** is established between the sender and receiver *before* any data transfer begins. All bandwidth along that path is exclusively reserved for the entire duration of the session.

### Phases of Circuit Switching
1. **Circuit Establishment:** Setup signals reserve a dedicated path through intermediate switches.
2. **Data Transfer:** Continuous, uninterrupted data flows at a fixed rate with minimal delay.
3. **Circuit Disconnection (Teardown):** Resources are released once communication ends.

```
Sender ----[Switch 1]====(Dedicated Path)====[Switch 2]---- Receiver
       (All intermediate links reserved exclusively during call)
```

* **Pros:** Guaranteed bandwidth, constant delay (no jitter), no packet reordering needed.
* **Cons:** Inefficient bandwidth utilization (idle periods waste reserved links), connection setup delay.
* **Example:** Traditional Public Switched Telephone Network (PSTN).

---

## 3. Message Switching
In **Message Switching**, no dedicated path is established. The **entire message** is treated as a single unit and transmitted hop-by-hop using the **Store-and-Forward** technique.

* **How it works:** Each intermediate node receives the **complete message**, stores it on disk/buffer, checks for errors, and forwards it to the next node when an outgoing link becomes available.

```
Sender ---> [Switch 1: Store & Forward Full Msg] ---> [Switch 2: Store & Forward Full Msg] ---> Receiver
```

* **Pros:** Efficient link utilization (links are shared), no setup delay, supports broadcasting/priority queuing.
* **Cons:** **Very high end-to-end delay** (must wait for full message at every hop), requires huge storage/disk buffers at every switch, **unsuitable for real-time voice/video**.
* **Example:** Legacy telegraph systems, early store-and-forward email relays.

---

## 4. Packet Switching
In **Packet Switching**, the message is split into small, fixed-maximum-size blocks called **packets**. Each packet carries a header (source/destination IP, sequence number) and is forwarded independently across shared network links.

```
               +---> [Router A] ---> [Router C] ---+
Sender (P1,P2) |                                   |---> Receiver (Reassembles P1,P2)
               +---> [Router B] ---> [Router D] ---+
```

### Two Approaches to Packet Switching
1. **Datagram Packet Switching (Connectionless):**
   * Each packet is routed **independently**. Packets of the same message may take different paths and arrive out of order (reassembled at the receiver). Used in the **Internet (IP)**.
2. **Virtual Circuit Packet Switching (Connection-Oriented):**
   * A logical path (**Virtual Circuit**) is set up before data transfer; all packets follow the same route in order, though physical links are still dynamically shared. Used in **ATM / Frame Relay**.

* **Pros:** High bandwidth efficiency (dynamic sharing), high fault tolerance (reroutes around failed links), cost-effective.
* **Cons:** Variable delay (jitter) due to queuing, header overhead, possible packet loss under congestion.
* **Example:** The Modern Internet, Web browsing, VoIP.

---

## 5. Comprehensive Comparison Table

| Feature | Circuit Switching | Message Switching | Packet Switching |
| :--- | :--- | :--- | :--- |
| **Dedicated Physical Path?** | **Yes** (reserved end-to-end) | **No** | **No** *(logical path only in Virtual Circuit)* |
| **Unit of Transfer** | Continuous bit stream | Entire message as one block | Small packets |
| **Store-and-Forward?** | No | **Yes** (disk/large buffer) | **Yes** (RAM/fast router buffers) |
| **Bandwidth Utilization** | Low (wasted during silence) | High | **Very High** (dynamic sharing) |
| **Setup Phase Required?** | **Yes** (before data transfer) | No | No (Datagram) / Yes (Virtual Circuit) |
| **End-to-End Delay** | Setup delay, then constant low delay | **Very High** | Low to Moderate (variable jitter) |
| **Intermediate Storage Need** | None | Very High (disk storage) | Low (fast memory buffers) |
| **Fault Tolerance** | Low (link failure breaks call) | Moderate (can reroute message) | **High** (packets reroute dynamically) |
| **Real-Time Suitability** | Excellent | Poor (too slow) | Good (with QoS) |
| **Examples** | Traditional PSTN telephone | Legacy telegraph / early email | Internet (IP), Web, VoIP |

---

## References & Study Hints
* **Tutorial Reference:** [GeeksforGeeks – Circuit Switching in Computer Network](https://www.geeksforgeeks.org/computer-networks/circuit-switching-in-computer-network/)
* **Video Lecture:** [Neso Academy – Computer Networks Playlist (YouTube)](https://www.youtube.com/hashtag/computernetworksbyneso)
* **Exam Study Hints:**
  * Draw a **separate neat diagram** for each of the three techniques (highlighting the dedicated path in Circuit, Store-and-Forward in Message, and multi-path packets P1/P2 in Packet Switching).
  * Mention **Datagram vs. Virtual Circuit** under Packet Switching and the **3 phases** (Setup, Transfer, Teardown) under Circuit Switching.
