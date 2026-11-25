# Q14. Network Congestion, Congestion Control & Leaky Bucket Algorithm

> **Exam Weightage:** 8–10 Marks | **Module 2:** Network Layer

---

## 1. What is Congestion?

**Congestion** is a state in a network where **too many packets are present in the subnet simultaneously**, exceeding the capacity of routers and links. As a result:
- Router buffers overflow and **packets are dropped**.
- **Queuing delays** increase sharply.
- **Throughput collapses** (often called *congestion collapse*) because senders retransmit dropped packets, adding even more load to an already overloaded network.

---

## 2. Congestion Control Mechanisms

Congestion control techniques fall into two broad categories:

### 2.1 Open-Loop Congestion Control (Prevention)
Designed to **prevent** congestion before it happens using good network design (no runtime feedback):
- **Retransmission Policy:** Careful timeout tuning to avoid unnecessary duplicate packets.
- **Window Policy:** Selective Repeat ARQ avoids resending already-received packets (unlike Go-Back-N).
- **Acknowledgment Policy:** Piggybacking and delayed ACKs reduce control-packet overhead.
- **Traffic Shaping:** Regulates the rate and burstiness of packets entering the network (e.g., **Leaky Bucket**, **Token Bucket**).

### 2.2 Closed-Loop Congestion Control (Detection & Recovery)
Detects congestion **at runtime** and notifies sources to slow down:
- **Backpressure:** A congested router tells its upstream neighbor to slow down, propagating back toward the source.
- **Choke Packet:** A congested router sends an explicit control packet directly back to the source telling it to reduce its transmission rate.
- **Implicit Signaling:** The source infers congestion from packet loss or rising RTT (e.g., TCP congestion control).
- **Explicit Congestion Notification (ECN):** Routers set ECN bits in the IP header to warn the receiver/sender before dropping packets.

---

## 3. Leaky Bucket Algorithm

### Concept
The **Leaky Bucket Algorithm** is a **traffic-shaping** mechanism that converts **irregular, bursty input traffic** into a **smooth, constant-rate output stream**.

**Analogy:** Imagine a bucket with a small hole at the bottom:
- Water (packets) can pour into the bucket at any irregular/bursty rate.
- Water leaks out of the hole at a **fixed, constant rate ($r$)**.
- If the bucket is full (capacity $B$) and more water arrives, the excess water **overflows (packets are dropped)**.

```text
   Bursty Input Traffic (Variable Rate)
          |  |  |  |
          v  v  v  v
      +----------------+
      |  Bucket /      |  ---> Overflow (Packets Dropped if Full)
      |  FIFO Queue    |
      |  (Capacity B)  |
      +-------+--------+
              |
              v  Constant Output Rate (r)
      Smooth, Steady Traffic to Network
```

### Working Steps
1. A host/router maintains a finite **FIFO queue (bucket)** of size $B$ (in bytes or packets).
2. When a packet arrives:
   - If the bucket has space $\rightarrow$ place the packet at the tail of the queue.
   - If the bucket is full $\rightarrow$ **discard (drop)** the packet.
3. At every clock tick, the bucket transmits packets at a **constant rate $r$** (e.g., $1$ packet or $L$ bytes per tick), regardless of how bursty the input was.

---

## 4. Limitations of the Leaky Bucket Algorithm

1. **No Burst Tolerance (Rigid Output Rate):** Even when the network is completely idle, the leaky bucket strictly enforces the constant rate $r$ and cannot temporarily speed up to clear a burst.
2. **Inefficient Bandwidth Utilization:** Idle network capacity during low-traffic periods goes wasted because saved capacity cannot be "banked" for future bursts.
3. **Packet Dropping During Bursts:** Large legitimate bursts overflow the fixed bucket and are dropped, even if downstream bandwidth is available.
4. **Added Queuing Delay (Latency):** Packets arriving in a burst must wait in the queue to leak out, hurting delay-sensitive real-time apps (VoIP, gaming, live video).

---

## 5. How Limitations Are Resolved: The Token Bucket Algorithm

The **Token Bucket Algorithm** resolves the rigidity of the Leaky Bucket by allowing **controlled bursts** while still enforcing a long-term average rate:

- **How it works:**
  - Tokens are generated at a constant rate $r$ and placed into a bucket of capacity $B$.
  - To transmit a packet (or $L$ bytes), the host must **remove a token** from the bucket.
  - During idle periods, **unused tokens accumulate** up to capacity $B$.
  - When a sudden burst arrives, the host can spend all accumulated tokens at once to transmit at a **high burst rate**, after which it is limited to the token generation rate $r$.
- **Result:** Eliminates unnecessary packet drops and queuing delays during short bursts while still protecting the network from sustained overload.

| Feature | Leaky Bucket | Token Bucket |
| :--- | :--- | :--- |
| **Output Rate** | Strictly **constant** | **Allows controlled bursts** |
| **Idle Bandwidth** | Wasted | Saved as tokens (up to $B$) |
| **Delay on Bursts** | Higher (strict queuing) | Lower (if tokens are available) |

---

## 6. References & Study Hints

- **GeeksforGeeks – Leaky Bucket & Token Bucket:** [GeeksforGeeks Congestion Control](https://vertexaisearch.cloud.google.com/grounding-api-redirect/AUZIYQHOPydE7AtTsSqR9dIOdo54mxq8eLnCYBXqb6I_qnVHTY8Df908RjAUsFgYO-I44zha4XV9Z1xNwFxadxRlzR7-F1_qWAwOrnFIErTsP3xgwH2tFO2kiQDlNKS6awJu-QZhBforYBpCt5toRdIj03gzVyhOr3a8ubK1xikXiQ==)
- **TutorialsPoint – Congestion Control:** [TutorialsPoint Leaky Bucket](https://vertexaisearch.cloud.google.com/grounding-api-redirect/AUZIYQEr86yogRa2nDfh7p3mOwbV5RJKO_pLVKXhhT0qmuzf2kD0ZnStFzw7o4d-eq0uSlK6GJnZnfRW66QU3002dYDSgilBDL5rWfsFCro41bdYSFoccwmawSdeQuB2djZejLg8MPOqYzRo7NT-O6wfL15_Yewsc0N9YObtg5ocAuGAD4wJehdQ2BxT3JGID4DdGejq2qlM9ww069d5)
- **Exam Tip:** Always draw the **Leaky Bucket diagram** and explicitly contrast it with **Token Bucket** when explaining how its limitations are resolved.
