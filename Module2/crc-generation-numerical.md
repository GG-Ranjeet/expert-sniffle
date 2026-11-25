# Q4. CRC Generation Numerical Problem

> **Exam Weightage:** 5–10 Marks | **Module 2:** Data Link Layer

**Question:** Find the CRC for the data `1010101010` with the divisor $x^2 - x - 1$.

---

## 1. Converting the Polynomial Divisor to Binary

In Cyclic Redundancy Check (CRC), all polynomial arithmetic is performed in **modulo-2 arithmetic over the Galois Field $GF(2)$**, where addition and subtraction are both identical to the **XOR** operation ($-1 \equiv +1 \pmod 2$).

Therefore:
$$G(x) = x^2 - x - 1 \equiv x^2 + x + 1 \pmod 2$$

Writing the coefficients of $1\cdot x^2 + 1\cdot x^1 + 1\cdot x^0$:
- **Binary Divisor ($G$):** **`111`** (3 bits)
- **Degree of Generator ($k$):** $2$

---

## 2. Padding the Data with Zeros

Since the degree of the divisor is $k = 2$, we append **$2$ zeros** to the end of the original 10-bit data:
- **Original Data ($D$):** `1010101010` (10 bits)
- **Padded Dividend:** `1010101010`**`00`** (12 bits)

---

## 3. Step-by-Step Modulo-2 (XOR) Binary Division

We divide `101010101000` by `111`. In each step:
- If the leftmost bit of the current 3-bit window is **`1`**, XOR with `111` (quotient bit = `1`).
- If the leftmost bit is **`0`**, XOR with `000` (quotient bit = `0`).
- Drop down the next bit from the dividend.

```text
                1 1 1 0 0 0 1 1 1 0   <-- Quotient
          _________________________
    1 1 1 ) 1 0 1 0 1 0 1 0 1 0 0 0
          ^ 1 1 1
          -------
            0 1 0 0                   (010 + drop 0 -> 100)
            ^ 1 1 1
            -------
              0 1 1 1                 (011 + drop 1 -> 111)
              ^ 1 1 1
              -------
                0 0 0 0               (000 + drop 0 -> 000)
                ^ 0 0 0
                -------
                  0 0 1               (000 + drop 1 -> 001)
                  ^ 0 0 0
                  -------
                    0 1 0             (001 + drop 0 -> 010)
                    ^ 0 0 0
                    -------
                      1 0 1           (010 + drop 1 -> 101)
                    ^ 1 1 1
                    -------
                      0 1 0 0         (010 + drop 0 -> 100)
                      ^ 1 1 1
                      -------
                        0 1 1 0       (011 + drop 0 -> 110)
                        ^ 1 1 1
                        -------
                          0 0 1 0     (001 + drop 0 -> 010)
                          ^ 0 0 0
                          -------
                            0 1 0     <-- Remainder = 10 (last 2 bits)
```

### Verification (Checking the Transmitted Codeword)
Replacing the 2 appended zeros with the remainder **`10`** gives the transmitted codeword:
$$\text{Transmitted Codeword} = \mathbf{101010101010}$$

If we divide `101010101010` by `111`:
- At the second-to-last step, `111 ^ 111 = 000`, dropping the final `0` gives `000`, yielding a remainder of **`00`** (confirmed valid!).

---

## 4. Final Answer

- **Divisor Polynomial:** $x^2 - x - 1 \equiv x^2 + x + 1 \rightarrow$ **`111`**
- **CRC Bits (Remainder):** **`10`**
- **Final Transmitted Codeword (Data + CRC):** **`101010101010`**

---

## 5. References & Study Hints

- **GeeksforGeeks – Cyclic Redundancy Check (CRC):** [GeeksforGeeks CRC Guide](https://vertexaisearch.cloud.google.com/grounding-api-redirect/AUZIYQEjrOBeVM-IoQGt8BrufaFn2rmpfdERHTvzqkrR6Aqwan-R1MLZakjPr8OYFDbeK4JStrVz67DWGziDTnbA1NG-7fp3bco04JGv3VAnMfr8RgfIYf-HJ8gTX9ADUQmcdG3t26vRNdzgbun0io2kySnaNitoNoCF6YQxyPszlpVlvM1L6Dujz4_69-A=)
- **Exam Tip:** Notice the trick in the question: $x^2 - x - 1$ uses minus signs, which in $GF(2)$ modulo-2 arithmetic are identical to plus signs ($x^2 + x + 1 = 111$). Mentioning this explicitly in your first line shows strong conceptual clarity!
