# Trends
- https://explodingtopics.com/blog/data-generated-per-day#data-creation-by-category

# Data Compression Fundamentals: A Study Guide

## I. The Growing Problem of Data Volume

### Understanding Data Volume

* **Units of Measurement**:

  * [Megabyte (MB)](https://en.wikipedia.org/wiki/Megabyte)
  * [Gigabyte (GB)](https://en.wikipedia.org/wiki/Gigabyte)
  * [Terabyte (TB)](https://en.wikipedia.org/wiki/Terabyte)
  * [Petabyte (PB)](https://en.wikipedia.org/wiki/Petabyte)
  * [Exabyte (EB)](https://en.wikipedia.org/wiki/Exabyte)
  * [Zettabyte (ZB)](https://en.wikipedia.org/wiki/Zettabyte)
* Understand the distinction between power-of-10 vs. power-of-2 units.

### Exponential Growth

* Recognize the global curve of exponential data creation and replication.

### Real-World Scale

* Relate units to practical data types:

  * Smartphone images
  * 4K video
  * Laptop/cloud storage
  * Daily internet traffic

### The "Why" of Data Management

* **Storage Costs**: High data volumes mean high costs.
* **Data in Motion**: Includes streaming (e.g., [Netflix](https://en.wikipedia.org/wiki/Netflix)) and bandwidth constraints.

---

## II. The Ubiquitous Nature of Data Compression

### Beyond Video

* Compression is vital for:

  * Text
  * Log files
  * Code ([GitHub](https://github.com/))
  * Genomic data
  * Emails, web searches, tweets
  * Sensor data (e.g., [EEG](https://en.wikipedia.org/wiki/Electroencephalography))
  * [Large Language Models (LLMs)](https://en.wikipedia.org/wiki/Large_language_model)

### Compression as a Necessity

* Background necessity for efficient systems.

### Trade-offs in Compression

* **Size vs. Error**: Illustrated by the [Rate-Distortion](https://en.wikipedia.org/wiki/Rate%E2%80%93distortion_theory) curve.
* **Perception and Application**: Human perception influences acceptable compression levels.
* **Design Decisions**: Trade-offs are central to compression design.

---

## III. Core Concepts and Principles of Data Compression

### Definition

* "The succinct representation of information."

### Why We Care

* **Storage & Transmission Efficiency**
* **Information Processing**: Focus on essential information.
* **Signal Denoising & Communication**: Parallels in reducing noise.
* **Simplified Implementations**
* **Link to Prediction**: Compression ↔ Prediction
* **Building Block**: Enables scalable systems.

---

## IV. Fields of Compression Research and Application

### Theory

* **[Claude Shannon](https://en.wikipedia.org/wiki/Claude_Shannon)** and [Information Theory](https://en.wikipedia.org/wiki/Information_theory)
* **[Entropy](https://en.wikipedia.org/wiki/Entropy_%28information_theory%29)**: Compression limit
* **[Rate-Distortion Theory](https://en.wikipedia.org/wiki/Rate%E2%80%93distortion_theory)**: Lossy limits

### Algorithms

* Elegant approaches:

  * [LZ-based schemes](https://en.wikipedia.org/wiki/LZ77_and_LZ78)
  * [Gzip](https://en.wikipedia.org/wiki/Gzip)
  * Transforms: [KLT](https://en.wikipedia.org/wiki/Karhunen%E2%80%93Lo%C3%A8ve_transform), [FFT](https://en.wikipedia.org/wiki/Fast_Fourier_transform), [DCT](https://en.wikipedia.org/wiki/Discrete_cosine_transform)

### Numeral Systems

* Surprising link to compression.

### Implementations

* **Efficiency**: Required for real-time decoding.
* **Hardware Optimization**: e.g., laptop decoders, instruction sets
* **Frame Groups**: [IPB frames](https://en.wikipedia.org/wiki/Inter_frame)

### Data Structures

* Tools like [Suffix Trees](https://en.wikipedia.org/wiki/Suffix_tree), [BWT](https://en.wikipedia.org/wiki/Burrows%E2%80%93Wheeler_transform)

---

## V. Course Structure and Approach

### Compression Types

* **Lossless**: No information loss
* **Lossy**: Acceptable information loss

### Learning Blend

* Theory, proofs, tools, and code

### Key Topics

* **Lossless**: Entropy, [Huffman Coding](https://en.wikipedia.org/wiki/Huffman_coding), [Arithmetic Coding](https://en.wikipedia.org/wiki/Arithmetic_coding), [Asymmetric Numeral Systems](https://en.wikipedia.org/wiki/Asymmetric_numeral_systems), Gzip
* **Lossy**: Rate-Distortion, Mutual Information, [Quantisation](https://en.wikipedia.org/wiki/Quantization_%28signal_processing%29), Transform Coding, JPEG, BPG, ML compressors, Video, Human perception

### Projects

* ML, hardware, low-level coding

---

## VI. Introduction to Lossless Compression Basics

### Alphabet and Distribution

* **Alphabet**: Symbol set (e.g., A, B, C, D)
* **Distribution**:

  * **Uniform**: Equal probabilities
  * **Non-uniform**: Unequal probabilities

### Bits and Bytes

* **Bit**: 0 or 1
* **Byte**: 8 bits
* Conversion: 1 KB = 1000 or 1024 bytes

### Encoding and ASCII

* **Encoding**: Symbol to bit conversion
* **[ASCII](https://en.wikipedia.org/wiki/ASCII)**: 8 bits per symbol

### Fixed Bitwidth Codes

* Concept: Same bit count per symbol
* Calculation: `log2(K)` bits
* Limitation: Inefficient for non-uniform distributions

### Variable Length Codes

* Shorter codes for common symbols
* More efficient for non-uniform distributions
* Decoding complexity previewed

### Expected Code Length

* Formula: `Σ (P(symbol) × Code Length)`
* Evaluates code efficiency

### Optimal Compression Rate

* Related to **Entropy**
* There is a theoretical compression limit

---

Here is your content formatted into structured, link-enhanced Markdown:

---

# Key Questions on Data Compression

---

## Why is Data Compression Important in Today's World?

Data compression is essential due to the **exponential growth of global data volume**, measured in [zettabytes (10²¹ bytes)](https://en.wikipedia.org/wiki/Zettabyte). This growth leads to:

* **High storage and management costs**: Storing [petabytes (10¹⁵ bytes)](https://en.wikipedia.org/wiki/Petabyte) can cost companies millions of dollars.
* **Network strain from data in motion**: For example, [Netflix](https://en.wikipedia.org/wiki/Netflix) was asked to reduce bandwidth during COVID-19 due to high video traffic.

**Compression reduces** storage needs and bandwidth usage, making data handling more **cost-effective** and **efficient**.

---

## Where is Data Compression Applied Beyond Videos and Images?

Compression is critical in numerous areas beyond media:

* **Text and Code**: Used in [Git](https://git-scm.com/) for storing changes.
* **Log Files & Databases**: Efficient storage of diagnostics and transactions.
* **Genomic Data**: Enables large-scale biological data processing.
* **Emails & Search**: Underpins systems like Gmail and [Google Search](https://www.google.com/).
* **Sensor Data**: Includes [EEG](https://en.wikipedia.org/wiki/Electroencephalography) and neural recordings.
* **Machine Learning Models**: Used in both improving and compressing [LLMs](https://en.wikipedia.org/wiki/Large_language_model).

---

## What Fundamental Trade-Offs Are Involved in Data Compression?

Compression involves a trade-off between **file size** and **quality**, illustrated by the [Rate-Distortion Curve](https://en.wikipedia.org/wiki/Rate%E2%80%93distortion_theory):

* **Higher size → Lower error**: Useful for high-fidelity applications (e.g., HD streaming).
* **Lower size → Higher error**: Acceptable in bandwidth-constrained scenarios.

This trade-off shapes compression strategy and is often controlled by user settings (e.g., Spotify’s streaming quality options).

---

## What Is the Difference Between Lossless and Lossy Compression?

### Lossless Compression

* No information is lost.
* Used for text, code, logs.
* Examples: [ZIP](https://en.wikipedia.org/wiki/ZIP_%28file_format%29), [Huffman coding](https://en.wikipedia.org/wiki/Huffman_coding).

### Lossy Compression

* Discards non-essential information.
* Used for images (e.g., [JPEG](https://en.wikipedia.org/wiki/JPEG)), videos (e.g., Netflix).
* Allows for smaller files at the cost of quality.

---

## Why Can't We Compress a File to Zero Bytes?

Compression has a theoretical limit defined by **[entropy](https://en.wikipedia.org/wiki/Entropy_%28information_theory%29)**:

* **Entropy** quantifies the minimum bits needed to represent data.
* **Infinite compression** is impossible; even the best algorithm cannot reduce truly random or optimally compressed data further.
* **Over-compression** may increase file size due to headers or metadata.

---

## How Does Variable-Length Coding Improve Efficiency?

Variable-length coding assigns **shorter codes to frequent symbols** and **longer ones to rare symbols**, unlike fixed-bitwidth coding:

* **Fixed-bitwidth**: 2 bits per symbol (e.g., A=00, B=01, etc.).
* **Variable-length**: Common symbols like A might be encoded as `0`, rare ones like D as `111`.

This results in a **lower average (expected) code length**, improving compression.

---

## What Is the Significance of the Expected Code Length?

The **expected code length** measures the **average bits per symbol**, calculated as:

```
E[L] = Σ [P(x) × L(x)]
```

Where:

* `P(x)` = Probability of symbol `x`
* `L(x)` = Code length of symbol `x`

A lower expected code length means more efficient compression and serves as a **benchmark** for evaluating compression schemes.

---

## How Does Compression Impact Streaming Services?

Compression is crucial for services like [YouTube](https://en.wikipedia.org/wiki/YouTube) and Netflix:

* **Real-time decoding**: Enabled by hardware-accelerated codecs.
* **Bandwidth adaptation**: Streams adjust quality dynamically based on network speed.
* **Seeking functionality**: Powered by frame structures like [IPB frames](https://en.wikipedia.org/wiki/Inter_frame), allowing fast navigation.

Without compression, **smooth playback** and **low latency** would be impossible.

Here is a **Markdown-formatted summary** of the key points from the lecture transcript on **Stanford EE274 Lecture 1: Introduction to Data Compression**:

---

## 🌍 Why Data Compression?

### Exponential Growth in Data

* Data volumes are increasing **exponentially**, from megabytes (MB) to **zettabytes (ZB)** ([Zettabyte](https://en.wikipedia.org/wiki/Zettabyte)).
* Real-world scale:

  * **MB**: Smartphone image
  * **GB**: 4K video
  * **TB**: Laptop storage
  * **PB**: Cloud storage (e.g., [AWS S3](https://aws.amazon.com/s3/))
  * **EB**: Daily internet traffic
  * **ZB**: Global yearly data creation

### Data at Rest vs. Data in Motion

* **Data at Rest**: Storage challenges and cost.
* **Data in Motion**: Network bandwidth (e.g., Netflix asked to reduce bitrate during COVID-19).

---

## 📌 Ubiquity of Compression

### Beyond Multimedia

* Applies to:

  * Text, logs, code (e.g., [GitHub](https://github.com))
  * Genomic data, EEG recordings
  * Emails, Google searches, tweets
  * [LLMs](https://en.wikipedia.org/wiki/Large_language_model) and ML models

### Practical Necessity

* Compression enables:

  * Feasible transmission
  * Efficient storage
  * Real-time analytics
  * Deployment of large models

---

## ⚖️ Compression Trade-Offs

### Rate-Distortion Trade-Off

* Higher compression → Higher distortion (loss of quality)
* Trade-offs depend on use-case:

  * Audio: bitrate vs. perceived sound quality
  * Images: resolution vs. visual artifacts
  * Apps like **Spotify** and **Netflix** balance these trade-offs

---

## 📚 Core Concept: What is Compression?

> **Compression is the succinct representation of information.**

### Why Compression?

* Saves storage and bandwidth
* Extracts relevant information (like denoising)
* Facilitates simpler computation and prediction
* Fundamental to efficient system design

---

## 🔍 Theoretical Foundations

### Information Theory

* Founded by [Claude Shannon](https://en.wikipedia.org/wiki/Claude_Shannon)
* Key concept: [Entropy](https://en.wikipedia.org/wiki/Entropy_%28information_theory%29) — the theoretical lower bound of compressibility

### Impossibility Result

* You **cannot compress** a file **infinitely** (e.g., to zero bytes)
* Every distribution has a **minimum achievable compression rate**

---

## 💻 Types of Compression

### Lossless Compression

* No data is lost (e.g., ZIP, Gzip)
* Useful for: code, logs, medical data

### Lossy Compression

* Permits information loss for higher compression
* Used in: images (JPEG), audio (MP3), video (MPEG)

---

## 🧠 Link to Machine Learning

* **ML helps compression**: ML-based compressors (e.g., learned JPEG alternatives)
* **Compression helps ML**: Quantization and pruning in model deployment

---

## 🧪 Course Breakdown

### Course Flow

* **First Half**: Lossless compression

  * Topics: Entropy, Huffman coding, arithmetic coding, LZ schemes
* **Second Half**: Lossy compression

  * Topics: Rate-distortion theory, transform coding, JPEG, learned compression

### Learning Approach

* Blend of **theory**, **practical algorithms**, and **tools**
* Exposure to: hardware optimization, low-level coding, transform methods (e.g., [FFT](https://en.wikipedia.org/wiki/Fast_Fourier_transform), [DCT](https://en.wikipedia.org/wiki/Discrete_cosine_transform))

---

## 🧩 Introduction to Lossless Compression

### Basics

* **Bit**: Basic unit (0 or 1)
* **Byte**: 8 bits (256 possible values)
* **ASCII**: Standard encoding scheme (1 byte per character)

### Fixed vs. Variable Length Coding

* **Fixed-bitwidth**: Equal bits per symbol; simple but inefficient for skewed distributions
* **Variable-length**: Shorter codes for frequent symbols; better compression
* Metric: **Expected Code Length** = `Σ P(x) * L(x)`

---

## 🏁 Final Thoughts

* Compression is fundamental across disciplines
* Combines **elegant algorithms**, **real-world utility**, and **deep theory**
* Homework: Decode a variable-length encoded bitstring

