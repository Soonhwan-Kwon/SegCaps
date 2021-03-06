# Capsules for Object Segmentation (SegCaps)
### by [Rodney LaLonde](https://rodneylalonde.wixsite.com/personal) and [Ulas Bagci](http://www.cs.ucf.edu/~bagci/)
### Modified by [Cheng-Lin Li](https://cheng-lin-li.github.io/about/)
### Objectives: Improve this model for Object Segmentation on different dataset (COCO) with multi-class classification tasks.

## This repo is the clone implementation of SegCaps from official site with modification.

The original paper for SegCaps can be found at https://arxiv.org/abs/1804.04241.
The original source code can be found at https://github.com/lalonderodney/SegCaps
A project page for this work can be found at https://rodneylalonde.wixsite.com/personal/research-blog/capsules-for-object-segmentation.


## TODO List:
  1. Execute programs on LUNA 16 dataset. Done. Jun 11
    1-1. Porting program from python 2.7 to 3.6 (Jun 11)
    1-2. Execute manipulation function. (Jun 11)
    1-2. Execute test function on one image without pre-trained weight(Jun 11)
    1-3. Execute train function on 3 images. (Jun 12)
    1-4. Execute test function on trained model (Jun 12)
    1-5. Display original image and result mask image. (Jun 12)
    1-6. Identify input image mask format. 
  2. Find right dataset for person/cat/dog segmentation. Candidate dataset is MS COCO. Done. 6/12 COCO 2017
    2-1. Identify COCO stuff 2017 as target dataset.
    2-2. Download annotation files for COCO 2017.
  3. Test existing program on color images.
    3-1. Generate single class mask on COCO masked image data.(Jun 13)
    3-2. Convert the image mask format to background=0, objects=1. 
    3-3. Feed the color images with single class mask to model.
  4. Modify program for color images.
  5. Modify existing program on multi-classification tasks.
  6. Integrate model with webcam.
  7. Pipeline up:
    7-1. Modify code to support experiments.
      7-1-1. Models persistent by version with configuration and dataset.
      7-1-2. Notebook folder build up to store experiment results.
    7-2. Test pipeline



## Getting Started Guide

### Install Required Packages on Ubuntu / Windows
This repo of code is written for Keras using the TensorFlow backend. 
You may need to adjust requirements.txt file according to your environment (CPU only or GPU for tensorflow installation). 

Please install all required packages before using this code.


```bash
pip install -r requirements.txt
```
### You may need to install additional library in Ubuntu version 17 or above version.
Following steps will resolve below issue.
```text
ImportError: libjasper.so.1: cannot open shared object file: No such file or directory
```
```bash
sudo apt-get update
sudo apt-get install libjasper-dev
```

### Install package on Raspberry Pi 3

#### Download tensorflow pre-compile version for ARM v7.
Tensorflow for ARM - Github Repo:
https://github.com/lhelontra/tensorflow-on-arm/releases

installation instruction.

https://medium.com/@abhizcc/installing-latest-tensor-flow-and-keras-on-raspberry-pi-aac7dbf95f2


#### OpenCV installation on Raspberry Pi 3
https://www.alatortsev.com/2018/04/27/installing-opencv-on-raspberry-pi-3-b/



### Dataset

Test the result on original LUNA 16 dataset.
  1. Go to [LUng Nodule Analysis 2016 Grand-Challenges website](https://luna16.grand-challenge.org/)
  2. Get an account by registration.
  3. Join the 'LUNA 16' challenge by click 'All Challenges' on the tab of top. Click the 'Join' and goto 'Download' section to get your data.


### Dataset Structure

Inside the data root folder (*i.e.* where you have your data stored) you should have two folders: one called *imgs* and one called *masks*. All models, results, etc. are saved to this same root directory.

You also need to create a *split_lists* folder to keep training and testing index files.
*train_split_0.csv* for training set.
*test_split_0.csv* for test set.

### Main File

From the main file (main.py) you can train, test, and manipulate the segmentation capsules of various networks. Simply set the ```--train```, ```--test```, or ```--manip flags``` to 0 or 1 to turn these off or on respectively. The argument ```--data_root_dir``` is the only required argument and should be set to the directory containing your *imgs* and *masks* folders. There are many more arguments that can be set and these are all explained in the main.py file. 

### Program Descriptions
  1. main.py: The entry point of this project.
  2. load_3D_data.py: The data loading model.
  

### Citation

This project based on the official codebase of Capsules for Object Segmentation:
```
@article{lalonde2018capsules,
  title={Capsules for Object Segmentation},
  author={LaLonde, Rodney and Bagci, Ulas},
  journal={arXiv preprint arXiv:1804.04241},
  year={2018}
}
```

### Questions or Comments
For this modification version, please email me at clark.cl.li@gmail.com

For the original implementation, please direct any questions or comments to the author. You can either comment on the [project page](https://rodneylalonde.wixsite.com/personal/research-blog/capsules-for-object-segmentation), or email author directly at lalonde@knights.ucf.edu.















## Original README.md description:
<img src="imgs/qualitative1.png" width="900px"/>

## Condensed Abstract
Convolutional neural networks (CNNs) have shown remarkable results over the last several years for a wide range of computer vision tasks. A new architecture recently introduced by [Sabour et al., referred to as a capsule networks with dynamic routing](https://arxiv.org/abs/1710.09829), has shown great initial results for digit recognition and small image classification. Our work expands the use of capsule networks to the task of object segmentation for the first time in the literature. We extend the idea of convolutional capsules with *locally-connected routing* and propose the concept of *deconvolutional capsules*. Further, we extend the masked reconstruction to reconstruct the positive input class. The proposed convolutional-deconvolutional capsule network, called **SegCaps**, shows strong results for the task of object segmentation with substantial decrease in parameter space. As an example application, we applied the proposed SegCaps to segment pathological lungs from low dose CT scans and compared its accuracy and efficiency with other U-Net-based architectures. SegCaps is able to handle large image sizes (512 x 512) as opposed to baseline capsules (typically less than 32 x 32). The proposed SegCaps reduced the number of parameters of U-Net architecture by **95.4%** while still providing a better segmentation accuracy.

## Baseline Capsule Network for Object Segmentation

<img src="imgs/baselinecaps.png" width="900px"/>

## SegCaps (R3) Network Overview

<img src="imgs/segcaps.png" width="900px"/>

## Quantative Results on the LUNA16 Dataset

| Method           | Parameters | Split-0 (%) | Split-1 (%) | Split-2 (%) | Split-3 (%) | Average (%) |
|:---------------- |:----------:|:-----------:|:-----------:|:-----------:|:-----------:|:-----------:|
| U-Net            | 31.0 M     | 98.353      | 98.432      | 98.476      | **98.510**  | 98.449      |
| Tiramisu         | 2.3 M      | 98.394      | 98.358      | **98.543**  | 98.339      | 98.410      |
| Baseline Caps    | 1.7 M      | 82.287      | 79.939      | 95.121      | 83.608      | 83.424      |
| SegCaps (R1)     | **1.4 M**  | 98.471      | 98.444      | 98.401      | 98.362      | 98.419      |
| **SegCaps (R3)** | **1.4 M**  | **98.499**  | **98.523**  | 98.455      | 98.474      | **98.479**  |

## Results of Manipulating the Segmentation Capsule Vectors

<img src="imgs/manip_cropped.png" width="900px"/>

