# Facial-Biometrics-Encryption-Using-Henon-Ricker-Hybrid-Chaotic-Maps

A Python-based Thumbnail-Preserving Encryption (TPE) pipeline for facial privacy. By combining image processing with Henon-Ricker chaotic maps, it completely scrambles high-resolution facial features to block AI recognition while keeping low-resolution thumbnail previews perfectly intact for secure cloud browsing and file utility.

Traditional encryption algorithms scramble image data globally into random cryptographic noise. While secure, this completely breaks the file's structural format, rendering cloud storage un-browsable because system previews and thumbnails become useless. I engineered this project to resolve that dilemma by integrating localized digital image processing with high-entropy chaotic cryptography. The pipeline completely scrambles high-resolution, identifiable facial features to defeat automated AI face detection, yet leaves the low-resolution thumbnail preview perfectly intact and recognizable to the human eye.

---

## 🧠 Core Architecture & Mathematical Framework

The project achieves its dual utility through a two-stage pipeline: **Block-Based Permutation (Spatial Domain)** and **Chaotic Keystream Diffusion (Cryptographic Domain)**.

### 1. Spatial Domain Block Manipulation (OpenCV)
Instead of processing the image globally, the pipeline uses **OpenCV** to segment the input color channels into distinct, non-overlapping $16 \times 16$ or $32 \times 32$ pixel blocks. 
* Mathematical operations, pixel shuffling, and substitution are strictly constrained *inside* the boundaries of each individual block.
* Because pixel mutations are locked within these localized sub-matrices, the **local DC component (the mathematical average pixel intensity of the block) remains completely invariant**.
* When a cloud provider downscales the image to generate a thumbnail (e.g., via bilinear or bicubic interpolation), the sub-pixel scrambling averages out, rendering a clear, recognizable thumbnail preview. At native high resolution, however, the edge structures are completely shattered.

### 2. High-Entropy Chaotic Cryptography (Henon-Ricker Map)
To drive the internal pixel permutation and diffusion mechanisms, I implemented a dynamic, highly unpredictable pseudo-random keystream generator based on coupled **Henon-Ricker chaotic maps**. 

The Henon-Ricker map combines the quadratic stretching of the classical Henon map with the exponential dampening of the Ricker population model, governed by the following system of non-linear difference equations:

$$x_{n+1} = a \cdot x_n \cdot \exp(-x_n) + b \cdot y_n$$
$$y_{n+1} = x_n$$

* **Sensitivity to Initial Conditions:** A tiny change ($\Delta = 10^{-16}$) in the initial security keys ($x_0, y_0, a, b$) produces an entirely different, orthogonal keystream, making brute-force decryption mathematically infeasible.
* **NumPy Vectorization:** The generation of the chaotic orbits and subsequent element-wise XOR diffusion operations are fully vectorized using **NumPy**, eliminating performance-heavy Python loops to ensure high-throughput processing.

---

## 🛠️ Tech Stack & Dependencies

* **Language:** Python 3.10+
* **Image Processing Engine:** OpenCV (`opencv-python`) — utilized for optimized block segmentation, multi-channel splitting/merging (BGR/YCrCb), and spatial transformations.
* **Mathematical Processing:** NumPy — utilized for vectorized matrix mutations, chaotic orbit state tracking, and fast bitwise XOR diffusion layers.
* **Testing Infrastructure:** Pillow (PIL) & Matplotlib — for rendering performance comparisons and sub-pixel structural evaluation.

---

## 📂 Installation & Setup

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/haldarAryan/Facial-Biometrics-Encryption-Using-Henon-Ricker-Hybrid-Chaotic-Maps.git](https://github.com/haldarAryan/Facial-Biometrics-Encryption-Using-Henon-Ricker-Hybrid-Chaotic-Maps.git)
   cd Facial-Biometrics-Encryption-Using-Henon-Ricker-Hybrid-Chaotic-Maps
