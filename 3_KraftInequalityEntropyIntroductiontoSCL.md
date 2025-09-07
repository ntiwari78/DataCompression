

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

