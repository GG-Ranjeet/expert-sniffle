# 5. UDP Header Format

## Introduction

The **User Datagram Protocol (UDP)**—standardized in **RFC 768**—is a lightweight, connectionless, and unreliable ("best-effort") transport-layer protocol. Unlike TCP, UDP does not perform handshaking, sequencing, flow control, or congestion control, making it ideal for latency-sensitive applications such as **DNS, DHCP, VoIP, online gaming, and live video streaming**.

Because of its simplicity, the UDP header has a **fixed size of only 8 bytes (64 bits)**, consisting of four 16-bit (2-byte) fields.

---

## UDP Header Format Diagram (32-bit Wide Grid)

```text
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|          Source Port          |       Destination Port        |  Row 1 (4 B)
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|            Length             |           Checksum            |  Row 2 (4 B)
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                                                               |
|                        Data (Payload)                         |
|                              ...                              |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

---

## Detailed Explanation of the 4 UDP Header Fields

| Field | Size | Description |
| :--- | :--- | :--- |
| **Source Port** | 16 bits (2 bytes) | Identifies the sending process's port number on the source host (range `0`–`65535`).<br>• **Optional in UDP:** If the sender does not expect a reply, this field may be set to all zeros (`0x0000`). |
| **Destination Port** | 16 bits (2 bytes) | Identifies the target application process on the destination host (e.g., Port `53` for DNS, `67/68` for DHCP, `69` for TFTP, `161` for SNMP).<br>• **Mandatory:** Required for demultiplexing the datagram at the receiver. |
| **Length (Total Length)** | 16 bits (2 bytes) | Specifies the **total length in bytes** of the entire UDP datagram (**8-byte header + payload data**).<br>• **Minimum value:** `8` bytes (when payload is 0 bytes).<br>• **Maximum theoretical value:** `65,535` bytes (though practically limited to `65,507` bytes of payload inside IPv4: $65,535 - 20\text{ B IP header} - 8\text{ B UDP header}$). |
| **Checksum** | 16 bits (2 bytes) | Used for error detection over the **UDP header**, **UDP payload**, and a **12-byte IP pseudo-header** (Source IP, Destination IP, Protocol=17, UDP Length).<br>• **IPv4:** Optional (set to `0x0000` if not computed).<br>• **IPv6:** **Mandatory** (cannot be skipped because IPv6 has no network-layer header checksum). |

---

## UDP Pseudo-Header (Used in Checksum Calculation)

Even though UDP does not include IP addresses in its 8-byte header, the checksum calculation prepends a conceptual **pseudo-header** from the IP layer to detect misrouted packets:

```text
+-----------------------------------+-----------------------------------+
|                   Source IP Address (32 bits / 4 B)                   |
+-----------------------------------+-----------------------------------+
|                Destination IP Address (32 bits / 4 B)                 |
+-----------------+-----------------+-----------------------------------+
|  Zeros (8 bits) | Protocol = 17   |        UDP Length (16 bits)       |
+-----------------+-----------------+-----------------------------------+
```

---

## Why is the UDP Header So Small? (TCP vs. UDP Header Comparison)

| Feature | UDP Header | TCP Header |
| :--- | :--- | :--- |
| **Header Size** | Fixed **8 bytes** | Variable **20 to 60 bytes** |
| **Number of Fields** | **4 fields** | **11+ fields** |
| **Sequence / ACK Numbers** | Absent | Present (32 bits each) |
| **Flow Control (Window)** | Absent | Present (16 bits) |
| **Control Flags** | Absent | Present (`URG, ACK, PSH, RST, SYN, FIN`) |
| **Overhead** | Minimal (fast, low latency) | Higher (ensures reliability & ordering) |

---

## References & Study Hints

* **RFC 768 (UDP Specification):** [https://www.rfc-editor.org/info/rfc768/](https://www.rfc-editor.org/info/rfc768/)
* **YouTube Lecture (Neso Academy — UDP Header Format):** [https://www.youtube.com/watch?v=zrOtIj7ONdg](https://www.youtube.com/watch?v=zrOtIj7ONdg)
* **Exam Tip (5–10 Marks):** Draw the 2-row (8-byte) header diagram, clearly state the 16-bit width of each field, highlight the formula $\text{UDP Length} = 8 + \text{Data Length}$ (minimum = 8), and note that the Checksum is **optional in IPv4** but **mandatory in IPv6**.
