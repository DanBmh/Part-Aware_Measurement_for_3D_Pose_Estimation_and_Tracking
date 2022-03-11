# Part-aware Measurement for Robust Multi-View Multi-Human 3D Pose Estimation and Tracking

> [Part-Aware Measurement for Robust Multi-View Multi-Human 3D Pose Estimation and Tracking](https://arxiv.org/abs/2106.11589)  
> Hau Chu, Jia-Hong Lee, Yao-Chih Lee, Ching-Hsien Hsu, Jia-Da Li, Chu-Song Chen  
> 2021 CVPR B-AMFG Workshop

[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/part-aware-measurement-for-robust-multi-view-1/3d-multi-person-pose-estimation-on-campus)](https://paperswithcode.com/sota/3d-multi-person-pose-estimation-on-campus?p=part-aware-measurement-for-robust-multi-view-1)
[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/part-aware-measurement-for-robust-multi-view-1/3d-multi-person-pose-estimation-on-shelf)](https://paperswithcode.com/sota/3d-multi-person-pose-estimation-on-shelf?p=part-aware-measurement-for-robust-multi-view-1)

The code is released for academic research use only. For commercial use, please contact Prof. Chu-Song Chen(chusong@csie.ntu.edu.tw).

## Installation

 - Python 3.6+

 - Cuda 9.0

 - Cudnn 7

 - gcc 5 & g++ 5 (for Ubuntu 18.04)
```
$ sudo apt install gcc-5 g++-5
$ sudo ln -s /usr/bin/gcc-6 /usr/local/bin/gcc
$ sudo ln -s /usr/bin/g++-6 /usr/local/bin/g++
```

 - Conda Env
```
$ conda create -n venv python=3.6
$ conda activate venv
$ conda install pytorch==1.1.0 torchvision==0.3.0 cudatoolkit=9.0 -c pytorch
$ pip install tensorflow_gpu==1.9.0
$ pip install -r requirements.txt
```
 
 - Git
```
$ sudo apt install git
```

# Data preparation
Download datasets:
1. Campus (http://campar.in.tum.de/Chair/MultiHumanPose)
2. Shelf (http://campar.in.tum.de/Chair/MultiHumanPose)
3. CMU Panoptic (https://github.com/CMU-Perceptual-Computing-Lab/panoptic-toolbox)

Datasets' camera_parameter.pickle [(download)](https://drive.google.com/drive/folders/1JUB4zmOJBZ78aTFCCeK2dn-HWR7dTFvB?usp=sharing)

The directory tree should look like below:
```
${ROOT}
    |-- CatchImage
        |-- CampusSeq1
        |   |-- Camera0
        |   |-- Camera1
        |   |-- Camera2
        |   |-- camera_parameter.pickle
        |   |-- actorsGT.mat
        |-- Shelf
        |   |-- Camera0
        |   |-- ...
        |   |-- Camera4
        |   |-- camera_parameter.pickle
        |   |-- actorsGT.mat
        |-- Panoptic
        |   |-- 160906_pizza1
            |   |-- 00_03 # hdImgs folder of 03 camera
            |   |-- 00_06 # hdImgs folder of 06 camera
            |   |-- ...
            |   |-- camera_parameter.pickle
            |   |-- hdPose_stage1_coco19
            |-- ...
    |-- src
```

## Backend Models
Backend models, which is not our works, are released codes from others. We only did some small modifications to fit the format of our input/output.
Put models in {ROOT}/src/backend
1. YOLOv3
    - origin: https://github.com/ZQPei/deep_sort_pytorch
    - [modification](https://drive.google.com/drive/u/1/folders/1WQhNrY7k69maUFnjgLLeSbIKpa2Cbg1p) 
2. HRNet
    - origin: https://github.com/stefanopini/simple-HRNet
    - [modification](https://drive.google.com/drive/u/1/folders/1ZpdwEbu5AAKTyCGanNRUMimdTgCraDrv) 

## Run Codes
### Demo
```bash
$cd src
python -W ignore testmodel.py --dataset CampusSeq1 # For Campus
python -W ignore testmodel.py --dataset Shelf # For Shelf
python -W ignore testmodel.py --dataset Panoptic # For Panoptic (sub-dataset can be modified in config)
```
### Evaluation
```bash
$cd src
python -W ignore evalmodel.py --dataset CampusSeq1 
python -W ignore evalmodel.py --dataset Shelf
```
## Campus PCP Score
| Bone Group | Actor 0 | Actor 1 | Actor 2 | Average |
|    ----    |   ---   |   ---   |   ---   |   ---   |
|    Head    |  100.00 |  100.00 |  100.00 |  100.00 |
|   Torso    |  100.00 |  100.00 |  100.00 |  100.00 |
| Upper arms |  98.98  |  100.00 |  100.00 |  99.66  |
| Lower arms |  92.86  |  68.78  |  91.30  |  84.31  |
| Upper legs |  100.00 |  100.00 |  100.00 |  100.00 |
| Lower legs |  100.00 |  100.00 |  100.00 |  100.00 |
|   Total    |  98.37  |  93.76  |  98.26  |  96.79  |

## Shelf PCP Score
| Bone Group | Actor 0 | Actor 1 | Actor 2 | Average |
|    ----    |   ---   |   ---   |   ---   |   ---   |
|    Head    |  94.98  |  100.00 |  91.30  |  95.43  |
|   Torso    |  100.00 |  100.00 |  100.00 |  100.00 |
| Upper arms |  100.00 |  100.00 |  96.27  |  98.76  |
| Lower arms |  98.21  |  77.03  |  96.27  |  90.50  |
| Upper legs |  100.00 |  100.00 |  100.00 |  100.00 |
| Lower legs |  100.00 |  100.00 |  100.00 |  100.00 |
|   Total    |  99.14  |  95.41  |  97.64  |  97.39  |

## Citation
```bash
@InProceedings{Chu_2021_CVPR,
    author    = {Chu, Hau and Lee, Jia-Hong and Lee, Yao-Chih and Hsu, Ching-Hsien and Li, Jia-Da and Chen, Chu-Song},
    title     = {Part-Aware Measurement for Robust Multi-View Multi-Human 3D Pose Estimation and Tracking},
    booktitle = {Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR) Workshops},
    month     = {June},
    year      = {2021},
    pages     = {1472-1481}
}
```
