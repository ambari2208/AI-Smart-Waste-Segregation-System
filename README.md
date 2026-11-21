# AI-Powered Smart Waste Segregation System

An intelligent waste segregation system that combines deep learning, computer vision, and embedded hardware to automate the identification and sorting of waste into four categories: Plastic, E-Waste, Organic, and Recyclable.

The system uses **EfficientNet-B0** for image classification, integrates the **Google Gemini API**, and connects a **Raspberry Pi 5** with an **Arduino UNO** to control the physical waste segregation mechanism.

## Project Overview

Improper waste disposal and the mixing of recyclable and non-recyclable materials create significant environmental challenges. This project explores an automated approach to waste segregation using artificial intelligence and hardware-based automation.

A camera captures an image of the waste item, the trained deep learning model predicts its category, and the hardware mechanism directs the item into its corresponding compartment.

The system combines AI-based classification with motor control to demonstrate an end-to-end smart waste segregation solution.

## Waste Categories

| Category | Description |
|---|---|
| **PLASTIC** | Plastic waste materials |
| **E_WASTE** | Electronic waste |
| **ORGANIC** | Biodegradable waste |
| **RECYCLABLE** | Recyclable materials |

## Key Features

- **Deep Learning Classification:** Waste identification using the EfficientNet-B0 architecture.
- **Gemini API Integration:** Google Gemini API integration within the system.
- **Local Prediction:** EfficientNet-B0-based local classification fallback.
- **Real-Time Camera Input:** Image capture and processing using OpenCV.
- **Hardware Automation:** Raspberry Pi 5 and Arduino UNO integration.
- **Automated Sorting:** Servo and stepper motor-based waste routing.
- **Motion Control Interface:** PyQt6-based graphical interface.
- **Safety Mechanisms:** Limit-switch-based homing and movement protection.
- **Dataset Processing:** Tools for dataset cleaning, duplicate detection, and evaluation.

## System Architecture

The system follows a sequence of image acquisition, AI-based classification, and hardware-controlled waste segregation.

### Processing Workflow

1. **Image Capture:** A USB camera captures an image of the waste item.
2. **Image Processing:** The captured image is processed using computer vision techniques.
3. **Waste Classification:** EfficientNet-B0 predicts the waste category. Gemini API integration is also included in the system.
4. **Category Mapping:** The predicted category is mapped to its corresponding waste compartment.
5. **Hardware Communication:** The Raspberry Pi communicates with the Arduino UNO.
6. **Motor Control:** The Arduino controls the servo and stepper motor.
7. **Waste Segregation:** The mechanism directs the waste item into the selected compartment.

## Technology Stack

### Artificial Intelligence and Software

| Technology | Purpose |
|---|---|
| Python | Main programming language |
| PyTorch | Deep learning framework |
| Torchvision | Image transformations and model utilities |
| EfficientNet-B0 | Waste classification model |
| OpenCV | Image capture and processing |
| Google Gemini API | AI API integration |
| PyQt6 | Graphical user interface |
| NumPy | Numerical operations |
| Scikit-learn | Model evaluation and metrics |

### Hardware Components

| Component | Purpose |
|---|---|
| Raspberry Pi 5 | AI inference and system-level processing |
| Arduino UNO | Hardware and motor control |
| A4988 Driver | Stepper motor control |
| NEMA 17 Stepper Motor | Bin positioning |
| Servo Motor | Waste-routing mechanism |
| USB Camera | Waste image capture |
| Limit Switches | Homing and movement safety |
| Four-Compartment Bin | Waste collection and segregation |

## Model Performance

The EfficientNet-B0 model was trained using a combined dataset of **15,110 images** and evaluated on a separate held-out test dataset.

### Overall Evaluation Results

| Metric | Result |
|---|---:|
| Validation Accuracy | **97.88%** |
| Test Accuracy | **97.44%** |
| Correct Test Predictions | 2,208 / 2,266 |
| Macro Precision | 96.84% |
| Macro Recall | 96.79% |
| Macro F1-Score | 96.82% |

### Class-Wise F1-Score

| Waste Category | F1-Score |
|---|---:|
| E_WASTE | 99.30% |
| ORGANIC | 98.84% |
| PLASTIC | 91.58% |
| RECYCLABLE | 97.55% |

### Training Configuration

| Parameter | Value |
|---|---|
| Model Architecture | EfficientNet-B0 |
| Image Size | 224 × 224 |
| Epochs | 20 |
| Batch Size | 32 |
| Optimizer | AdamW |
| Learning Rate | 0.0001 |
| Weight Decay | 0.0001 |
| Loss Function | Weighted Cross-Entropy Loss |

