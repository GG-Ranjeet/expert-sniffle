# 4. TCP Header Format

## Introduction

The **Transmission Control Protocol (TCP)**—standardized in **RFC 793** (updated by RFC 9293)—is a connection-oriented, reliable transport-layer protocol. Every TCP segment consists of a **TCP Header** followed by an optional **Data Payload**.

The TCP header has a **minimum size of 20 bytes** (5 rows × 32 bits) and a **maximum size of 60 bytes** (when up to 40 bytes of Options are included).

---

## TCP Header Format Diagram (32-bit Wide Grid)

```text
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|          Source Port          |       Destination Port        |  Row 1 (4 B)
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                        Sequence Number                        |  Row 2 (4 B)
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Acknowledgment Number                      |  Row 3 (4 B)
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|  Data |           |U|A|P|R|S|F|                               |
| Offset| Reserved  |R|C|S|S|Y|I|          Window Size          |  Row 4 (4 B)
| (4 b) |  (6 b)    |G|K|H|T|N|N|                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|           Checksum            |         Urgent Pointer        |  Row 5 (4 B)
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Options (0 to 40 bytes)                    |  (Optional)
|                   + Padding (to 32-bit align)                 |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                             Data                              |
|                       (Application Payload)                   |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

---

## Detailed Explanation of TCP Header Fields

| Field | Size | Description |
| :--- | :--- | :--- |
| **Source Port** | 16 bits | Identifies the sending application process (port number) on the source host. |
| **Destination Port** | 16 bits | Identifies the receiving application process (port number) on the destination host (e.g., 80 for HTTP, 443 for HTTPS). |
| **Sequence Number** | 32 bits | • If `SYN = 1`: Contains the **Initial Sequence Number (ISN)**.<br>• If `SYN = 0`: Indicates the byte number of the **first data byte** in this segment, enabling in-order reassembly and duplicate detection. |
| **Acknowledgment Number** | 32 bits | Valid only when `ACK = 1`. Specifies the **next sequence number** the receiver expects to receive (`Last Received Byte + 1`), acting as a cumulative acknowledgment. |
| **Data Offset (HLEN)** | 4 bits | Specifies the length of the TCP header in **32-bit words (4-byte chunks)**. Tells the receiver where the payload begins.<br>• Minimum value: `5` ($5 \times 4 = 20\text{ bytes}$).<br>• Maximum value: `15` ($15 \times 4 = 60\text{ bytes}$). |
| **Reserved** | 6 bits | Reserved for future use; must be set to `0` (in modern RFCs, 3 of these bits are used for ECN: `NS`, `CWR`, `ECE`). |
| **Control Flags** | 6 bits | Six 1-bit flags that control connection state and segment handling (detailed below). |
| **Window Size** | 16 bits | Used for **flow control**. Indicates the size of the receiver's available buffer (receive window `rwnd`) in bytes (up to $65,535$ bytes without window scaling). |
| **Checksum** | 16 bits | Mandatory error-detection field computed over the **TCP header**, **TCP payload**, and a **12-byte IP pseudo-header** (Source IP, Dest IP, Protocol=6, TCP Length). |
| **Urgent Pointer** | 16 bits | Valid only when `URG = 1`. Holds a positive offset added to the Sequence Number to mark the end of urgent (out-of-band) data. |
| **Options & Padding** | 0–40 bytes | Variable-length field (multiple of 32 bits via zero-padding) used for **MSS (Maximum Segment Size)**, **Window Scaling**, **SACK (Selective ACK)**, and **Timestamps**. |

---

## Control Flags (6 Bits)

1. **`URG` (Urgent):** Signals that the Urgent Pointer field is active and urgent data is present.
2. **`ACK` (Acknowledgment):** Indicates that the Acknowledgment Number field is valid (set on all segments after the initial `SYN`).
3. **`PSH` (Push):** Instructs the receiving TCP stack to push buffered data immediately to the application without waiting for the buffer to fill.
4. **`RST` (Reset):** Abruptly terminates a corrupted, invalid, or refused connection.
5. **`SYN` (Synchronize):** Used during connection establishment (3-way handshake) to synchronize Initial Sequence Numbers.
6. **`FIN` (Finish):** Indicates the sender has finished transmitting data and requests connection termination.

---

## Key Numerical Facts for Exams

* **Minimum Header Size:** $20\text{ bytes}$ (`HLEN = 5` $\rightarrow 5 \times 4 = 20\text{ B}$).
* **Maximum Header Size:** $60\text{ bytes}$ (`HLEN = 15` $\rightarrow 15 \times 4 = 60\text{ B}$).
* **Maximum Options Size:** $60 - 20 = 40\text{ bytes}$.
* **Maximum Sequence Numbers:** $2^{32} \approx 4.29 \times 10^9$ bytes before wrap-around.

---

## References & Study Hints

* **RFC 793 (TCP Specification):** [https://www.rfc-editor.org/info/rfc793/](https://www.rfc-editor.org/info/rfc793/)
* **GeeksforGeeks — Services and Segment Structure in TCP:** [https://www.geeksforgeeks.org/computer-networks/services-and-segment-structure-in-tcp/](https://www.geeksforgeeks.org/computer-networks/services-and-segment-structure-in-tcp/)
* **YouTube Lecture (Neso Academy — TCP Header Format):** [https://www.youtube.com/watch?v=gRINp9gh2nM](https://www.youtube.com/watch?v=gRINp9gh2nM)
* **Exam Tip (5–10 Marks):** Always draw the 32-bit wide header diagram accurately (5 fixed rows + Options), state the exact bit widths of all fields, explain all 6 flags (`URG`, `ACK`, `PSH`, `RST`, `SYN`, `FIN`), and mention the `HLEN` scaling factor ($\times 4$ bytes) giving 20–60 bytes.
