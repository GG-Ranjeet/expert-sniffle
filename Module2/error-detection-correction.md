# Q2. Error Detection and Error Correction Methods in the Data Link Layer

> **Exam Weightage:** 5–10 Marks | **Module 2:** Data Link Layer

---

## 1. Introduction: Why Errors Occur

During transmission across a physical medium, electromagnetic interference, thermal noise, attenuation, and crosstalk can alter transmitted bits:
- **Single-Bit Error:** Only 1 bit of a given data unit is changed (`0` $\rightarrow$ `1` or `1` $\rightarrow$ `0`).
- **Burst Error:** Two or more consecutive/non-consecutive bits in the data unit are changed. Burst errors are much more common in real networks because noise impulses typically last longer than a single bit duration.

To handle these errors, the Data Link Layer adds **redundant bits** (check bits) to the original data using two approaches:
1. **Error Detection:** Detect whether an error occurred; if so, discard the frame and request retransmission (ARQ).
2. **Error Correction (Forward Error Correction – FEC):** Detect the error *and* locate/repair the corrupted bit(s) at the receiver without retransmission.

---

## 2. Error Detection Methods

### 2.1 Simple Parity Check
- **Concept:** A single redundant bit (parity bit) is appended to a $k$-bit data block so that the total number of `1`s in the $(k+1)$-bit codeword is either **even** (Even Parity) or **odd** (Odd Parity).
- **Example (Even Parity):**
  - Data: `1011001` (four `1`s $\rightarrow$ already even) $\rightarrow$ Parity bit = `0` $\rightarrow$ Codeword: `10110010`
  - Data: `1010001` (three `1`s $\rightarrow$ odd) $\rightarrow$ Parity bit = `1` $\rightarrow$ Codeword: `10100011`
- **Capability:** Detects **all single-bit errors** (and any odd number of bit errors). **Fails** if an even number of bits (2, 4, …) are flipped.

### 2.2 Two-Dimensional (2D) Parity Check
- **Concept:** Data is arranged in a matrix of rows and columns. A parity bit is computed for **each row** and **each column**.
- **Capability:** Detects all single-bit, double-bit, and triple-bit errors, and most burst errors up to the column width. Fails only if 4 bits flip in a rectangular pattern (two in one row and two in the exact same columns of another row).

### 2.3 Checksum
- **Concept:** Widely used in upper layers (IPv4, TCP, UDP) and some link protocols.
- **Sender Steps:**
  1. Divide the data into $m$-bit segments (typically 16-bit words).
  2. Add all segments together using **1's complement arithmetic** (wrap any carry-out bit around and add it to the LSB).
  3. Take the **1's complement** (flip all bits) of the final sum $\rightarrow$ this is the **Checksum**.
  4. Append the checksum to the data.
- **Receiver Steps:**
  1. Add all received segments *including* the checksum using 1's complement arithmetic.
  2. Take the 1's complement of the sum.
  3. If the result is **all `0`s**, accept the data; otherwise, reject it.

### 2.4 Cyclic Redundancy Check (CRC)
- **Concept:** The most powerful and widely used error-detection method in Layer 2 (Ethernet, Wi-Fi, HDLC). It treats bit strings as polynomials over $GF(2)$ and uses **modulo-2 binary division (XOR)**.
- **Working:**
  1. Sender and receiver agree on an $(n+1)$-bit **Generator Polynomial** $G(x)$ of degree $n$.
  2. Sender appends $n$ zeros to the $k$-bit data $D$.
  3. Sender divides $D \cdot 2^n$ by $G$ using modulo-2 XOR division to obtain an $n$-bit **Remainder (CRC / FCS)**.
  4. Sender replaces the $n$ zeros with the CRC remainder and transmits the $(k+n)$-bit codeword.
  5. Receiver divides the received codeword by the same $G$.
     - **Remainder = 0** $\rightarrow$ No error detected (accept).
     - **Remainder $\neq$ 0** $\rightarrow$ Error detected (discard / request retransmission).
- **Strength:** Detects all single-bit errors, double-bit errors, any odd number of errors (if $G(x)$ has $(x+1)$ as a factor), and all burst errors of length $\le n$.

---

## 3. Error Correction Methods (Forward Error Correction)

