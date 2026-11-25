# Q3. Hamming Distance Numerical Problem

> **Exam Weightage:** 5 Marks | **Module 2:** Data Link Layer

**Question:** Find the Hamming distance between the following two pairs of words:
- **(a)** `000` and `011`
- **(b)** `10101` and `11110`

---

## 1. Definition of Hamming Distance

The **Hamming distance** $d(x, y)$ between two binary words $x$ and $y$ of equal length is the **number of bit positions in which the two words differ**.

Mathematically, it is computed by taking the bitwise **XOR** ($\oplus$) of the two words and counting the number of `1`s (the **Hamming weight**) in the resulting word:
$$d(x, y) = w(x \oplus y)$$

**XOR Truth Table Reminder:**
- $0 \oplus 0 = 0$ (bits are same)
- $1 \oplus 1 = 0$ (bits are same)
- $0 \oplus 1 = 1$ (bits differ)
- $1 \oplus 0 = 1$ (bits differ)

---

## 2. Part (a): `000` and `011`

### Step 1: Align the words bit-by-bit
```text
Word 1 (x) :  0   0   0
Word 2 (y) :  0   1   1
              ---------  (XOR)
x XOR y    :  0   1   1
```

### Step 2: Count the differing positions (`1`s in XOR result)
- Position 1 (leftmost): `0` vs `0` $\rightarrow$ Same (`0`)
- Position 2: `0` vs `1` $\rightarrow$ **Different (`1`)**
- Position 3 (rightmost): `0` vs `1` $\rightarrow$ **Different (`1`)**

Total number of `1`s in `011` = **2**.

$$\mathbf{d(000,\ 011) = 2}$$

---

## 3. Part (b): `10101` and `11110`

### Step 1: Align the words bit-by-bit
```text
Word 1 (x) :  1   0   1   0   1
Word 2 (y) :  1   1   1   1   0
              -----------------  (XOR)
x XOR y    :  0   1   0   1   1
```

### Step 2: Count the differing positions (`1`s in XOR result)
- Position 1 (leftmost): `1` vs `1` $\rightarrow$ Same (`0`)
- Position 2: `0` vs `1` $\rightarrow$ **Different (`1`)**
- Position 3: `1` vs `1` $\rightarrow$ Same (`0`)
- Position 4: `0` vs `1` $\rightarrow$ **Different (`1`)**
- Position 5 (rightmost): `1` vs `0` $\rightarrow$ **Different (`1`)**

Total number of `1`s in `01011` = **3**.

$$\mathbf{d(10101,\ 11110) = 3}$$

---

## 4. Final Answer Summary

| Pair | Word 1 | Word 2 | Bitwise XOR | Hamming Distance |
| :--- | :---: | :---: | :---: | :---: |
| **(a)** | `000` | `011` | `011` | **2** |
| **(b)** | `10101` | `11110` | `01011` | **3** |

---

## 5. References & Study Hints

- **GeeksforGeeks – Hamming Distance:** [GeeksforGeeks Hamming Distance](https://vertexaisearch.cloud.google.com/grounding-api-redirect/AUZIYQEPnjP5tQRlv9wLn5QZ5OFbAJFRoodH3VHEEmOBXYOgQh9N2E-Pj-aGIGCS1mnZAPR8ZkCh_JjLe7bd3IgQ1Xf7pn9i0RFBmmL6296YWvUtg20Cnkw7UgOwS1YmiHgS4hHimW0ZZVB6iUiERQQURlo73b71lg==)
- **Study Hint:** Always write the bitwise XOR alignment explicitly in your exam answer sheet—even for simple 3-bit or 5-bit words—so you get full step marks.