The evaluation results indicate strong classification performance across the four waste categories. Plastic classification has the lowest class-wise F1-score and remains an area for improvement.

## Dataset Information

The combined dataset contains **15,110 images** collected from multiple publicly available sources.

The dataset underwent preprocessing, cleaning, duplicate detection, and organization before being divided into training, validation, and testing sets.

Raw dataset images are not included in this repository.

For dataset sources and licensing information, refer to:

- [`docs/dataset_sources.md`](docs/dataset_sources.md)

Please obtain the original datasets from their respective publishers and follow their licensing and usage conditions.

## Repository Structure

```text
AI-Smart-Waste-Segregation-System/
│
├── dataset/
│   └── .gitkeep
│
├── docs/
│   └── dataset_sources.md
│
├── hardware/
│   └── arduino/
│       └── waste_motion_controller.ino
│
├── models/
│   └── efficientnet_b0_best.pth
│
├── results/
│   ├── confusion_matrix.png
│   ├── error_analysis.csv
│   ├── evaluation_report.txt
│   ├── evaluation_results.json
│   └── training_history.json
│
├── scripts/
│   ├── train.py
│   ├── evaluate.py
│   ├── predict.py
│   ├── camera_predict.py
│   ├── motion_controller_gui.py
│   ├── config.json
│   └── ...
│
├── README.md
└── requirements.txt
```

## Installation and Setup

### 1. Clone the Repository

```bash
git clone https://github.com/ambari2208/AI-Smart-Waste-Segregation-System.git
cd AI-Smart-Waste-Segregation-System
```

### 2. Create a Virtual Environment

```bash
python -m venv .venv
```

### 3. Activate the Environment

**Windows:**
```bash
.venv\Scripts\activate
```

**Linux / Raspberry Pi OS / macOS:**
```bash
source .venv/bin/activate
```

### 4. Install Dependencies

```bash
pip install -r requirements.txt
```

**Note:** PyTorch and other hardware-dependent packages may require platform-specific installation, particularly on Raspberry Pi 5.

### 5. Configure Gemini API

If using the Gemini API integration, configure your API key locally.

Create a `.env` file in the project root and add:

```env
GEMINI_API_KEY=your_api_key_here
```

Keep your API key private. Never commit your `.env` file or expose credentials publicly.

### 6. Dataset Setup

The raw dataset is not distributed with this repository. Obtain the original datasets from their respective publishers and prepare the directory structure required by the training scripts.

## Hardware Integration

The hardware subsystem connects the AI classification output to the physical segregation mechanism.

- **Raspberry Pi 5:** Handles AI inference and system-level operations.
- **Arduino UNO:** Executes hardware control instructions.
- **Servo Motor:** Supports the waste-routing mechanism.
- **NEMA 17 Stepper Motor:** Controls compartment positioning.
- **A4988 Driver:** Drives the stepper motor.
- **Limit Switches:** Support homing and movement protection.

The Arduino control program is available at:

[`hardware/arduino/waste_motion_controller.ino`](hardware/arduino/waste_motion_controller.ino)

## Project Demonstration

Watch the working demonstration of the AI-Powered Smart Waste Segregation System:

[▶ Watch the Project Demonstration on YouTube](https://youtu.be/HUJFUk7StMc)

## Results and Evaluation

The trained EfficientNet-B0 model achieved **97.44% test accuracy** on 2,266 test images.

The project also includes evaluation outputs and training records for further analysis:

- `results/evaluation_report.txt`
- `results/evaluation_results.json`
- `results/confusion_matrix.png`
- `results/error_analysis.csv`
- `results/training_history.json`

## Future Scope

- Expand the dataset with more diverse real-world waste images.
- Improve classification of visually similar waste materials.
- Optimize model inference for edge devices.
- Introduce additional waste categories.
- Improve the mechanical design and reliability of the segregation mechanism.
- Develop remote monitoring and performance analytics.

## Acknowledgements

This project makes use of publicly available datasets and open-source software libraries. Credit and licensing information for dataset sources should be reviewed in the dataset documentation and the respective publishers' terms.

## License

License and third-party attribution terms are to be finalized. Until a project license is added, please refer to the original licenses of the datasets and software libraries before reusing their materials.

---

**AI-Powered Smart Waste Segregation System**

Developed as an academic engineering project.
