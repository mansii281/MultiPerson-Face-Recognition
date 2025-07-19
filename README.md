# 🚀 FaceTrackR - MultiPerson Face Recognition System

## 🔍 Overview

**FaceTrackR** is a deep learning-powered real-time **multi-face detection and recognition** system built using cutting-edge computer vision libraries. It combines **MTCNN** for accurate face detection and **DLIB** for high-quality face recognition, all optimized for **GPU acceleration** to deliver fast and reliable performance.

Designed for scenarios like **automated attendance systems**, **security surveillance**, and **live monitoring**, FaceTrackR is scalable, modular, and ready for deployment on GPU-enabled infrastructures including **NVIDIA DGX** and **CUDA-supported devices**.

---

## 🎯 Aim

To detect and recognize **multiple faces** in real-time with high accuracy and optimized performance using **GPU acceleration** on systems like NVIDIA DGX or CUDA-supported machines.

---

## 🛠 Applications

- 📋 **Automated Attendance** — Contactless, real-time tracking of individuals in classrooms, offices, or events.  
- 🛡️ **Surveillance** — Intelligent monitoring of live feeds with alert capabilities.  
- 👥 **Multi-person Identification** — Seamless identity recognition in crowded scenarios.

---

## 🚀 Key Features

- ⚡ **High-speed GPU acceleration** with CUDA for real-time performance.
- 👥 **Multi-face detection** using MTCNN (Multi-task Cascaded Convolutional Networks).
- 🧠 **Face recognition** via DLIB’s face embeddings for robust matching.
- 🔁 **Buffer handling** using intelligent **LOCK/UNLOCK** mechanism to prevent deadlocks.
- 🧩 Supports **single-frame**, **multi-frame**, and **batched frame** processing.
- 🎥 **OpenCV-based** real-time frame-wise processing.
- 📐 **Dynamic resolution management** via downsampling/upsampling.
- 🌐 **Web interface** with Flask for live video stream monitoring.
- 💾 **Local storage** of processed frames with metadata for later analysis.

---

## 🧰 Tech Stack

| Tech | Description |
|------|-------------|
| **Python 3.8+** | Core programming language |
| **OpenCV** | Video capture, frame manipulation |
| **TensorFlow** | Backend for MTCNN model |
| **MTCNN** | Deep learning-based face detector |
| **DLIB** | Face embedding & recognition |
| **CUDA** | GPU acceleration for performance |
| **Flask** | Web-based monitoring |
| **NumPy & Pandas** | Data manipulation |

---

## 🧾 Code Snippet: Drawing Bounding Boxes on Detected Faces

```python
for face in faces:
    x, y, w, h = face['box']
    cv2.rectangle(image, (x, y), (x + w, y + h), (0, 255, 0), 2)

output_path = "output.jpg"
cv2.imwrite(output_path, image)
print("Output saved successfully at:", output_path)
```

---

## ⚙️ Project Setup

### 🔄 1. Clone the Repository

```bash
git clone https://github.com/mansii281/MutliPerson-Face-Recognition.git
cd multiperson_face_recognition
```

### 🧪 2. Set Up Virtual Environment

```bash
python -m venv myenv
```

### ▶️ 3. Activate the Virtual Environment

- **Windows:**
```bash
myenv\Scripts\activate
```
- **Linux/macOS:**
```bash
source myenv/bin/activate
```

### 📦 4. Install Dependencies

```bash
pip install tensorflow mtcnn opencv-python dlib flask numpy pandas
```

### 🚀 5. Run the Application

```bash
python app.py
```

---

## 📡 Deployment on NVIDIA DGX A100

### 🌐 1. Access the DGX Server

Navigate to the application in your browser:

```
http://<DGX_IP>:<application_port>
```

### 📂 2. Transfer Files to DGX Server

```bash
scp -r -P <port_number> <local_folder> user@<DGX_IP>:<remote_folder>
```

### 🧠 3. Run the Application

```bash
python3 app.py
```

---

## 🔒 Buffer Management & Optimization

- Automatically **cleans buffer** when frame queue exceeds a defined threshold (e.g., 10 frames).
- Uses **thread-safe locks** to handle batched frame processing.
- Prevents race conditions and **deadlocks** via `LOCK/UNLOCK` strategy.

---

## 📦 Deployment Script (`deploy.sh`)

```bash
#!/bin/bash

echo "🚀 Setting up FaceTrackR environment..."

# Step 1: Create virtual environment
python3 -m venv facetrackr_env
source facetrackr_env/bin/activate

# Step 2: Upgrade pip
pip install --upgrade pip

# Step 3: Install dependencies
pip install tensorflow mtcnn opencv-python dlib flask numpy pandas

# Step 4: Run the app
echo "✅ Setup complete. Starting the app..."
python app.py
```

> Save as `deploy.sh` and run:
```bash
chmod +x deploy.sh
./deploy.sh
```

---

## 🐳 Docker Support

### `Dockerfile`
```dockerfile
FROM python:3.8-slim

RUN apt-get update && \
    apt-get install -y cmake libboost-all-dev libgtk2.0-dev libsm6 libxext6 libxrender-dev && \
    pip install --upgrade pip

WORKDIR /app
COPY . /app

RUN pip install tensorflow mtcnn opencv-python dlib flask numpy pandas

EXPOSE 5000
CMD ["python", "app.py"]
```

### `.dockerignore`
```
__pycache__/
*.pyc
*.pyo
*.pyd
venv/
facetrackr_env/
*.log
output.jpg
```

### Build & Run
```bash
docker build -t facetrackr .
docker run -p 5000:5000 facetrackr
```

---

## 📌 To-Do / Future Enhancements

- [ ] Add face enrollment via web interface  
- [ ] Integrate database for attendance logs  
- [ ] Implement alert system for unknown faces  
- [ ] Optimize memory for large-scale frame processing  
- [ ] Add support for edge devices (Jetson Nano, Raspberry Pi 5)  

---
