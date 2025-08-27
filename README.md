
# VisionCraft – Comprehensive Traffic Sign Classification & Multi-Category Object Segmentation using OpenCV

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)]()
[![OpenCV](https://img.shields.io/badge/OpenCV-4.x-green.svg)]()
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)]()

This repository contains the **full implementation and documentation** of the third Multimedia Systems assignment,  
featuring two major computer vision pipelines, built entirely in **Python** and **OpenCV**, with optional deep learning components for benchmarking.

---

## **Project Overview**
This project is organized into two core tasks:

- **Q1 – Traffic Sign Detection & Classification**  
  Implements full pipelines for detecting and classifying road signs based **solely** on classical computer vision methods (color, shape, and contour analysis), with optional CNN benchmarking. Covers both **single-sign** and **multi-sign** images.

- **Q2 – Multi-Category Object Segmentation**  
  Automatically detects and separates multiple object categories from composite images (digits, fruits, animals) and reconstructs their positions in category-specific canvases.

Both tasks were developed to meet the academic requirements of the Multimedia Systems course, while being directly applicable to real-world perception systems.

---

## **Part 1 – Traffic Sign Detection & Classification**

### **Objectives**
- Classify road signs into **Warning**, **Prohibitory**, **Informative/Service**, and **Route Guidance** categories based on geometric and chromatic cues.
- Handle both images containing **a single sign** and images containing **multiple signs simultaneously**.
- Design a **10-class classifier** to distinguish specific road sign types using:
  - Classical OpenCV-based pipeline
  - CNN-based deep learning model for performance comparison

### **Key Features**
- **Color Space Segmentation** in HSV domain for robust separation of red and blue signs.
- **Shape Analysis** for distinguishing circles, triangles, rectangles, and squares.
- **ROI Extraction** in multi-sign scenarios.
- **Strict Mode Circle Verification** for robust prohibitory sign detection.
- **Quantitative Evaluation** including per-class accuracy, confusion matrices, and processing time.

---

## **Part 2 – Multi-Category Object Segmentation**

### **Objectives**
- Detect and isolate **mixed-category objects** in a single image without human intervention.
- Output per-class images preserving:
  - Original scale & proportions
  - Original positions within the scene
  - Background consistency (white)

### **Targeted Classes**
1. **Digits:** 7, 8, 9  
2. **Fruits:** Apple, Banana, Cucumber  
3. **Animals:** Lion, Deer, Elephant  

### **Key Features**
- **Template-based Contour Matching** for robust shape/class association.
- **Per-Class Canvas Assembly** using `build_per_class_canvases`.
- **Grid Visualization** with `show_inplace_3x3_grid`.

---

## **Methodological Framework**

### **Q1: Traffic Sign Pipeline**
1. **Preprocessing & Mask Extraction**
   - Convert input images **BGR → HSV**.
   - Apply dual red range masks (`mask_red_1`, `mask_red_2`) and single blue mask.
   - Merge and refine masks using morphological **OPEN**/**CLOSE** with elliptical kernels.

2. **Feature Extraction**
   - Select largest contour from mask.
   - Derive:
     - Vertex count (`approxPolyDP`)
     - Rotated aspect ratio (`minAreaRect`)
     - Fill ratio vs bounding rectangle
     - Circularity (`4π * Area / Perimeter²`)
     - Area and perimeter metrics

3. **Strict Circle Check**
   - Enforce tolerance thresholds to reduce false positives in prohibitory signs.

4. **Classification Rules**
   - Triangle → Warning
   - Circle → Prohibitory
   - Square/Rectangle → Informative or Route Guidance

5. **Multi-Sign Handling**
   - Detect and crop bounding boxes.
   - Independently classify each ROI.

6. **10-Class Classification**
   - Method 1: Classical contour + template matching
   - Method 2: CNN trained with augmented dataset
   - Quantitative comparison and qualitative error analysis

---

### **Q2: Object Grouping Pipeline**
1. **Mask & Contour Extraction**
   - Generate binary masks for object regions.
   - Identify individual contours.

2. **Contour Matching**
   - Compare extracted contours to predefined templates for 9 total classes.
   - Assign detected objects to correct class.

3. **Per-Class Canvas Reconstruction**
   - Preserve exact position & scale in blank background canvases for each class.

4. **Result Visualization**
   - Arrange per-class images in 3x3 grid format for collective display.

---

## **Repository Structure**
```
├── main.ipynb              # Full implementation of Q1 & Q2
├── Multimedia HW 3.pdf     # Problem statement & requirements
├── گزارشکار مولتی 3.pdf     # Detailed Farsi project report
├── sample_images/          # Example input images for Q1 & Q2
├── outputs_strict/         # Detection/classification outputs for Q1
├── outputs_q2/             # Segmentation & grouping outputs for Q2
└── README.md               # Project documentation
```

---

## **Installation**
```bash
git clone https://github.com/Seyed07/opencv-traffic-sign-and-object-segmentation.git
cd opencv-traffic-sign-and-object-segmentation
pip install opencv-python numpy matplotlib
```
Optional for CNN-based classification:
```bash
pip install tensorflow keras
```

---

## **Usage Instructions**
To launch via Jupyter Notebook:
```bash
jupyter notebook main.ipynb
```
Outputs will be saved to:
- `outputs_strict/` for Part 1  
- `outputs_q2/` for Part 2

---

## **Results & Visual Output**

### **Traffic Sign Detection (Q1)**
| Input | Output |
|-------|--------|
| <img width="400" height="300" alt="Screenshot 2025-08-27 203413" src="https://github.com/user-attachments/assets/9db9e4f3-707e-4ac5-9fef-7fd86b0d420b" /> | <img width="400" height="300" alt="output" src="https://github.com/user-attachments/assets/234f2d0b-27e1-4b2f-adda-d648824ffba8" /> |

---

### **Object Segmentation (Q2)**
| Input | Output |
|-------|--------|
| <img width="1389" height="577" alt="1" src="https://github.com/user-attachments/assets/a3cfe342-2017-4228-8fe2-585bac0389d7" /> | <img width="1327" height="944" alt="2" src="https://github.com/user-attachments/assets/255e8c0d-7015-4b14-88ee-70a2e7767975" /> |


