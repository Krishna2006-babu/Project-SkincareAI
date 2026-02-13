# 🩺 Sky-AI: Advanced Skincare Analyzer

**Author:** Krishna Sharma, B.Tech (ECE), NIT Silchar  
**Version:** 1.0 (Phase 3 Integration Complete)  
**Date:** February 2026

Sky-AI is an end-to-end computer vision platform designed to democratize skincare diagnostics. It utilizes a laptop’s integrated webcam to capture high-definition skin samples, analyzes them using digital signal processing, and generates medical-style reports with personalized treatment plans.

---

## 🏗️ 1. Technical Architecture

The system is built on a modular, **three-tier architecture** designed for high throughput and hardware stability.

### **Tier 1: Data Acquisition (The Eyes)**
* **Backend**: Uses the `DSHOW` (DirectShow) video backend to bypass standard Windows Media Foundation (MSMF) errors, ensuring 100% frame-grab reliability.
* **Threading**: Implements `threading.Thread` to manage camera handshakes. This prevents the "Not Responding" GUI state while the hardware initializes.

### **Tier 2: Processing Engine (The Brain)**
* **Matrix Math**: Uses `NumPy` for high-speed color channel calculations.
* **Logic Module**: An externalized `day6_brain.py` script that maps numerical scores to a diagnostic knowledge base.

### **Tier 3: User Interface (The Body)**
* **Dashboard**: A dark-mode `Tkinter` GUI optimized for professional engineering presentations.
* **Visualizers**: Uses `ttk.Progressbar` widgets to provide immediate visual feedback on skin health.



---

## 🧪 2. Vision Logic & Mathematical Foundations

The **"Start AI Skin Scan"** button triggers three distinct analytical algorithms:

### **A. Redness (Inflammation) Scoring**
Skin inflammation is detected by calculating the variance between the Red and Green channels of the RGB color space.
$$Score_R = \mu(Red) - \mu(Green)$$
Higher values indicate higher levels of dermal irritation or sensitivity.

### **B. Oiliness (Sebum %) Detection**
To detect shine without being fooled by ambient light, the app converts frames into **HSV (Hue, Saturation, Value)** space. 
* It isolates the **Value (V)** channel and applies a binary mask to identify pixels in the range of $180-255$.
* The final score is the percentage of "shiny" pixels relative to the total frame size.

### **C. Texture (Smoothness) Analysis**
Texture is calculated using the **Laplacian Variance** method. By applying a Laplacian operator to a grayscale version of the image, the system measures the "sharpness" of edges (pores, fine lines, or bumps).



---

## 🛠️ 3. Full Tech Stack

* **Core Language**: Python 3.11+.
* **Computer Vision**: `OpenCV (cv2)` for real-time video stream management and image transformations.
* **UI Framework**: `Tkinter` & `ttk` for a lightweight, cross-platform dashboard.
* **Image Processing**: `PIL (Pillow)` for BGR-to-RGB conversion and Tkinter compatibility.
* **Numerical Computing**: `NumPy` for multi-dimensional array processing (frame data).
* **Data Management**: Python `datetime` and `os` for automated report logging and file I/O.

---

## 📂 4. Project File Structure

```plaintext
Skincare_AI/
├── reports/               # Auto-generated UTF-8 diagnostic files
├── scripts/
│   ├── app_ui.py          # Main GUI, Threading, and Camera Logic
│   └── day6_brain.py      # Recommendation Logic Engine
└── README.md              # Documentation for GitHub/Internships
