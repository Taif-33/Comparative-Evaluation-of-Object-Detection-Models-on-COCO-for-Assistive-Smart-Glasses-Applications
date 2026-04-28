# Comparative-Evaluation-of-Object-Detection-Models-on-COCO-for-Assistive-Smart-Glasses-Applications

---

## 📌 Project Description
A comprehensive evaluation of 10 state-of-the-art object detection models on the COCO val2017 dataset, optimized for real-time assistive smart-glasses applications for the visually impaired. This project compares two-stage detectors, single-stage anchor-based detectors, anchor-free detectors, and transformer-based architectures to find the optimal balance between inference speed and accuracy.

---

## 📖 Table of Contents
- [Project Overview](#-project-overview)
- [Models Evaluated](#-models-evaluated)
- [Dataset & Methodology](#-dataset--methodology)
- [Key Findings](#-key-findings)
- [Repository Structure](#-repository-structure)
- [Getting Started](#-getting-started)
- [Authors](#-authors)

---

## 🎯 Project Overview
Smart-glasses systems for the visually impaired must detect obstacles, people, and everyday objects in real-time, imposing strict constraints on both accuracy and inference latency. This project addresses the research question: **Which object detection architecture provides the best accuracy-speed trade-off for an assistive smart-glasses system deployed on an edge device?**

We evaluate ten models spanning all major architectural families using a single unified evaluation pipeline (`pycocotools`) to ensure a fair comparison.

---

## 🤖 Models Evaluated
We benchmarked 10 models across different architectural paradigms:

1. **YOLOv7** (Highest Accuracy/Speed Balance)
2. **Faster R-CNN R50-FPN-V2** (High Accuracy, Two-Stage)
3. **YOLOv8s** (Modern Single-Stage)
4. **DETR ResNet-50** (Transformer-based)
5. **RetinaNet R50-FPN-V2** (Focal Loss for Class Imbalance)
6. **YOLOv5s** (Fastest Inference)
7. **CenterNet FCOS R50** (Anchor-Free)
8. **EfficientDet-D0** (Compound Scaling)
9. **SSD300 VGG16** (Classic Single-Stage)
10. **SSD + MobileNetV3** (Lightweight Backbone)

---

## 📊 Dataset & Methodology
- **Dataset:** Microsoft COCO val2017 (5,000 images, 80 object categories)
- **Evaluation Metric:** standard COCO metric (`mAP@0.5:0.95`)
- **Hardware:** NVIDIA Tesla T4 GPU (Google Colab)
- **Standard Configuration:** `conf_threshold = 0.001`, `image_size = 640`, `iou_threshold = 0.5`

We also conducted experiments on **Adversarial Class Imbalance** (simulating crowded environments where "person" dominates) and **Weighted Box Fusion (WBF)** ensembles.

---

## 🏆 Key Findings

### Accuracy vs. Speed Trade-off

| Model | mAP@0.5:0.95 | FPS | Params (M) | Viability for Smart-Glasses |
|---|---|---|---|---|
| **YOLOv7** | **49.70%** | 81 | 36.9 | ✅ Optimal (Best Balance) |
| **YOLOv5s** | 37.40% | **204** | 7.2 | ✅ Excellent for Edge Devices |
| Faster R-CNN | 46.70% | 5.9 | 43.7 | ❌ Too Slow (<30 FPS) |
| YOLOv8s | 43.64% | 55 | 11.2 | ✅ Good Alternative |
| DETR | 42.05% | 10.7 | 41.5 | ❌ Too Slow |

- **Primary Recommendation:** YOLOv7 achieves the highest mAP (49.70%) while maintaining 81 FPS, making it the best overall model for real-time smart-glasses deployment on GPU-equipped devices.
- **Edge Deployment:** YOLOv5s (37.40% mAP, 204 FPS) provides the best real-time performance for extremely latency-sensitive or resource-constrained edge deployments.
- **Ensemble:** A Weighted Box Fusion (WBF) ensemble of YOLOv7, Faster R-CNN, and RetinaNet achieves the highest overall accuracy (**53.80% mAP**) but drops to 4.8 FPS, making it unsuitable for real-time use.

---

## 🚀 Getting Started

### Prerequisites
The project is designed to run in **Google Colab** to ensure standardized GPU access (NVIDIA T4) and reproducible environments.

### Installation & Execution
1. Open `notebooks/Object_Detection_COCO_Complete.ipynb` in Google Colab.
2. Ensure the Runtime type is set to **GPU** (`Runtime > Change runtime type > T4 GPU`).
3. Run the **"Shared Setup"** cells to mount Google Drive and download the COCO val2017 dataset.
4. Execute the specific model cells to install dependencies (e.g., `ultralytics`, `torchvision`, `transformers`) and run the evaluation pipeline.

---

## 👥 Authors
This project was developed for the **CS 4082: Machine Learning** course (Spring 2026) at **Effat University**, under the instruction of **Dr. Naila Marir**.

- **Rama Alkusair** (Member 1) — Evaluated YOLOv5s, SSD300 VGG16, RetinaNet R50-FPN-V2
- **Taif Alsulami** (Member 2) — Evaluated Faster R-CNN, YOLOv7, EfficientDet-D0
- **Sana Rahmani** (Member 3) — Evaluated YOLOv8s, SSD+MobileNetV3, DETR, CenterNet


