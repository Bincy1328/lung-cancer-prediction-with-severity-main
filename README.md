# Lung Disease Prediction using YOLOv8

## 📌 Project Overview
This project uses **Ultralytics YOLOv8** to detect lung diseases (**Cancer Malignant, Nodule, Multiple Nodules**) from images. The dataset consists of **10,780 images** split into training, validation, and test sets. The model is trained for **50 epochs** using **NVIDIA CUDA** for acceleration.

---

## ⚙️ Installation & Setup
### **1️⃣ Clone the Repository**
Run the following command to clone the repository and navigate into the project folder:
```bash
git clone <repo_name>
cd <repo_name>
```

### **2️⃣ Prerequisites**
Ensure you have:
- **Python 3.12.3** installed.
- **CUDA drivers** installed (for GPU acceleration with NVIDIA GPUs).
- **Ultralytics YOLOv8** installed.

### **3️⃣ Install Dependencies**
Run the following command to install the required Python packages:
```bash
pip install -r requirements.txt
```

### **4️⃣ Configure Ultralytics Settings**
To check and configure **Ultralytics settings**, run:
```bash
yolo settings
```
Update the `settings.json` file as required (especially paths and device settings for CUDA).

---

## 🏋️ Training the Model
### **1️⃣ Configure the Dataset**
Ensure your dataset directory has a `data.yaml` file specifying paths to images and labels. Example:
```yaml
train: ./train/images
val: ./valid/images
test: ./test/images
nc: 3
names: ['Cancer Malignant', 'Nodule', 'Multiple Nodules']
```

### **2️⃣ Run YOLOv8 Training**
Navigate to the dataset folder and execute:
```bash
yolo train data=data.yaml model=yolov8n.pt epochs=50
```
This will:
- Train YOLOv8 on the dataset for 50 epochs.
- Save the best weights in `runs/detect/train/weights/best.pt`.

---

## 🎯 Running Inference & Streamlit App
### **1️⃣ Running Inference on Test Images**
Use the following script to test the trained model:
```python
from ultralytics import YOLO
import torch

model = YOLO("runs/detect/train/weights/best.pt")
device = 'cuda' if torch.cuda.is_available() else 'cpu'
model.to(device)

# Run inference on a sample image
results = model("test_images/sample.jpg")
results.show()
results.save("output_detected.jpg")
```

### **2️⃣ Running Streamlit App**
To launch the web app, run:
```bash
streamlit run main.py
```
Then, open **localhost:8501** in your browser, upload an image, and get the predictions.

---

## 📊 Model Performance Metrics
| Metric       | Score  |
|-------------|--------|
| **mAP@50**  | 0.986  |
| **mAP@50-95** | 0.922  |
| **Precision** | 0.975  |
| **Recall**    | 0.975  |

The trained model achieves **high accuracy** and can reliably detect lung disease patterns in images.

---

## 🎬 Demo
Here’s a visual demonstration of the project workflow:
1. **After clicking the localhost link:**
   ![Demo 1](demo/demo_1.png)
2. **Detection result displayed:**
   ![Demo 2](demo/demo_2.png)
3. **Full-screen detection image:**
   ![Demo 3](demo/demo_3.png)
4. **Demo Video:**
   ![Demo Video](demo/demo_video.mp4)

---

## 📄 Project Reports
For detailed insights and documentation, refer to:
- **[Project Report (DOC)](demo/report.docx)**
- **[Project Report (PDF)](demo/report.pdf)**

