
# 📘 Data Compression I: Prefix-Free Codes and Shannon Code Briefing

A summary of key concepts from the lecture on **prefix-free codes**, **Shannon code**, and foundational principles in [lossless compression](https://en.wikipedia.org/wiki/Lossless_compression).

---

## 1. 🎯 Fixed-Length Codes and Sub-optimality

* **Definition**: Each symbol from an alphabet of size $N$ is assigned a codeword of fixed length:

$$
  \text{Bits per symbol} = \lceil \log_2(N) \rceil
$$

* **Example**: For $N = 9$,

$$
  \lceil \log_2(9) \rceil = 4 \text{ bits/symbol}
$$

* **Problem**:
  4 bits allow 16 combinations, but only 9 are used → **inefficient**.

* **Improvement via Blocking**:

  * Block size 2 → New alphabet: $9^2 = 81$

$$
    \lceil \log_2(81) \rceil = 7 \text{ bits/block} \Rightarrow 3.5 \text{ bits/symbol}
$$
  
  * Larger blocks converge to ideal $\log_2(N)$, but increase computational complexity.

---

## 2. 📊 Expected Code Length

* Formula:

$$
  \mathbb{E}[L] = \sum P_i \cdot L_i
$$

* **Example**:
  A (0.5, 1), B (0.3, 2), C (0.2, 2)

$$
  0.5 \cdot 1 + 0.3 \cdot 2 + 0.2 \cdot 2 = 1.5 \text{ bits/symbol}
$$

---

## 3. 🧩 Lossless Compression & Uniquely Decodable Codes

* **Lossless Compression**: Enables exact reconstruction of the original input.

* **Not Uniquely Decodable Examples**:

  * A = `0`, B = `0` → identical codewords.
  * A = `0`, B = `00` → ambiguous: `00` could be `AA` or `B`.

* **[Uniquely Decodable Code](https://en.wikipedia.org/wiki/Prefix_code#Uniquely_decodable_codes)**:

  * No two distinct input sequences map to the same output.
  * Necessary for error-free decoding.

* **[Morse Code](https://en.wikipedia.org/wiki/Morse_code)**:

  * Not uniquely decodable in binary form; relies on **timing gaps**.
  * Modern compression avoids separators—needs structural guarantees.

---

## 4. ⏱️ Prefix-Free Codes (Instantaneous Codes)

* **Definition**: No codeword is a **prefix** of another.

  * Example: A = `0`, B = `10`, C = `110`, D = `111`

* **Instantaneous Decoding**: Each symbol can be decoded immediately upon recognition.

  * Input: `11100` → Decode: D (111), A (0), A (0)

* **Key Point**:
  Prefix-free ⇒ Uniquely decodable
  But: Uniquely decodable ≠ Prefix-free

---

## 5. 🌲 Binary Tree Representation

* **Structure**: Prefix-free codes map to **leaf nodes** in a binary tree.

  * 0 = left, 1 = right
  * Path from root to leaf = codeword

* **Decoding Algorithm**:

  1. Start at root
  2. Traverse left/right based on bit
  3. When a leaf is reached → decode symbol
  4. Return to root and repeat

* **Prefix Violation**:
  If a codeword is an internal node (not a leaf), it is a prefix of its descendants → **not prefix-free**

---

## 6. ✅ Properties of Good Prefix-Free Codes

A **good** prefix-free code minimizes expected code length, while remaining prefix-free.

### Property 1: Qualitative (Order Alignment)

* If $P(S_1) > P(S_2)$, then $L(S_1) \leq L(S_2)$
* Reordering to reflect this reduces expected length.

### Property 2: Quantitative (Shannon's Ideal Length)

$$
L(X) \approx \log_2\left(\frac{1}{P(X)}\right)
$$

* **Rationale**: Output is binary ⇒ base 2

* **Uniform Example**:
  $P(A) = P(B) = 0.5$ ⇒ $L = \log_2(2) = 1$

* **Non-Uniform Example**:
  $P(A)=0.5, B=0.25, C=0.125, D=0.125$
  Ideal lengths: A=1, B=2, C=3, D=3
  Code: A=0, B=10, C=110, D=111 → **Optimal**

---

## 7. 🧠 Shannon Code Construction

A method to construct near-optimal **prefix-free codes**.

### Steps:

1. **Calculate Ideal Lengths**:

$$
   L(X) = \lceil \log_2(1/P(X)) \rceil
$$

2. **Sort** symbols by increasing $L(X)$

3. **Greedy Assignment**:

   * Assign a binary code at depth $L(X)$
   * Ensure no codeword is a prefix of another

### Kraft's Inequality (Underlying Proof):

$$
\sum 2^{-L_i} \leq 1
$$

* Guarantees that the binary tree has enough "space" to assign all codewords at their required depth.

### Inductive Insight:

* When assigning a codeword at depth $L_{m+1}$, enough unoccupied leaves remain.
* Previously assigned codewords only exclude parts of the tree ⇒ remaining space always suffices.

---

## 8. 📉 Why Shannon Codes Aren’t Always Optimal

* Uses **ceiling function** → may exceed entropy.
* Leaves some tree paths unused.
* Other algorithms like [Huffman Coding](https://en.wikipedia.org/wiki/Huffman_coding) offer **optimal** prefix-free encoding for given symbol distributions.

---


# 📘 Data Compression: Prefix-Free Codes and Kraft's Inequality

A study guide for understanding the role of **prefix-free codes** and **Kraft's inequality** in data compression.

---

## I. 📏 Fixed-Length Codes and Their Limitations

* **Definition**: Fixed-length codes assign the same number of bits to every symbol.
* **Bits per Symbol**:
  $\text{Bits} = \lceil \log_2(\text{alphabet size}) \rceil$
* **Suboptimality**: Wastes bits when alphabet size ≠ power of 2.
* **Blocking**: Encoding groups of symbols increases the effective alphabet size and reduces bits per symbol.

### Key Questions

* How does blocking improve compression?
* What are its computational and memory limitations?

---

## II. 📐 Variable-Length Codes and Decoding

* **Expected Code Length**:
  $\mathbb{E}[L] = \sum P(x) \cdot L(x)$
* **Decoding Issue**: Without separators, decoding is ambiguous unless the code is well-structured (e.g., prefix-free).

---

## III. 🔁 Lossless Compression & Unique Decodability

* **Lossless Compression**: Perfect reconstruction of original data.
* **Uniquely Decodable Code**:
  No two different input sequences map to the same output.

### Example:

* Not uniquely decodable:
  `A = 0, B = 00` ⇒ "00" could mean "B" or "AA".

* [Morse Code](https://en.wikipedia.org/wiki/Morse_code):
  Not formally uniquely decodable; relied on **pauses** for disambiguation.

---

## IV. 🟢 Prefix-Free (Instantaneous) Codes

* **Definition**: No codeword is a prefix of another.
* **Instantaneous**: Symbols can be decoded as soon as a full codeword is read.

### Decoding Algorithm (Greedy):

1. Start with empty buffer.
2. Append bits one by one.
3. If buffer matches a codeword, decode it.
4. Reset buffer and continue.

### Property:

* Every prefix-free code is uniquely decodable.
* Converse is not always true.

---

## V. 🌲 Tree Representation of Prefix-Free Codes

* **Binary Tree Structure**:

  * Left = 0, Right = 1.
  * Codewords are **leaf nodes**.
* **Prefix Property**:
  A codeword must not be an internal node (else it’s a prefix).

---

## VI. ✅ Properties of "Good" Prefix-Free Codes

* **1st Property (Qualitative)**:
  If $P(S_1) > P(S_2)$, then $L(S_1) \leq L(S_2)$

* **2nd Property (Quantitative)**:
  $L(x) \approx \log_2(1/P(x))$

### Example:

* $A = 0$ (P=½), $B = 10$ (P=¼), etc.
  → Lengths align with $\log_2(1/P(x))$

---

## VII. 🧠 Shannon Code Construction

* **Inventor**: [Claude Shannon](https://en.wikipedia.org/wiki/Claude_Shannon)
* **Goal**:
  $L(x) = \lceil \log_2(1/P(x)) \rceil$

### Steps:

1. Compute $\lceil \log_2(1/P(x)) \rceil$ for each symbol.
2. Sort by length.
3. Greedily assign codewords as leaves at required depth.

### Kraft's Inequality:

* **Condition** for prefix-free codes:

  $$
  \sum 2^{-L(x)} \leq 1
  $$

* **Interpretation**:
  All codewords must fit into the total binary "space" at each depth.

* **Inductive Proof**:
  Always at least one unclaimed leaf node available when assigning a new codeword.

---

## 📋 Quiz Questions (Short Answer)

1. Why is fixed-length coding suboptimal for 9-symbol alphabets?
2. How does block encoding improve compression for non-power-of-2 alphabets?
3. Define uniquely decodable codes. Give a counterexample.
4. What is a prefix-free code, and why is it "instantaneous"?
5. Describe the greedy decoding process for prefix-free codes.
6. How is a prefix-free code represented using a binary tree?
7. State the first "goodness" property for prefix-free codes.
8. Approximate codeword length for symbol X with probability P(X)?
9. Steps in constructing a Shannon code?
10. What does $2^L$ mean in Kraft’s inequality context?

---

## 🧠 Essay Prompts

* Compare **fixed-length vs. prefix-free** codes in compression efficiency and decoding.
* Explain the importance of **unique decodability** and why prefix-free codes are significant.
* Define a "good" prefix-free code and how Shannon’s method approximates it.
* Use **tree representation** to illustrate prefix violations.
* Detail the **inductive proof** behind Shannon code feasibility using Kraft’s inequality.

---

## 📖 Glossary of Key Terms

| Term                                                                           | Definition                                              |
| ------------------------------------------------------------------------------ | ------------------------------------------------------- |
| **Alphabet**                                                                   | Set of all possible input symbols                       |
| **Bit**                                                                        | Basic binary unit: 0 or 1                               |
| **Binary Tree**                                                                | Hierarchical structure with two children per node       |
| **Block Encoding**                                                             | Encoding fixed-size blocks of symbols                   |
| **Code**                                                                       | Mapping from symbols to bit strings                     |
| **Codeword**                                                                   | Bit string assigned to a symbol                         |
| **Expected Code Length**                                                       | $\sum P(x) \cdot L(x)$                                  |
| **Fixed-Length Code**                                                          | Code with equal-length codewords                        |
| **Greedy Algorithm**                                                           | Local-optimal approach used in Shannon code             |
| **Instantaneous Code**                                                         | Same as prefix-free; decodable without lookahead        |
| **Internal Node**                                                              | Tree node with at least one child                       |
| **[Kraft’s Inequality](https://en.wikipedia.org/wiki/Kraft%27s_inequality)**   | Feasibility condition for prefix-free codes             |
| **Leaf Node**                                                                  | Tree node with no children; valid codeword endpoint     |
| **[Lossless Compression](https://en.wikipedia.org/wiki/Lossless_compression)** | No data loss during compression                         |
| **[Morse Code](https://en.wikipedia.org/wiki/Morse_code)**                     | Early variable-length code with timing-based separation |
| **Prefix-Free Code**                                                           | Code with no codeword as prefix of another              |
| **[Shannon Code](https://en.wikipedia.org/wiki/Shannon%E2%80%93Fano_coding)**  | Near-optimal code based on symbol probabilities         |
| **Uniquely Decodable Code**                                                    | No ambiguity in decoding bitstreams                     |
| **Variable-Length Code**                                                       | Different symbols have different-length codewords       |


---

# 🧵 Study Guide: Fixed-Length Codes, Prefix-Free Codes, and Shannon Coding

---

## I. 📏 Fixed-Length Codes

### Definition

A **fixed-length code** assigns an equal number of bits to every symbol in the alphabet.

* **Formula**:

$$
  \text{Bits per symbol} = \lceil \log_2(N) \rceil
$$

  where $N$ is the number of symbols.

* **Example**:
  For $N = 9$, $\log_2(9) \approx 3.17 \Rightarrow \lceil 3.17 \rceil = 4$ bits/symbol.

### Limitations

* **Wasted space**: 4 bits allow for 16 combinations, but only 9 are used.
* **Inefficiency** for non-power-of-two alphabets.

---

## II. 🧮 Block Encoding with Fixed-Length Codes

### Concept

* Encode **blocks of symbols** to improve compression efficiency.
* Creates a larger **product alphabet**.

### Example

* Original: 9 symbols → 4 bits/symbol
* Block of 2: $9^2 = 81$ → $\lceil \log_2(81) \rceil = 7$ bits/block

$$
  \text{Bits per symbol} = \frac{7}{2} = 3.5
$$

### Pros & Cons

* **Pro**: Closer to entropy-bound.
* **Con**: Alphabet size grows exponentially; increases memory and computation.

---

## III. 🧵 Uniquely Decodable Codes

### Definition

A code is **uniquely decodable** if **no two input sequences map to the same output sequence**.

* **Example (Invalid)**:
  A = `0`, B = `00` → Output `00` could be “AA” or “B”

### Importance

* Essential for [lossless compression](https://en.wikipedia.org/wiki/Lossless_compression).
* Prevents ambiguity in decoding without needing separators or pauses (unlike [Morse code](https://en.wikipedia.org/wiki/Morse_code)).

---

## IV. 🟢 Prefix-Free (Instantaneous) Codes

### Definition

A **prefix-free** (or **instantaneous**) code ensures **no codeword is a prefix of another**.

* **Example**:
  A = `0`, B = `10`, C = `110`, D = `111`

### Properties

* Enables **immediate decoding**.
* All prefix-free codes are uniquely decodable.
* Not all uniquely decodable codes are prefix-free, but prefix-free codes are preferred for efficiency.

---

## V. 🌲 Binary Tree Representation of Prefix Codes

### Tree Mapping

* Root → Left (0), Right (1)
* **Path to leaf** = codeword

### Key Insight

* Only **leaf nodes** can be codewords.
* **Internal node** as codeword ⇒ it’s a prefix of deeper codewords ⇒ violates prefix-free property.

### Decoding Algorithm

1. Start at root.
2. Traverse tree per bit.
3. On reaching leaf, decode symbol and return to root.

---

## VI. 📉 Properties of Good Prefix-Free Codes

### 1. Qualitative Property

If $P(S_1) > P(S_2)$, then $L(S_1) \leq L(S_2)$.

* **Reason**: Shorter codewords for frequent symbols reduce expected length.

### 2. Quantitative Property

$$
L(X) \approx \log_2\left(\frac{1}{P(X)}\right)
$$

* **Example**:

  * A = `0` (P=½), L=1
  * B = `10` (P=¼), L=2
  * C = `110` (P=⅛), L=3
  * D = `111` (P=⅛), L=3

---

## VII. 🧠 Shannon Code Construction

### Overview

Designed by [Claude Shannon](https://en.wikipedia.org/wiki/Claude_Shannon), this prefix-free code approximates the entropy lower bound.

### Construction Steps

1. **Calculate Lengths**:

$$
   L(X) = \lceil \log_2(1 / P(X)) \rceil
$$

2. **Sort** symbols by $L(X)$

3. **Greedy Assignment**:

   * Assign shortest unused binary strings that maintain the prefix-free property.
   * Each codeword corresponds to a **leaf** in the binary tree.

---

## VIII. 📉 Why Shannon Codes Aren’t Always Optimal

* **Rounding**: $\lceil \log_2(1 / P(X)) \rceil$ may exceed ideal $-\log_2(P(X))$
* **Unused space**: Some binary tree paths may remain unassigned.
* **Better methods**: [Huffman coding](https://en.wikipedia.org/wiki/Huffman_coding) often produces **optimal prefix-free codes**.

