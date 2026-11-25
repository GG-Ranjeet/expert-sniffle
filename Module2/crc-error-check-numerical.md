# Q5. CRC Error Detection Numerical Problem

> **Exam Weightage:** 5–10 Marks | **Module 2:** Data Link Layer

**Question:** The code word is received as `1100100101011`. Check whether there are errors in the received code word if the divisor is `10101`.

---

## 1. Method for CRC Error Verification at Receiver

At the receiver side, the incoming codeword is divided by the **same divisor (`10101`)** using **modulo-2 (XOR) binary division**:
- **If Remainder = `0000` (all zeros):** No error detected; the codeword is accepted.
- **If Remainder $\neq$ `0000` (non-zero):** An error occurred during transmission; the codeword is rejected.

**Given:**
- **Received Codeword:** `1100100101011` (13 bits)
- **Divisor ($G$):** `10101` (5 bits, degree $k = 4$)
- **Expected Remainder Length:** $4$ bits

*(Note: Do NOT append extra zeros at the receiver; divide the received codeword directly.)*

---

## 2. Step-by-Step Modulo-2 Binary Division

We divide `1100100101011` by `10101`:

```text
                    1 1 1 1 1 0 0 0 1   <-- Quotient
              _______________________
    1 0 1 0 1 ) 1 1 0 0 1 0 0 1 0 1 0 1 1
              ^ 1 0 1 0 1
              -----------
                0 1 1 0 0 0               (01100 + drop 0 -> 11000)
                ^ 1 0 1 0 1
                -----------
                  0 1 1 0 1 0             (01101 + drop 0 -> 11010)
                  ^ 1 0 1 0 1
                  -----------
                    0 1 1 1 1 1           (01111 + drop 1 -> 11111)
                    ^ 1 0 1 0 1
                    -----------
                      0 1 0 1 0 0         (01010 + drop 0 -> 10100)
                      ^ 1 0 1 0 1
                      -----------
                        0 0 0 0 1 1       (00001 + drop 1 -> 00011)
                        ^ 0 0 0 0 0
                        -----------
                          0 0 0 1 1 0     (00011 + drop 0 -> 00110)
                          ^ 0 0 0 0 0
                          -----------
                            0 0 1 1 0 1   (00110 + drop 1 -> 01101)
                            ^ 0 0 0 0 0
                            -----------
                              0 1 1 0 1 1 (01101 + drop 1 -> 11011)
                              ^ 1 0 1 0 1
                              -----------
                                0 1 1 1 0 <-- Remainder = 1110 (last 4 bits)
```

---

## 3. Step-by-Step Verification Table

| Step | Current 5-Bit Window | Leading Bit | Operation | XOR Result (4 bits) | Next Bit Dropped |
| :---: | :---: | :---: | :---: | :---: | :---: |
| 1 | `11001` | `1` | `11001 ^ 10101` | `1100` | `0` |
| 2 | `11000` | `1` | `11000 ^ 10101` | `1101` | `0` |
| 3 | `11010` | `1` | `11010 ^ 10101` | `1111` | `1` |
| 4 | `11111` | `1` | `11111 ^ 10101` | `1010` | `0` |
| 5 | `10100` | `1` | `10100 ^ 10101` | `0001` | `1` |
| 6 | `00011` | `0` | `00011 ^ 00000` | `0011` | `0` |
| 7 | `00110` | `0` | `00110 ^ 00000` | `0110` | `1` |
| 8 | `01101` | `0` | `01101 ^ 00000` | `1101` | `1` |
| 9 | `11011` | `1` | `11011 ^ 10101` | **`1110`** | *(End)* |

---

## 4. Conclusion

- **Remainder Obtained:** **`1110`**
- Since the remainder `1110` $\neq$ `0000` (non-zero), **errors ARE present in the received codeword `1100100101011`**.
- The receiver will **discard** the frame and request retransmission.

---

## 5. References & Study Hints

- **GeeksforGeeks – Modulo-2 Division & CRC:** [GeeksforGeeks CRC Guide](https://vertexaisearch.cloud.google.com/grounding-api-redirect/AUZIYQEjrOBeVM-IoQGt8BrufaFn2rmpfdERHTvzqkrR6Aqwan-R1MLZakjPr8OYFDbeK4JStrVz67DWGziDTnbA1NG-7fp3bco04JGv3VAnMfr8RgfIYf-HJ8gTX9ADUQmcdG3t26vRNdzgbun0io2kySnaNitoNoCF6YQxyPszlpVlvM1L6Dujz4_69-A=)
- **Exam Tip:** A common mistake is appending zeros at the receiver—remember that zeros are ONLY appended at the sender when *generating* the CRC, never at the receiver when *checking* a received codeword.
