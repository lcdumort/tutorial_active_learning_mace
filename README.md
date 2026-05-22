# MACE Active Learning Tutorial: Environment Setup Guide

This repository contains the hands-on materials for the machine learning potentials and active learning tutorial using MACE. 

To ensure fast, reliable, and isolated dependency management without the overhead of a full Anaconda installation, this project uses **Micromamba**. Micromamba is a lightweight, single-binary version of the `mamba` (and `conda`) package manager written in C++. It does not require a base Python installation and installs packages in parallel, making it significantly faster than traditional Conda.

---

## 1. Installation of Micromamba

Choose the installation command matching your operating system. Run this in your terminal:

### Linux / macOS
```bash
"${SHELL}" <(curl -L micro.mamba.pm/install.sh)
```

## 2. Creating the Environment
I have provided an environment.yml configuration file that contains all necessary dependencies, including MACE, PyTorch (with GPU acceleration support where applicable), ASE (Atomic Simulation Environment), and Jupyter for running the tutorial notebooks.

### Step 1. Clone this repository
```bash
git clone <your-repository-url>
cd <repository-folder-name>
```

### Step 2. Create the Environment from the Configuration
Run the following command to automatically download and build the environment (named `mace-al`):
```bash
micromamba env create -f environment.yml
```
do note that the current environment.yml file will only install cpu versions, as that takes less memory.
You can easily change this in the file by removing the cpuonly tag and replacing it with a cuda/cudnn version.

### Step 3. Activate the Environment
Once the installation finishes, activate the environment using:
```bash
micromamba activate mace-al
```

## 3. Verifying the installation
To verify that everything was installed correctly and that your Python environment can access your hardware accelerators (like CUDA GPUs), run the following verification commands. If you're working locally, you will probably not have a fancy computer and GPU acceleration will not be available. When doing production stuff, make sure you work on a system with GPU!
```bash
# Check that the correct python environment is active
which python

# Verify PyTorch and CUDA/MPS accessibility
python -c "import torch; print('PyTorch Version:', torch.__version__); print('CUDA Available:', torch.cuda.is_available())"

# Verify MACE and ASE can be imported smoothly
python -c "import mace; import ase; print('MACE and ASE imported successfully!')"
```

