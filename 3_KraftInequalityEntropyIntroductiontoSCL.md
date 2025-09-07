

# 📘 Lecture 3: Theoretical Foundations of Lossless Compression

Welcome to Lecture 3! This is the final lecture focusing on the **theory** behind lossless compression. Starting next session, we will shift to more **algorithmic** content.

---

## 🗂️ Topics Covered

1. [Kraft's Inequality](https://en.wikipedia.org/wiki/Kraft%E2%80%93McMillan_inequality)
2. The Fundamental Limits of Lossless Compression
3. Entropy and Its Role in Compression

---

## 📚 Kraft's Inequality

### What It Is

Kraft’s inequality provides a **necessary and sufficient condition** for the existence of a **prefix-free code**. It states:

* If you have codeword lengths $L_1, L_2, ..., L_k$, then:

$$
  \sum_{i=1}^{k} 2^{-L_i} \leq 1
$$

* **Converse**: If this inequality holds, then there exists a prefix-free code with those lengths.

### Significance

* This replaces English-like definitions (e.g., prefix-free = "no codeword is a prefix of another") with a precise mathematical formulation.
* It allows you to validate the feasibility of code lengths **without constructing the actual code**.

---

## 🧠 Entropy: The Measure of Information

### Definition

For a random variable $X$ with distribution $P = \{p_1, p_2, ..., p_k\}$, the **entropy** $H(X)$ is defined as:

$$
H(X) = -\sum_{i=1}^{k} p_i \log_2 p_i = \sum_{i=1}^{k} p_i \log_2 \frac{1}{p_i}
$$

### Properties

* **Maximum**: $H(X) = \log_2 k$ when $X$ is uniformly distributed over $k$ values.
* **Minimum**: $H(X) = 0$ when $X$ is deterministic.
* Units: **Bits**
* Interpretation: Represents the **average number of bits** needed to encode a symbol from the distribution.

---

## 🧾 The Fundamental Theorem of Lossless Compression

### Main Result

Let $L(X)$ be the **expected length** of a prefix-free code for random variable $X$. Then:

$$
H(X) \leq L(X) < H(X) + 1
$$

* **Lower Bound (Converse)**: No prefix-free code can do better than $H(X)$.
* **Achievability**: Shannon codes achieve within **1 bit** of entropy.
* **Optimality**: Only **dyadic distributions** (probabilities as powers of 2) can achieve entropy exactly.

---

## 🔄 Shannon Code vs. Optimal Code (Huffman)

### Shannon Code

* Constructs codewords with length $L_i = \lceil \log_2 \frac{1}{p_i} \rceil$
* Guarantees:

$$
  H(X) \leq L(X) < H(X) + 1
$$

### Huffman Code

* Uses a greedy algorithm to construct **optimal prefix-free codes**.
* Expected length $L(X)$ is minimized.
* Still cannot always reach entropy exactly unless distribution is dyadic.

---

## 🧮 KL Divergence (Relative Entropy)

Given two distributions $P$ and $Q$ over the same alphabet:

$$
D_{KL}(P \parallel Q) = \sum_{i=1}^{k} p_i \log_2 \frac{p_i}{q_i}
$$

### Properties

* $D_{KL}(P \parallel Q) \geq 0$
* Equality **iff** $P = Q$
* Used to prove the **converse** part of the fundamental theorem
* Not symmetric: $D_{KL}(P \parallel Q) \neq D_{KL}(Q \parallel P)$

---

## 📦 Block Coding

To get arbitrarily close to entropy:

* Use blocks of $n$ symbols

* Apply Shannon coding to blocks

* Result:

$$
  H(X) \leq \frac{L(X^n)}{n} < H(X) + \frac{1}{n}
$$

* As $n \to \infty$, expected length per symbol approaches $H(X)$

---

## 🛠️ Stanford Compression Library

* A pedagogical library built to provide **readable implementations** of common compression algorithms.
* Useful for:

  * Homework
  * Projects
  * Understanding concepts in practice

### Features

* Implementations of:

  * Prefix-free codes
  * Entropy coders
  * Bit-level utilities
  * Tree structures
* GitHub: [Stanford Compression Library](https://github.com/stanford-compression)

---

## 🔍 References

* [Kraft–McMillan Inequality (Wikipedia)](https://en.wikipedia.org/wiki/Kraft%E2%80%93McMillan_inequality)
* [Entropy (Information Theory)](https://en.wikipedia.org/wiki/Entropy_%28information_theory%29)
* [Shannon Coding (Wikipedia)](https://en.wikipedia.org/wiki/Shannon%E2%80%93Fano_coding)
* [Huffman Coding (Wikipedia)](https://en.wikipedia.org/wiki/Huffman_coding)
* [KL Divergence (Wikipedia)](https://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence)
* [Stanford Compression Library on GitHub](https://github.com/stanford-compression)

---
---


# 🧾 EE274: Data Compression I — Lecture 3 Study Guide

This guide reviews theoretical foundations in **lossless compression**, with emphasis on [Kraft's Inequality](https://en.wikipedia.org/wiki/Kraft%E2%80%93McMillan_inequality), [entropy](https://en.wikipedia.org/wiki/Entropy_%28information_theory%29), and the **Stanford Compression Library (SCL)**.

---

## I. 📘 Detailed Study Guide

### A. Stanford Compression Library (SCL)

#### 📌 Purpose and Motivation

* **Problem Addressed**: SCL bridges the gap between **theoretical understanding** and **practical implementation** in data compression. It addresses the lack of readable and efficient implementations of common algorithms.
* **Goals**:

  * Readable, understandable implementations.
  * A framework for students to build or extend compressors.
  * A tool to deepen researchers’ understanding of algorithmic subtleties.
* **Differentiation**:

  * Other implementations (e.g., low-level C or SIMD code) are optimized but often unreadable for learners.

#### 🔍 Key Features and Structure

* **Access**: [GitHub - Stanford Compression Library](https://github.com/stanford-compression)

* **Algorithms**:

  * Prefix-free codes.
  * Entropy coders.
  * External libraries for integration.

* **Utils Module**:

  * Handles **bit and byte manipulation**:

    * Convert between bit arrays and bytes.
    * Bit width calculation.
    * `int_to_bitarray()`, `bitarray_to_int()`, etc.

* **Tree & Probability Utils**:

  * Tree utilities for prefix code decoding/encoding.
  * Probability distribution tools for sorting, normalization, and cumulative calculations.

* **Function Structure**:

  * Core operations such as `decode_block()` and `decode_symbol()` in a **loop-based format**.

#### 🛠️ Practical Use

* SCL is deeply integrated into homeworks and projects.
* Designed for **modifiability and extensibility**.
* Students are encouraged to reach out to instructors if SCL becomes a bottleneck.

---

### B. Review of Previous Concepts

#### Prefix Codes

* **Definition**: No code word is a prefix of another.
* **Decoding Simplicity**: Enables efficient tree-based decoding.

#### Good Codes and Shannon Codes

* **Thumb Rule**: $L(x) \approx \log_2 \left(\frac{1}{P(x)}\right)$
* **Construction**:

  * Sort by probability.
  * Assign shortest available code satisfying prefix condition.
* **Example of Non-Optimality**:

  * Shannon assigned length 4 to a symbol where 3 was possible, increasing expected length.

---

### C. Kraft's Inequality

#### 🔢 Definition

* **Forward Part**:

$$
  \sum_{i=1}^K 2^{-L_i} \leq 1
$$
* **Converse**:

  * If the inequality is satisfied, then a prefix code exists for those lengths.
* **Implication**:

  * It characterizes **prefix codes exactly**.

#### 🧮 Proof Sketch (Forward)

* Define $L_{\max}$ = maximum code word length.
* $2^{L_{\max} - L_i}$: number of descendants at depth $L_{\max}$.
* **Disjointness**: Prefix property ensures no overlap.
* Leads to: $\sum 2^{-L_i} \leq 1$

#### 🔄 Relationship to Uniquely Decodable Codes

* Kraft’s inequality also applies to all **uniquely decodable codes** (not just prefix codes).

---

### D. Entropy

#### 🧠 Definition

$$
H(X) = \sum_{i=1}^K P_i \log_2 \left( \frac{1}{P_i} \right)
$$

* **Units**: Bits
* **Special Case**: $P_i = 0 \Rightarrow \text{term} = 0$

#### 📈 Properties

* Depends only on **distribution**, not variable identity.
* Can be expressed as:

$$
  H(X) = \mathbb{E}[\log_2 \left( \frac{1}{P(X)} \right)]
$$
* **Range**: $0 \leq H(X) \leq \log_2 K$

  * 0 = deterministic
  * $\log_2 K$ = uniform distribution

#### 💬 Interpretations

* **Uncertainty**: More randomness → higher entropy.
* **Information**: More unpredictable → more informative.
* **Compression Limit**: Entropy is the **minimum** expected length for lossless encoding.

#### 🔗 Joint Entropy (IID)

* If $X_1, X_2$ are independent:

$$
  H(X_1, X_2) = H(X_1) + H(X_2)
$$
* For $n$ IID variables:

$$
  H(X^n) = n \cdot H(X)
$$

---

### E. KL Divergence

#### 🧾 Definition

$$
D_{KL}(P \parallel Q) = \sum_{i=1}^K P_i \log_2 \left( \frac{P_i}{Q_i} \right)
$$

#### 📌 Key Properties

* $D_{KL}(P \parallel Q) \geq 0$
* Equality **iff** $P = Q$
* **Not symmetric**: $D_{KL}(P \parallel Q) \neq D_{KL}(Q \parallel P)$

#### 🤖 Application

* Common in **machine learning**, especially generative models like [VAEs](https://en.wikipedia.org/wiki/Variational_autoencoder) and language models.

---

### F. Main Result: Shannon’s Source Coding Theorem

#### ⚖️ Fundamental Lower Bound

$$
\mathbb{E}[L] \geq H(X)
$$

* No prefix/uniquely decodable code can **beat entropy**.

#### ✅ Achievability

* **Shannon Codes**:

$$
  H(X) \leq \mathbb{E}[L] < H(X) + 1
$$

* **Dyadic Distributions**:

  * Exact match when $P(x) = 1/2^n$

#### 📏 Proof Sketch (Converse)

* Define auxiliary distribution:

$$
  Q_i = C \cdot 2^{-L_i}, \quad \text{where } C = \frac{1}{\sum 2^{-L_i}}
$$

* Use [KL Divergence](https://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence):

$$
  D_{KL}(P \parallel Q) \geq 0 \Rightarrow \mathbb{E}[L] \geq H(X)
$$

* **Equality Conditions**:

  1. $\sum 2^{-L_i} = 1$ (Kraft with equality)
  2. $L_i = \log_2(1/P_i)$

#### 📉 "Arbitrarily Close" via Block Coding

* Shannon Codes are within **1 bit**, but not always sufficient.

* Block Coding:

$$
  H(X) \leq \frac{\mathbb{E}[L_n]}{n} < H(X) + \frac{1}{n}
$$

* **Trade-off**:

  * Large $n$ → better compression.
  * But higher computational/storage complexity.

* Efficient alternatives:

  * [Huffman coding](https://en.wikipedia.org/wiki/Huffman_coding)
  * [Arithmetic coding](https://en.wikipedia.org/wiki/Arithmetic_coding)
  * [ANS (Asymmetric Numeral Systems)](https://en.wikipedia.org/wiki/Asymmetric_numeral_systems)

---

## II. 🧠 Quiz Section

**Instructions**: Answer each in 2–3 sentences. \[See the full question/answer set above.]

---

## III. 📝 Essay Questions (Examples)

1. Discuss the motivations behind SCL’s creation. How does its design support learning?
2. Explain Kraft's Inequality as a mathematical tool for understanding prefix code structure.
3. Compare entropy as randomness vs. information. Why is it the limit of compression?
4. Elaborate the converse proof using Kraft’s inequality and KL divergence.
5. Why isn’t Shannon code "arbitrarily close"? How do block codes address this? What trade-offs arise?

---

## IV. 📚 Glossary

| Term                        | Definition                                                                     |
| --------------------------- | ------------------------------------------------------------------------------ |
| **SCL**                     | A Python library for compression algorithms designed for readability.          |
| **Prefix Code**             | A code where no word is a prefix of another. Enables unambiguous decoding.     |
| **Shannon Code**            | Uses $\lceil \log_2(1/P(x)) \rceil$ for code lengths. Within 1 bit of entropy. |
| **Kraft's Inequality**      | $\sum 2^{-L_i} \leq 1$; defines prefix code feasibility.                       |
| **L\_max**                  | The maximum code word length in a code.                                        |
| **Descendants**             | Tree nodes branching from a given node.                                        |
| **Uniquely Decodable Code** | Can be decoded unambiguously, even if not prefix-free.                         |
| **Entropy**                 | Expected information per symbol; lower bound for compression.                  |
| **Deterministic Variable**  | A variable with only one possible outcome (zero entropy).                      |
| **Uniform Distribution**    | Equal probability for all outcomes (max entropy).                              |
| **IID**                     | Independent, identically distributed random variables.                         |
| **Joint Entropy**           | Total entropy of multiple variables.                                           |
| **KL Divergence**           | Non-negative, asymmetric distance between two distributions.                   |
| **Source Coding Theorem**   | Establishes entropy as the minimum average code length.                        |
| **Dyadic Distribution**     | All probabilities are powers of two.                                           |
| **Block Coding**            | Encoding symbols in groups to reduce overhead.                                 |
| **Huffman Code**            | Optimal prefix code using a greedy tree-based approach.                        |
| **Arithmetic Code**         | Encodes full messages as fractional intervals.                                 |
| **ANS**                     | Fast, modern entropy coding method.                                            |

---

## 🔗 References

* [Kraft–McMillan Inequality](https://en.wikipedia.org/wiki/Kraft%E2%80%93McMillan_inequality)
* [Entropy (Information Theory)](https://en.wikipedia.org/wiki/Entropy_%28information_theory%29)
* [Shannon–Fano Coding](https://en.wikipedia.org/wiki/Shannon%E2%80%93Fano_coding)
* [Huffman Coding](https://en.wikipedia.org/wiki/Huffman_coding)
* [KL Divergence](https://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence)
* [Arithmetic Coding](https://en.wikipedia.org/wiki/Arithmetic_coding)
* [ANS Coding](https://en.wikipedia.org/wiki/Asymmetric_numeral_systems)
* [Stanford Compression Library on GitHub](https://github.com/stanford-compression)

