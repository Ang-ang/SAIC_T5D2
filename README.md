# SAIC_T5D2
use pointpillars as baseline, use SAIC dataset to do 3D detection

mainly forked from https://github.com/nutonomy/second.pytorch

### Install

#### 1. Clone code

```bash
git clone https://github.com/Ang-ang/SAIC_T5D2.git
```
#### 2. Install Python packages

It is recommend to use the Anaconda package manager.

First, use Anaconda to configure as many packages as possible.
```bash
conda create -n SAIC python=3.7 anaconda
source activate SAIC



#### 3. Setup cuda for numba

You need to add following environment variables for numba to ~/.bashrc:

```bash
export NUMBAPRO_CUDA_DRIVER=/usr/lib/x86_64-linux-gnu/libcuda.so
export NUMBAPRO_NVVM=/usr/local/cuda/nvvm/lib64/libnvvm.so
export NUMBAPRO_LIBDEVICE=/usr/local/cuda/nvvm/libdevice
```

#### 4. PYTHONPATH

Add second.pytorch/ to your PYTHONPATH.

### Prepare dataset

#### 1. Dataset preparation

Download SAIC dataset and create some directories first:

```plain
└── SAIC_DATASET_ROOT
       ├── training    <-- 6000 train data
       |   ├── calibration
       |   ├── label
       |   ├── velodyne
       └── testing     <-- 1200 test data
           ├── velodyne
```

Note: this repo use ```SAIC_DATASET_ROOT=/data/SAIC_dataset/```.
