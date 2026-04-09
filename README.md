# 🚗 TraffIQ - Autonomous Vehicle AI  

## 📌 Overview  
TraffIQ is an autonomous driving system that uses deep learning models to control a vehicle in real-time using camera input. It combines **lane-following (end-to-end steering)** and **obstacle detection (YOLO)** to make intelligent driving decisions.

---

## 🧠 Features  
- 🚘 End-to-end lane detection using neural networks  
- 🚧 Real-time obstacle detection and avoidance (YOLO)  
- ⚡ Dynamic throttle and steering control  
- 🔁 Closed-loop control with simulator feedback  
- 🧩 Modular architecture (easy to extend)

---

## ⚙️ Tech Stack  
- Python  
- OpenCV  
- ONNX Runtime  
- TensorFlow / PyTorch (for training)  
- Socket.IO + Flask (real-time communication)  

---

## 🚀 How to Run  

```bash
pip install -r requirements.txt
python src/main.py
```

```mermaid
flowchart TD

A[Start Server] --> B[Connect to Simulator]
B --> C[Receive Telemetry Data]

C --> D[Decode Base64 Image]
D --> E[Convert to NumPy Array]

%% Steering Branch
E --> F1[Steering Preprocess]
F1 --> F2[Crop + YUV + Gray + Resize]
F2 --> F3[ONNX Steering Model]
F3 --> F4[Steering Angle Output]

%% YOLO Branch
E --> G1[YOLO Preprocess]
G1 --> G2[Resize 640x640 + Normalize]
G2 --> G3[YOLO ONNX Model]
G3 --> G4[Detection Outputs]
G4 --> G5[Filter by Confidence]
G5 --> G6[Analyze Obstacles]
G6 --> G7[Obstacle Position + Area]

%% Decision Layer
F4 --> H[Decision Layer]
G7 --> H

H --> I[Adjust Steering]
H --> J[Compute Throttle]

I --> K[Clamp Steering]
J --> L[Speed Limiting + Clamp]

K --> M[Send Control]
L --> M

M --> N[Emit Steering + Throttle]
N --> C

%% Error Handling
C -->|Error| X[Print Error]
X --> C
```
