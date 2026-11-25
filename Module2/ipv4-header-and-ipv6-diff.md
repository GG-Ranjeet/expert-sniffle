# Q10. IPv4 Header Format and Differences Between IPv4 and IPv6

> **Exam Weightage:** 8–10 Marks | **Module 2:** Network Layer

---

## 1. IPv4 Header Format (Neat Diagram)

An IPv4 header has a **minimum size of 20 bytes** (5 rows $\times$ 4 bytes) and can extend up to **60 bytes** when Options are included.

```text
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|Version|  IHL  |Type of Service|          Total Length         |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|         Identification        |Flags|      Fragment Offset    |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|  Time to Live |    Protocol   |         Header Checksum       |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                       Source IP Address                       |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Destination IP Address                     |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Options (0 - 40 bytes)     |    Padding    |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

---

## 2. Function of Each IPv4 Header Field

1. **Version (4 bits):** Indicates the IP version (`0100` = `4` for IPv4).
2. **IHL – Internet Header Length (4 bits):** Specifies the length of the IPv4 header in **32-bit (4-byte) words**.
   - Minimum value = `5` ($5 \times 4 = 20$ bytes, no options).
   - Maximum value = `15` ($15 \times 4 = 60$ bytes).
3. **Type of Service (ToS) / DSCP & ECN (8 bits):** Specifies Quality of Service (QoS) priority (e.g., low delay, high throughput for voice/video) and Explicit Congestion Notification.
4. **Total Length (16 bits):** Total size of the entire IPv4 packet (**header + payload**) in bytes. Maximum packet size = $2^{16} - 1 = 65,535$ bytes.
5. **Identification (16 bits):** A unique 16-bit number assigned by the sender to identify all fragments belonging to the same original datagram.
6. **Flags (3 bits):** Controls fragmentation:
   - Bit 0: Reserved (always `0`).
   - Bit 1 (**DF – Don't Fragment**): If `1`, routers must not fragment the packet.
   - Bit 2 (**MF – More Fragments**): `1` for all fragments except the last fragment (`0`).
7. **Fragment Offset (13 bits):** Indicates the position of a fragment's payload relative to the start of the original unfragmented payload, measured in **8-byte units**.
8. **Time to Live – TTL (8 bits):** Limits packet lifetime (hop count). Each router decrements TTL by `1`; if TTL reaches `0`, the packet is discarded and an ICMP Time Exceeded message is sent back—preventing infinite routing loops.
9. **Protocol (8 bits):** Identifies the upper-layer protocol encapsulated in the payload (e.g., `1` = ICMP, `6` = TCP, `17` = UDP).
10. **Header Checksum (16 bits):** 1's complement checksum covering **only the IPv4 header**. Because TTL is decremented at every hop, **every router must recompute the header checksum**.
11. **Source IP Address (32 bits):** Logical IPv4 address of the sending host.
12. **Destination IP Address (32 bits):** Logical IPv4 address of the final receiving host.
13. **Options & Padding (0–40 bytes):** Optional fields for security, record route, or timestamping; **Padding** adds `0` bits so the header ends on a 32-bit boundary.

---

## 3. Major Differences Between IPv4 and IPv6

| Feature | IPv4 | IPv6 |
| :--- | :--- | :--- |
| **Address Size** | **32-bit** (~4.3 billion addresses) | **128-bit** ($3.4 \times 10^{38}$ addresses) |
| **Address Notation** | Dotted-decimal (`192.168.1.1`) | Colon-hexadecimal (`2001:db8::1`) |
| **Header Size** | Variable (**20–60 bytes**) | **Fixed 40 bytes** (streamlined; uses Extension Headers) |
| **Header Fields** | 12+ fields | 8 fields (simpler, faster router processing) |
| **Header Checksum** | **Present** (recomputed at every router hop) | **Removed** (relies on Layer 2 & Layer 4 checksums) |
| **Fragmentation** | Performed by **sender AND intermediate routers** | Performed **ONLY by sender** (via Path MTU Discovery) |
| **Configuration** | Manual or **DHCP** | **SLAAC** (Stateless Address Autoconfiguration) or DHCPv6 |
| **Security (IPsec)** | Optional | **Built-in / natively supported** |
| **Broadcast** | Supported | **Eliminated** (replaced by Multicast & Anycast) |
| **QoS Support** | Basic (ToS field) | Enhanced (**Traffic Class** and **Flow Label** fields) |
| **NAT Requirement** | Heavily required due to address exhaustion | Not required (ample global public addresses) |

---

## 4. References & Study Hints

- **GeeksforGeeks – IPv4 Header Format:** [GeeksforGeeks IPv4 Header](https://vertexaisearch.cloud.google.com/grounding-api-redirect/AUZIYQG4-FbBsoPw0h1Lq6T2Bhp2ouXRivuhX9jvc-PUQqYie4HShYtASJKG5IVab-DRbsVIMLNHj3p-_sMAoPrCz8264kdgV8J3lV9QRxwlNJris04M7wTn7HqqfAxEc6wInNMg7CBTovPKboiLWqr5-xMWdTbVhR9xwhABfQ5Az98f7vV0fA==)
- **GeeksforGeeks – Differences Between IPv4 and IPv6:** [GeeksforGeeks IPv4 vs IPv6](https://vertexaisearch.cloud.google.com/grounding-api-redirect/AUZIYQFUPB0qpYOk9DrT0dN8qRc9muEZIn-VlEkPAqWXy-OHZlyAOR7MlHIQIX8zBtLM9ks9iONG7_WghJu7tf9e9mhy4S8VlAcB9dhA46LPiYPN5yzMnZfGjT2sA0RVTgJRZoTVdJ09OJeJOIAv2XRZSX9poIPGnJFLjSyq1aOrH6P9i6EBn1vFQe0K)
- **Exam Tip:** Practice drawing the **32-bit-wide IPv4 header box** cleanly with bit markers `0..31` on top—neatly aligned boxes earn top marks!