### 3.1 Hamming Distance & Theoretical Bounds
- **Hamming Distance $d(u, v)$:** Number of bit positions in which two equal-length codewords $u$ and $v$ differ.
- **Minimum Hamming Distance ($d_{\min}$):** Smallest Hamming distance between any two valid codewords in a coding scheme.
  - To **detect** up to $s$ bit errors:
    $$d_{\min} \ge s + 1$$
  - To **correct** up to $t$ bit errors:
    $$d_{\min} \ge 2t + 1$$

### 3.2 Hamming Code (Single-Bit Error Correction)
Developed by R. W. Hamming, this block code can **detect up to 2-bit errors** and **automatically correct any single-bit error**.

#### Step 1: Calculate Number of Redundant Bits ($r$)
For $m$ data bits, choose the smallest integer $r$ satisfying:
$$2^r \ge m + r + 1$$
*Example:* For $m = 4$ data bits, $r = 3$ because $2^3 = 8 \ge 4 + 3 + 1 = 8$. Total codeword length = $m + r = 7$ bits (Hamming $(7,4)$ code).

#### Step 2: Position of Parity Bits
Parity bits ($P_1, P_2, P_4, P_8, \dots$) are placed at bit positions that are **powers of 2** ($1, 2, 4, 8, \dots$); data bits fill the remaining positions ($3, 5, 6, 7, \dots$).

#### Step 3: Parity Calculation (Even Parity)
Each parity bit $P_i$ checks all bit positions whose binary representation has a `1` at the $i$-th position:
- **$P_1$ (pos 1):** checks positions $1, 3, 5, 7, 9, \dots$
- **$P_2$ (pos 2):** checks positions $2, 3, 6, 7, 10, 11, \dots$
- **$P_4$ (pos 4):** checks positions $4, 5, 6, 7, 12, \dots$

#### Step 4: Error Detection & Correction at Receiver (Syndrome)
The receiver recomputes parity checks $C_4 C_2 C_1$:
- If $C_4 C_2 C_1 = 000$ $\rightarrow$ **No error**.
- If $C_4 C_2 C_1 \neq 000$ $\rightarrow$ Its binary value directly gives the **exact bit position of the error**. Flipping that bit corrects the error!

*Quick Example:* Suppose 7-bit Hamming code `1010101` (positions 7..1) is sent, and bit at position `5` flips. The receiver computes $C_4 C_2 C_1 = 101_2 = 5$, immediately flips bit 5, and recovers the original data.

---

## 4. Comparison of Error Control Techniques

| Method | Type | Overhead | Burst Error Capability | Common Usage |
| :--- | :--- | :--- | :--- | :--- |
| **Simple Parity** | Detection | 1 bit | Poor (fails on even flips) | Serial links, memory |
| **Checksum** | Detection | 16 bits (typical) | Moderate | IPv4, TCP, UDP |
| **CRC** | Detection | $n$ bits (e.g., 16/32) | Excellent (all bursts $\le n$ bits) | Ethernet, Wi-Fi, USB |
| **Hamming Code** | Detection & Correction | $r$ bits ($2^r \ge m+r+1$) | Corrects 1-bit; detects 2-bit | ECC RAM, satellite/space links |

---

## 5. References & Study Hints

- **GeeksforGeeks – Error Detection in Computer Networks:** [GeeksforGeeks Error Detection](https://vertexaisearch.cloud.google.com/grounding-api-redirect/AUZIYQEjrOBeVM-IoQGt8BrufaFn2rmpfdERHTvzqkrR6Aqwan-R1MLZakjPr8OYFDbeK4JStrVz67DWGziDTnbA1NG-7fp3bco04JGv3VAnMfr8RgfIYf-HJ8gTX9ADUQmcdG3t26vRNdzgbun0io2kySnaNitoNoCF6YQxyPszlpVlvM1L6Dujz4_69-A=)
- **GeeksforGeeks – Hamming Code:** [GeeksforGeeks Hamming Code](https://vertexaisearch.cloud.google.com/grounding-api-redirect/AUZIYQH5VrZspuyJymbq53ZBYsntUiFz6bwL2FPDd01uV_kMbQeNPTwWIjaUI42tv8vnGvtycE9uZBoabUfpZWmhKw0NFATFWiOPB4bhXuMhOdZpCraJ7glNwga2gl1QTGMdtZB1rBa09fNGhrXApvQTDpZKamvepgTiJ2Tf0uJ-mRICAg==)
- **Exam Tip:** Memorize the two Hamming distance formulas ($d_{\min} \ge s+1$ for detection, $d_{\min} \ge 2t+1$ for correction) and the $2^r \ge m+r+1$ inequality—they appear in almost every exam paper.
