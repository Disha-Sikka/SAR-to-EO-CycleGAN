# SAR-to-EO-CycleGAN

This project implements a CycleGAN-based approach to translate SAR (Synthetic Aperture Radar) satellite imagery (Sentinel-1) into corresponding EO (Electro-Optical / RGB, i.e., Sentinel-2) imagery. This has practical use in enhancing SAR interpretability and filling EO data gaps due to cloud cover.

## Directory Structure

```

├── my\_sen12ms\_data\_subset/
│   ├── winter\_s1/         # Input SAR images (VV & VH)
│   └── winter\_s2/         # Target EO images (RGB)

````

##  Requirements

- Python 3.x
- PyTorch
- torchvision
- numpy
- matplotlib
- PIL
- Rasterio


## Getting Started

### 1. Prepare Data

* Place your Sentinel-1 SAR images (VV & VH as channels) in `winter_s1/`.
* Place corresponding Sentinel-2 EO RGB images in `winter_s2/`.
* Ensure the filenames match between the two directories.

### 2. Configure Parameters

Set data paths and model configurations in `config.py`:

```python
data_root_dir = './my_sen12ms_data_subset'
SAR_DIR = 'winter_s1'
EO_DIR = 'winter_s2'
```

Other parameters:

* `INPUT_NC = 3` (for SAR: VV, VH)
* `OUTPUT_NC = 3` (for RGB)

### 3. Train the Model

```bash
python train.py
```

Progress will be logged, and checkpoints/results will be saved in `./results/`.

### 4. Test the Model

```bash
python test.py
```

The translated EO images will be saved in the results directory for visualization.

## 📈 Model Architecture

* Generator: ResNet-based generator from CycleGAN paper
* Discriminator: PatchGAN
* Loss Functions:

  * Adversarial Loss
  * Cycle Consistency Loss
  * Identity Loss (optional)
