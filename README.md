# Pen Detection with YOLOv11s

This project implements an object detection system for identifying different pen types using the YOLOv11s (You Only Look Once) model. The system can detect five different pen types: Frixion, HTW, Muji, Round Stic, and Starpie.

## Project Structure

```
├── dataset/
│   ├── HEICtoPNG_converter.ipynb    # Utility for converting HEIC images to PNG format
│   ├── labeled/                    # Contains labeled training data
│       ├── classes.txt             # List of object classes (pen types)
│       ├── images/                 # Training images (180+ images)
│       ├── labels/                 # YOLO format annotation files
│       └── notes.json              # Additional metadata
│   └── original/                   # Original unlabeled images (if any)
├── train/                          # Training results and model artifacts
│   ├── args.yaml                   # Training configuration
│   ├── confusion_matrix.png        # Model evaluation visualization
│   ├── other visualization files   # Performance curves and metrics
│   ├── results.csv                 # Training metrics
│   └── weights/                    # Trained model weights
│       ├── best.pt                 # Best model checkpoint
│       └── last.pt                 # Last model checkpoint
├── my_model.pt                     # Exported model for inference
├── YOLO11s.ipynb                   # Jupyter notebook for model training
└── yolo_detect.py                  # Detection script for inference
```

## Requirements

- Python 3.8+
- OpenCV
- NumPy
- Ultralytics YOLO
- PyTorch
- (Optional) picamera2 for Raspberry Pi camera support

## Installation

1. Clone this repository:

```bash
git clone <repository-url>
cd <repository-directory>
```

2. Install required packages:

```bash
pip install ultralytics opencv-python numpy
```

3. For Raspberry Pi camera support (optional):

```bash
pip install picamera2
```

## Usage

### Running the Detection Script

The main inference script is `yolo_detect.py`, which can process images, folders of images, video files, or camera feeds:

```bash
python yolo_detect.py --model my_model.pt --source <source> [--thresh 0.5] [--resolution 640x480] [--record]
```

Arguments:
- `--model`: Path to the trained YOLO model file (required)
- `--source`: Input source, can be:
  - Image file: `test.jpg`
  - Directory of images: `test_dir`
  - Video file: `video.mp4`
  - USB camera: `usb0` (where 0 is the camera index)
  - Raspberry Pi camera: `picamera0`
- `--thresh`: Confidence threshold for detections (default: 0.5)
- `--resolution`: Output resolution in WxH format (e.g., `640x480`)
- `--record`: Flag to record video output to file (requires --resolution to be specified)

### Controls During Inference

While the detection is running:
- Press `q` to quit
- Press `s` to pause detection
- Press `p` to save a screenshot of the current frame with detections

### Training Your Own Model

This project was trained using the YOLOv11s model. The training process can be found in the `YOLO11s.ipynb` notebook.

Key training parameters:
- Model: YOLOv11s
- Image size: 640x640
- Batch size: 16
- Epochs: 60
- Augmentation: Random augmentation, scaling, flipping, etc.

## Dataset

The dataset consists of over 180 images of various pens with corresponding YOLO-format annotation files. The classes are:
1. frixion
2. htw
3. muji
4. round_stic
5. starpie

## Performance

Training results and model performance metrics can be found in the `train/` directory. The model was trained for 60 epochs with standard YOLO loss functions.

## License

[Specify your license information here]

## Acknowledgements

- [Ultralytics YOLO](https://github.com/ultralytics/ultralytics) for the YOLO implementation
- [Add any other acknowledgements or references]
