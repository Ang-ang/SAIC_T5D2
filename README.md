# SAIC_T5D2
use pointpillars(https://arxiv.org/pdf/1812.05784.pdf) as baseline, use SAIC dataset to do 3D detection

mainly forked from: https://github.com/nutonomy/second.pytorch

Pre_trained model download:

[Model_car](https://drive.google.com/file/d/1bDuc4clHaIBmme8iq4oR5uaSqvjS6sBo/view?usp=sharing)

[Model_pedestrian](https://drive.google.com/file/d/1grf_VlbgwvflnpfqYuM1wXF_80q8FAUq/view?usp=sharing)

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
```
#### 3. Setup cuda for numba

Add following environment variables for numba to ~/.bashrc:

```bash
export NUMBAPRO_CUDA_DRIVER=/usr/lib/x86_64-linux-gnu/libcuda.so
export NUMBAPRO_NVVM=/usr/local/cuda/nvvm/lib64/libnvvm.so
export NUMBAPRO_LIBDEVICE=/usr/local/cuda/nvvm/libdevice
```
#### 4. PYTHONPATH

Add SAIC_T5D2/ to PYTHONPATH.

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

#### 2. Create infos:

```bash
python create_data.py create_kitti_info_file --data_path=SAIC_DATASET_ROOT
```
#### 3. Create groundtruth-database infos:

```bash
python create_data.py create_groundtruth_database --data_path=SAIC_DATASET_ROOT
```
#### 4. Modify config file

The config file needs to be edited to point to the above datasets:

```bash
train_input_reader: {
  ...
  database_sampler {
    database_info_path: "/path/to/SAIC_dataset_dbinfos_train.pkl"
    ...
  }
  kitti_info_path: "/path/to/SAIC_dataset_infos_train.pkl"
  kitti_root_path: "SAIC_DATASET_ROOT"
}
...
eval_input_reader: {
  ...
  kitti_info_path: "/path/to/SAIC_dataset_infos_val.pkl"
  kitti_root_path: "SAIC_DATASET_ROOT"
}
```
### Train

```bash
cd ~/second.pytorch/second/pytorch
python train.py train --config_path=(path to config file) --model_dir=(path to model dir) --ckpt_path=(path to model)
```
### Evaluate

```bash
cd ~/second.pytorch/second/pytorch
python train.py evaluate --config_path=(path to config file) --model_dir=(path to model dir) --ckpt_path=(path to model)
```
