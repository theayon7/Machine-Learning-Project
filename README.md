This project addresses the challenge of object detection in aerial imagery, specifically focusing on the Aerial Vehicle OBB (Oriented Bounding Box) Dataset. The study benchmarks modern object detection architectures against label-efficient learning strategies to solve unique challenges like arbitrary object orientation, scale variation, and background clutter in overhead views.
+1

The project is divided into three methodological approaches:


Supervised Baseline: Establishing performance benchmarks using YOLOv10, YOLOv11, and YOLOv12.


Semi-Supervised Learning (SSL): Leveraging unlabeled data using the STAC (Self-Training with Augmentation Consistency) framework.


Self-Supervised Learning (Self-SL): Learning robust features without labels using BYOL and SimCLR before fine-tuning.

📊 Key Results
Our experiments demonstrate that label-efficient methods offer viable alternatives to fully supervised learning in data-constrained scenarios.
Model / Method,mAP@0.5,mAP@0.5:0.95,Precision,Recall,F1 Score
Baseline (YOLOv10s),0.8456,0.5664,0.8422,0.7741,0.8061
Baseline (YOLOv11n),0.8122,0.5302,0.8255,0.7434,0.7814
Baseline (YOLOv12n),0.8198,0.5371,0.8360,0.7465,0.7875
Semi-Supervised (STAC),0.8429,0.5632,0.8382,0.7737,0.8040
Self-Supervised (BYOL),0.7860,0.5110,0.8014,0.7132,0.7534
Self-Supervised (SimCLR),0.7745,0.4977,0.7904,0.7085,0.7456


📂 Dataset

Name: Aerial Vehicle Oriented Bounding Box (OBB) Dataset.


Format: YOLOv11-OBB (<class_id> <x1> <y1> <x2> <y2> <x3> <y3> <x4> <y4>).


Total Images: 29,125.

Classes:


Small Vehicle (e.g., sedans, compact cars).


Large Vehicle (e.g., trucks, buses, freight carriers).


Splits: Training (18,274), Validation (5,420), Test (5,431).

🛠️ Methodology & Architecture
1. Baseline Models

YOLOv10s: Chosen for its NMS-free training and consistent dual assignments.


YOLOv11n / YOLOv12n: Selected for enhanced backbones and efficiency in detecting small, high-density objects.

2. Semi-Supervised Learning (STAC)
Mechanism: Uses a "Teacher" model trained on labeled data to generate pseudo-labels for unlabeled data. A "Student" model is then trained on strongly augmented versions of this data to enforce consistency.
+1


Confidence Threshold: 0.7 (Only detections ≥ 75% confidence are used as pseudo-labels).

Augmentations: Weak (Flip, Resize) for Teacher; Strong (Gaussian Blur, Color Jitter) for Student.

3. Self-Supervised Learning

BYOL (Bootstrap Your Own Latent): Uses Online and Target networks to predict latent representations without negative pairs.
+1


SimCLR: Maximizes agreement between augmented views of the same image using NT-Xent loss and negative pairs.


Pre-training: Models are pre-trained on the entire dataset without labels before fine-tuning the detector.

⚙️ Experimental Setup

Environment: Kaggle Notebooks (Cloud Computing).


Hardware: Dual NVIDIA Tesla T4 GPUs (2x 16GB VRAM).


Frameworks: PyTorch, Ultralytics YOLOv10/v11/v12.


Training Configuration: Distributed Data Parallel (DDP) with Mixed Precision (FP16).

🚀 Conclusion
The study identifies the YOLOv10s + Semi-Supervised (STAC) combination as the most effective framework for label-limited scenarios. While the supervised baseline offers the highest performance, STAC matches it closely (0.84 mAP) while reducing the need for manual annotation. BYOL proved to be more stable than SimCLR for aerial feature extraction.
+4

👥 Authors

Ayon Adhikary (ID: 2022-3-60-137) 


Shanghita Naha Sristy (ID: 2022-3-60-311) 


Submitted to Dr. Md. Rifat Ahmmad Rashid, Dept. of CSE, East West University.
