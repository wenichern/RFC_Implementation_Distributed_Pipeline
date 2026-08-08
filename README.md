# Local Setup Guide - Jupyter Notebook Testing

This guide will help you set up a virtual environment and install Jupyter to test the Real-Time ML Inference Platform Pipeline notebook locally.

## Prerequisites

- Python 3.9 or higher installed on your system
- pip (Python package installer)
- Terminal/Command Prompt access

## Step 1: Create a Virtual Environment

### On macOS/Linux:

```bash
# Navigate to your project directory
cd /path/to/your/project

# Create a virtual environment named 'venv'
python3 -m venv venv

# Activate the virtual environment
source venv/bin/activate
```

### On Windows:

```bash
# Navigate to your project directory
cd C:\path\to\your\project

# Create a virtual environment named 'venv'
python -m venv venv

# Activate the virtual environment
venv\Scripts\activate
```

**Note:** When activated, you should see `(venv)` at the beginning of your terminal prompt.

## Step 2: Upgrade pip

```bash
pip install --upgrade pip
```

## Step 3: Install Jupyter Notebook

```bash
# Install Jupyter Notebook
pip install jupyter

# Verify installation
jupyter --version
```

## Step 4: Install Required Dependencies

Install all the packages needed for the ML pipeline notebook:

```bash
# Core ML and Data Science packages
pip install torch torchvision torchaudio
pip install numpy pandas matplotlib seaborn

# Distributed computing
pip install ray[tune]

# AWS services (optional, for cloud integration)
pip install boto3 sagemaker

# Additional utilities
pip install s3fs fsspec pyarrow tqdm
```

**Alternative:** Install all at once:
```bash
pip install jupyter torch torchvision torchaudio numpy pandas matplotlib seaborn \
    ray[tune] boto3 sagemaker s3fs fsspec pyarrow tqdm
```

## Step 5: Launch Jupyter Notebook

```bash
# Start Jupyter Notebook server
jupyter notebook
```

This will:
- Start the Jupyter server
- Open your default web browser
- Display the Jupyter file browser at `http://localhost:8888`

## Step 6: Open and Run Your Notebook

1. Navigate to the notebook file: `Real_Time_ML_Inference_Platform_Pipeline.ipynb`
2. Click to open it
3. Run cells individually by pressing `Shift + Enter`
4. Or run all cells: `Cell` → `Run All`

## Step 7: Deactivate Virtual Environment (When Done)

```bash
deactivate
```

---

## Troubleshooting

### Issue: "python3: command not found"
- **Solution:** Try `python` instead of `python3`, or install Python from [python.org](https://www.python.org/downloads/)

### Issue: CUDA/GPU errors
- **Solution:** The notebook will automatically fall back to CPU if CUDA is not available. For GPU support, install CUDA toolkit from [NVIDIA](https://developer.nvidia.com/cuda-downloads)

### Issue: Ray initialization fails
- **Solution:** Ray may have issues on some systems. You can comment out Ray-related cells and still run the rest of the notebook.

### Issue: Memory errors
- **Solution:** Reduce batch size or sample size in the configuration:
  ```python
  CONFIG['BATCH_SIZE'] = 16  # Reduce from 32
  ```

---

## Quick Start Script

Save this as `setup.sh` (macOS/Linux) or `setup.bat` (Windows):

### macOS/Linux (`setup.sh`):
```bash
#!/bin/bash
python3 -m venv venv
source venv/bin/activate
pip install --upgrade pip
pip install jupyter torch torchvision torchaudio numpy pandas matplotlib seaborn \
    ray[tune] boto3 sagemaker s3fs fsspec pyarrow tqdm
echo "Setup complete! Run 'jupyter notebook' to start."
```

Make executable and run:
```bash
chmod +x setup.sh
./setup.sh
```

### Windows (`setup.bat`):
```batch
@echo off
python -m venv venv
call venv\Scripts\activate
pip install --upgrade pip
pip install jupyter torch torchvision torchaudio numpy pandas matplotlib seaborn ray[tune] boto3 sagemaker s3fs fsspec pyarrow tqdm
echo Setup complete! Run 'jupyter notebook' to start.
```

Run:
```batch
setup.bat
```

---

## Alternative: Using Conda

If you prefer Conda:

```bash
# Create conda environment
conda create -n ml-pipeline python=3.10

# Activate environment
conda activate ml-pipeline

# Install Jupyter
conda install jupyter

# Install PyTorch with CUDA (for GPU support)
conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia

# Install other packages
pip install ray[tune] boto3 sagemaker pandas numpy matplotlib seaborn s3fs fsspec pyarrow tqdm

# Launch Jupyter
jupyter notebook
```

---

## Testing Without Full Installation

If you just want to test the notebook structure without running heavy ML operations:

```bash
# Minimal installation
pip install jupyter numpy pandas matplotlib

# Comment out or skip cells that require:
# - torch (PyTorch)
# - ray (Ray)
# - boto3 (AWS)
```

---

## Additional Resources

- **Jupyter Documentation:** https://jupyter.org/documentation
- **PyTorch Installation Guide:** https://pytorch.org/get-started/locally/
- **Ray Documentation:** https://docs.ray.io/en/latest/ray-overview/installation.html
- **Virtual Environments Guide:** https://docs.python.org/3/tutorial/venv.html

---

**Happy Testing! 🚀**
