# Car Detection System

A comprehensive car detection system built on YOLOv5, providing real-time vehicle detection and classification capabilities.

## 🚗 Overview

This project implements a state-of-the-art car detection system using YOLOv5 (You Only Look Once version 5), a fast and accurate object detection model. The system can detect various types of vehicles including cars, trucks, buses, and motorcycles in images and video streams.

## ✨ Features

- **Real-time Detection**: Fast inference for live video streams
- **Multiple Vehicle Types**: Detects cars, trucks, buses, motorcycles, and more
- **High Accuracy**: State-of-the-art YOLOv5 models for precise detection
- **Multiple Input Formats**: Supports images, videos, and webcam streams
- **Easy Training**: Tools for custom dataset training
- **Export Options**: Convert models to various formats (ONNX, TensorRT, etc.)
- **Web Interface**: Optional Flask REST API for easy integration

## 🛠️ Installation

### Prerequisites

- Python 3.8 or higher
- CUDA-compatible GPU (optional, for faster inference)

### Quick Start

1. **Clone the repository**
   ```bash
   git clone https://github.com/SoObai/Car-Detection-System.git
   cd Car-Detection-System
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Download pre-trained weights** (optional)
   ```bash
   # Download YOLOv5s weights
   wget https://github.com/ultralytics/yolov5/releases/download/v7.0/yolov5s.pt
   ```

## 🚀 Usage

### Basic Detection

#### Detect cars in an image
```bash
python detect.py --source path/to/image.jpg --weights yolov5s.pt
```

#### Detect cars in a video
```bash
python detect.py --source path/to/video.mp4 --weights yolov5s.pt
```

#### Real-time webcam detection
```bash
python detect.py --source 0 --weights yolov5s.pt
```

### Advanced Options

#### Save results
```bash
python detect.py --source path/to/image.jpg --weights yolov5s.pt --save-txt --save-conf
```

#### Adjust confidence threshold
```bash
python detect.py --source path/to/image.jpg --weights yolov5s.pt --conf 0.5
```

#### Use different model sizes
```bash
# YOLOv5n (nano) - fastest
python detect.py --weights yolov5n.pt

# YOLOv5s (small) - balanced
python detect.py --weights yolov5s.pt

# YOLOv5m (medium) - more accurate
python detect.py --weights yolov5m.pt

# YOLOv5l (large) - very accurate
python detect.py --weights yolov5l.pt

# YOLOv5x (extra large) - most accurate
python detect.py --weights yolov5x.pt
```

## 🎯 Training

### Train on Custom Dataset

1. **Prepare your dataset** in YOLO format:
   ```
   dataset/
   ├── images/
   │   ├── train/
   │   └── val/
   └── labels/
       ├── train/
       └── val/
   ```

2. **Create dataset configuration** (`data/cars.yaml`):
   ```yaml
   path: ../dataset
   train: images/train
   val: images/val
   nc: 1  # number of classes
   names: ['car']  # class names
   ```

3. **Start training**:
   ```bash
   python train.py --data data/cars.yaml --weights yolov5s.pt --epochs 100
   ```

### Training Options

#### Resume training
```bash
python train.py --resume runs/train/exp/weights/last.pt
```

#### Multi-GPU training
```bash
python train.py --data data/cars.yaml --weights yolov5s.pt --device 0,1
```

#### Hyperparameter tuning
```bash
python train.py --data data/cars.yaml --weights yolov5s.pt --hyp data/hyps/hyp.scratch-high.yaml
```

## 📊 Validation

### Validate trained model
```bash
python val.py --weights runs/train/exp/weights/best.pt --data data/cars.yaml
```

### Validate with custom confidence
```bash
python val.py --weights runs/train/exp/weights/best.pt --data data/cars.yaml --conf 0.5
```

## 🔧 Model Export

### Export to different formats

#### ONNX format
```bash
python export.py --weights yolov5s.pt --include onnx
```

#### TensorRT format
```bash
python export.py --weights yolov5s.pt --include engine --device 0
```

#### CoreML format
```bash
python export.py --weights yolov5s.pt --include coreml
```

#### TensorFlow formats
```bash
python export.py --weights yolov5s.pt --include saved_model pb tflite
```

## 🌐 Web API

### Start Flask REST API
```bash
python utils/flask_rest_api/restapi.py
```

### API Usage
```bash
curl -X POST "http://localhost:5000/v1/object-detection/yolov5s" \
     -H "Content-Type: image/jpeg" \
     --data-binary @path/to/image.jpg
```

## 📁 Project Structure

```
Car-Detection-System/
├── detect.py              # Detection script
├── train.py               # Training script
├── val.py                 # Validation script
├── export.py              # Model export script
├── requirements.txt       # Python dependencies
├── models/                # Model configurations
│   ├── yolo.py           # YOLO model definition
│   ├── common.py         # Common model components
│   └── hub/              # Pre-configured models
├── data/                  # Dataset configurations
│   ├── coco.yaml         # COCO dataset config
│   └── hyps/             # Hyperparameter files
├── utils/                 # Utility functions
│   ├── general.py        # General utilities
│   ├── plots.py          # Plotting functions
│   ├── torch_utils.py    # PyTorch utilities
│   └── flask_rest_api/   # Web API
├── classify/              # Classification module
└── segment/               # Segmentation module
```

## 🎨 Supported Datasets

- **COCO**: Common Objects in Context
- **VOC**: Pascal VOC
- **ImageNet**: Large-scale image classification
- **Custom**: Your own datasets

## 🔍 Detection Classes

The system can detect various vehicle types:
- Car
- Truck
- Bus
- Motorcycle
- Bicycle
- And more (depending on training data)

## 📈 Performance

| Model | Size | Speed (ms) | mAP@0.5 | mAP@0.5:0.95 |
|-------|------|------------|---------|--------------|
| YOLOv5n | 1.9M | 6.3 | 28.0 | 45.7 |
| YOLOv5s | 7.2M | 6.4 | 37.4 | 56.8 |
| YOLOv5m | 21.2M | 8.2 | 45.4 | 64.1 |
| YOLOv5l | 46.5M | 10.1 | 49.0 | 67.3 |
| YOLOv5x | 87.7M | 12.1 | 50.7 | 68.9 |

*Performance metrics on COCO dataset*

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.

### How to Contribute

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [Ultralytics](https://github.com/ultralytics/yolov5) for the YOLOv5 implementation
- [PyTorch](https://pytorch.org/) for the deep learning framework
- The open-source community for various tools and libraries

## 📞 Support

If you encounter any issues or have questions:

1. Check the [Issues](https://github.com/SoObai/Car-Detection-System/issues) page
2. Create a new issue with detailed information
3. Join our community discussions

## 🔄 Updates

Stay updated with the latest features and improvements by:
- Starring this repository
- Watching for updates
- Following our release notes

---

**Made with ❤️ for the computer vision community**
