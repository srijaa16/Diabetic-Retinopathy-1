# RetinaX — Diabetic Retinopathy Research Prototype

RetinaX is a modular research prototype for five-class diabetic retinopathy classification, model explainability, federated learning, and lesion segmentation.

## Features

- Five-class diabetic retinopathy classification
- Baseline CNN, CNN-LSTM, and Mixture-of-Experts (MoE) models
- Explainability using Grad-CAM
- Experimental federated learning support
- Attention U-Net-based lesion segmentation
- Streamlit web interface for image uploads and model inference

## Dataset Requirements

The classification pipeline expects an `ImageFolder` dataset with the following class folders:

- `Mild`
- `Moderate`
- `No_DR`
- `Proliferate_DR`
- `Severe`

The classification dataset does not contain pixel-level lesion masks. A separate paired image-and-mask dataset is required to train the segmentation model.

Use a suitable retinal dataset for meaningful model evaluation. Demo images are intended only for software testing.

## Setup

### 1. Clone the repository

```bash
git clone https://github.com/srijaa16/Diabetic-Retinopathy-1.git
cd Diabetic-Retinopathy-1
```

### 2. Create a virtual environment

**Windows PowerShell**

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**Linux / Google Colab**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
pip install -e .
```

## Inspect the Dataset

Replace the path below with the location of your dataset.

```bash
python -m retinax.cli inspect-data --data-root "path/to/gaussian_filtered_images"
```

## Train a Classification Model

Example using the baseline model:

```bash
python -m retinax.cli train --data-root "path/to/gaussian_filtered_images" --model baseline --epochs 15 --batch-size 32 --checkpoint checkpoints/retinax_baseline.pt
```

Available model options include `baseline`, `cnn_lstm`, and `moe`.

Training generates a checkpoint and evaluation metrics according to the configured training pipeline.

## Run the Web Interface

Install Streamlit if it is not already installed:

```bash
pip install streamlit
streamlit run app.py
```

Open the local URL displayed in the terminal. Upload a retinal image and provide a trained checkpoint if required by the interface.

Without a trained checkpoint, the interface may run only an untrained preview. Its predictions should not be interpreted as meaningful diagnostic results.

## Trained Model Checkpoints

Trained `.pt` model files are excluded from this repository because of their storage requirements.

To run inference with trained models, obtain the required checkpoint files from the project maintainer and place them in the `checkpoints/` directory. The required files depend on the selected model and task.

## Project Structure

```text
retinax/
├── app.py
├── configs/
├── notebooks/
├── src/retinax/
├── tests/
├── requirements.txt
├── pyproject.toml
├── README.md
└── SETUP.md
```

## Limitations

- Model performance depends on dataset quality, training configuration, and evaluation methodology.
- Segmentation requires a separate dataset containing appropriate lesion masks.
- CPU execution is suitable for basic testing; GPU acceleration may help with training.
- Demo images are not suitable for validating clinical performance.

## Disclaimer

RetinaX is a research prototype intended for educational and experimental use. It is not a medical device and must not be used as a substitute for professional medical advice or diagnosis.

For detailed setup instructions, see [SETUP.md](https://github.com/srijaa16/Diabetic-Retinopathy-1/blob/main/SETUP.md).
