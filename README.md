# Pen Detection with YOLOv11s

This project implements an object detection system for identifying different pen types using the YOLOv11s (You Only Look Once) model. The system can detect five different pen types: Frixion, HTW, Muji, Round Stic, and Starpie.



## Project Structure

```
├── dataset/
│   ├── HEICtoPNG_converter.ipynb   # Utility for converting HEIC images to PNG format
│   └── labeled/                    # Contains labeled training data
│       ├── classes.txt             # List of object classes (pen types)
│       ├── images/                 # Training images (180+ images)
│       ├── labels/                 # YOLO format annotation files
│       └── notes.json              # Additional metadata
├── results/                        # Training results and model artifacts
│   ├── confusion_matrix.png        # Model evaluation visualization
│   ├── other visualization files   # Performance curves and metrics
│   ├── results.csv                 # Training metrics
│   └── weights/                    # Trained model weights
│       ├── best.pt                 # Best model checkpoint
│       └── last.pt                 # Last model checkpoint 
├── requirements_.txt               # Project requirements
├── YOLO11s.ipynb                   # Jupyter notebook used for model training
├── args.yaml                       # Training configuration
├── my_model.pt                     # Exported model for deployment
└── yolo_detect.py                  # Run this file for deployment 
```

## Requirements

- Python 3.8+
- OpenCV
- NumPy
- Ultralytics YOLO
- PyTorch

## Installation

1. Clone this repository:

```bash
git clone <https://github.com/HayateSato/YOLO11---object-detection.git>
cd <dir_path_where_you_cloned_this_projectFile>
```

2. Install required packages:

```bash
pip install ultralytics opencv-python numpy
```

3. Run this file (it will activate the camera and the model will run)

```bash
python yolo_detect.py --model <model file.pt> --source <image/video file OR webcam port (read below for detail)>
```

## Deployment

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

- This project was trained using the YOLOv11s model. 
- (YOLOv8n was trained as well but YOLOv11s outpeformed)
- The training process can be found in the `YOLO11s.ipynb` notebook.

Key training parameters:
- Model: YOLOv11s
- Image size: 640x640
- Batch size: 16
- Epochs: 60
- Augmentation: Random augmentation, scaling, flipping, etc.

## Dataset

The dataset consists of 200 images of various pens with corresponding YOLO-format annotation files. The classes are:
1. frixion
2. htw
3. muji
4. round_stic
5. starpie

Anotation was done by using [Label Studio](https://labelstud.io/)

## Performance

Training results and model performance metrics can be found in the `results/` directory. The model was trained for 60 epochs with standard YOLO loss functions.


## Acknowledgements

- [Ultralytics YOLO](https://github.com/ultralytics/ultralytics) 
- [Edje Electronics](https://www.youtube.com/watch?v=r0RspiLG260&t=641s)
