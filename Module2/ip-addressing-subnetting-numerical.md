# Q11. IPv4 Addressing & Subnetting Numerical (`200.200.200.200`)

> **Exam Weightage:** 5–10 Marks | **Module 2:** Network Layer

**Question:** If an organization has an IP address **`200.200.200.200`**, find:
- **(i)** Class of IP
- **(ii)** Network ID
- **(iii)** Subnet Mask
- **(iv)** Number of Usable Hosts
- **(v)** Broadcast ID

---

## 1. Step-by-Step Solution

### (i) Class of IP Address
In classful IPv4 addressing, the class is determined by the **first octet** (and its leading bits):
- **Class A:** `0` – `127` (leading bit `0`)
- **Class B:** `128` – `191` (leading bits `10`)
- **Class C:** `192` – `223` (leading bits `110`)
- **Class D:** `224` – `239` (Multicast)
- **Class E:** `240` – `255` (Experimental)

Here, the first octet is **`200`** (binary: `11001000`), which lies in the range `192` – `223` and begins with `110`.
$$\therefore \text{Class of IP} = \mathbf{Class\ C}$$

---

### (ii) Network ID (Network Address)
For a **Class C** IP address:
- The **first 3 octets (24 bits)** represent the **Network portion**.
- The **last octet (8 bits)** represents the **Host portion**.

To find the Network ID, perform a **bitwise AND** between the IP address and the default subnet mask (or set all host bits to `0`):

```text
IP Address    :  200 . 200 . 200 . 200   (11001000.11001000.11001000.11001000)
Subnet Mask   :  255 . 255 . 255 .   0   (11111111.11111111.11111111.00000000)
                 ---------------------   (Bitwise AND)
Network ID    :  200 . 200 . 200 .   0   (11001000.11001000.11001000.00000000)
```

$$\therefore \text{Network ID} = \mathbf{200.200.200.0}$$

---

### (iii) Subnet Mask
Since no custom CIDR prefix is specified, the **default subnet mask** for Class C applies (24 network bits = `1`, 8 host bits = `0`):
- **Dotted-Decimal:** **`255.255.255.0`**
- **CIDR Notation:** **`/24`**

---

### (iv) Number of Usable Hosts
In a Class C network, there are **$h = 8$ host bits** in the last octet:
- **Total IP Addresses:** $2^8 = 256$ (`200.200.200.0` to `200.200.200.255`)
- **Reserved Addresses:** $2$ addresses cannot be assigned to hosts:
  1. `200.200.200.0` (Network ID)
  2. `200.200.200.255` (Broadcast ID)
- **Number of Usable Hosts:**
  $$\text{Usable Hosts} = 2^h - 2 = 2^8 - 2 = 256 - 2 = \mathbf{254}$$
- **Usable Host IP Range:** `200.200.200.1` to `200.200.200.254`

---

### (v) Broadcast ID (Broadcast Address)
To find the Broadcast ID, set all **host bits** (the last 8 bits) to **`1`**:

```text
Network Portion :  200 . 200 . 200   (11001000.11001000.11001000)
Host Portion    :  255               (11111111)
Broadcast ID    :  200 . 200 . 200 . 255
```

$$\therefore \text{Broadcast ID} = \mathbf{200.200.200.255}$$

---

## 2. Final Answer Summary Table

| Parameter | Answer |
| :--- | :--- |
| **(i) Class of IP** | **Class C** |
| **(ii) Network ID** | **`200.200.200.0`** |
| **(iii) Subnet Mask** | **`255.255.255.0`** (`/24`) |
| **(iv) Number of Usable Hosts** | **`254`** (`200.200.200.1` – `200.200.200.254`) |
| **(v) Broadcast ID** | **`200.200.200.255`** |

---

## 3. References & Study Hints

- **GeeksforGeeks – IPv4 Classful & Subnetting:** [GeeksforGeeks Subnetting](https://vertexaisearch.cloud.google.com/grounding-api-redirect/AUZIYQE4GH5Mp60SVYi0f-iwy1-S24L0dLGzH1nanx8s-6-a5XIkehGqvRdpronezD7IQ-QxBkh2NXFok5_4fmBEUgjcMfr62JZO2M-TnoZY74Lg0X5zU3jxo-DUgkwsVz9C2YrspQ2lxzGa8r4lMwJtEJLQNxl-3jf-uEzT01_k6PBZranhL50avKraPtNfgJEwAaiUUs2WrGRsmGsap7E=)
- **Exam Tip:** Always show the formula $2^h - 2$ explicitly and state why $2$ addresses are subtracted (Network ID and Broadcast ID).
