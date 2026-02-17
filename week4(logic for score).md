Here is the professional `README.md` file for your project. This document is designed to be your **"Cheat Sheet"** for interviews. It explains the *What*, *Why*, and *How* of every feature we have built so far (Weeks 1-4).

You can create a file named `README.md` in your project folder and paste this content into it.

---

# 🌤️ Sky-AI: Real-Time Intelligent Skin Analysis System

**Author:** Krishna Sharma (NIT Silchar)
**Status:** MVP Completed (Weeks 1-4)
**Tech Stack:** Python, OpenCV, MediaPipe, Pandas, Tkinter

---

## 📖 Project Overview

Sky-AI is a computer vision application that performs real-time dermatological analysis. Unlike standard image filters, it uses **Geometric Face Mesh** and **Color Theory** to isolate skin features (Acne, Oiliness, Texture) and calculates a quantitative **Skin Health Score (0-100)** based on weighted metrics. It also features a "Memory" system to track skin health over time using a CSV database.

---

## ⚙️ System Architecture

### 1. The "Eyes" (Computer Vision)

* **Library:** OpenCV (`cv2`) & MediaPipe
* **Technique:** We use **MediaPipe Face Mesh** to generate a 468-point 3D landmark map of the face.
* **ROI (Region of Interest):**
* **Face Boundary:** Calculated using the **Convex Hull** of the face landmarks to create a mask.
* **Exclusion Zones:** We mathematically subtract the Eyes and Lips from the mask to prevent false positives (e.g., red lips counting as acne).
* **Bitwise Operation:** `cv2.bitwise_and(image, image, mask=skin_mask)` ensures the AI *only* processes valid skin pixels.



### 2. The "Brain" (Mathematical Analysis)

The core logic resides in `skin_analysis.py`. It converts the raw image into data using three distinct algorithms:

#### A. Acne Detection (Color Thresholding)

* **Logic:** Acne appears as inflamed red spots on the skin.
* **Color Space:** Converted BGR to **HSV (Hue, Saturation, Value)** because HSV separates "Color" from "Lighting".
* **Formula:**
```python
Lower Red = [0, 60, 50]   to [10, 255, 255]
Upper Red = [170, 60, 50] to [180, 255, 255]

```


* **Counting:** We use `cv2.findContours` to count distinct red blobs. We filter out noise (area < 3px) and large non-acne objects (area > 1000px).

#### B. Oiliness (Luminance Analysis)

* **Logic:** Oil reflects light, creating "Hotspots" on the T-Zone (Forehead/Nose).
* **Formula:** We extract the **V-Channel (Value/Brightness)** from the HSV image.


* **Threshold:**  is considered Oily.

#### C. Texture (Edge Detection)

* **Logic:** Smooth skin has low variance. Rough skin (scars, pores) has high variance in pixel intensity.
* **Algorithm:** **Laplacian Variance**.


* **Implementation:** `cv2.Laplacian(gray_image, cv2.CV_64F).var()`

---

## 🧮 Week 4: The Skin Health Score Algorithm

To provide a single, understandable metric for the user, we implemented a **Weighted Linear Equation**. This normalizes disparate data types (Counts vs. Percentages) into a 0-100 score.

**The Formula:**


**Where:**

1. ** (Acne Penalty):**
* Weight: **1.5** (High Severity)
* Formula: 
* *Logic:* Acne is the most visible issue, so it heavily impacts the score.


2. ** (Texture Penalty):**
* Weight: **0.5** (Medium Severity)
* Formula: 
* *Logic:* We only penalize texture if it exceeds the "Normal" baseline of 20.


3. ** (Oil Penalty):**
* Weight: **0.5** (Low Severity)
* Formula: 
* *Logic:* Oil is natural; we only penalize excessive oiliness (>50%).



---

## 📂 Project Structure

| File | Description |
| --- | --- |
| `main.py` | The entry point. Launches the Application. |
| `app_ui.py` | **The Frontend.** Handles Tkinter window, Camera thread, and Button events. |
| `skin_analysis.py` | **The Brain.** Contains the `SkinAnalyzer` class, Computer Vision logic, and Math formulas. |
| `data_manager.py` | **The Memory.** Handles reading/writing to `skin_history.csv`. Uses **Pandas**. |
| `recommendation_engine.py` | **The Expert.** Filters `skin_products.csv` to find advice based on skin type. |
| `data/skin_history.csv` | Stores the user's scan history (Date, Time, Scores). |
| `data/skin_products.csv` | The database of dermatological products and rules. |

---

## 🚀 How to Run

1. **Install Dependencies:**
```bash
pip install opencv-python numpy mediapipe pandas pillow

```


2. **Run the App:**
```bash
python main.py

```



---

## 🔮 Future Roadmap (Weeks 5-12)

* **Week 5:** Deep Learning (CNNs) for specific acne classification (Cyst vs. Whitehead).
* **Week 6:** Model Training using TensorFlow/Keras.
* **Week 7:** Cloud Deployment.
