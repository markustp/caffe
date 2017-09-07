# Robot detector using SSD: Single Shot MultiBox Detector

By Markus Pike - markustpike@gmail.com

### Introduction

This is a copy of the [SSD](https://github.com/weiliu89/caffe/tree/ssd) framework modified for Ascend NTNU to perform detection of ground robots. The SSD paper can be found [here](http://arxiv.org/abs/1512.02325). The SSD framework is an extention of the [Caffe](https://github.com/BVLC/caffe) framework. 

### Citing SSD

For further use please cite SSD:

    @inproceedings{liu2016ssd,
      title = {{SSD}: Single Shot MultiBox Detector},
      author = {Liu, Wei and Anguelov, Dragomir and Erhan, Dumitru and Szegedy, Christian and Reed, Scott and Fu, Cheng-Yang and Berg, Alexander C.},
      booktitle = {ECCV},
      year = {2016}
    }

### Contents
1. [Required software](#required-software)
2. [Installation](#installation)
3. [Models](#models)
4. [Run the robot detection](#run-the-robot-detection)
5. [Retrain the model](#retrain-the-model)



### Required software

This installation requires a Linux OS and [Cuda Toolkit](https://developer.nvidia.com/cuda-downloads) to be installed. 


### Installation
1. Get the code. We will call the directory that you cloned Caffe into `$CAFFE_ROOT`. 
  ```Shell
  git clone https://github.com/AscendNTNU/SSD_Robot_Detection
  cd caffe
  ```
You will now be in `$CAFFE_ROOT`. 

2. Build the code. This should install all dependencies, make caffe and run some tests. 
  ```Shell
  sudo ./InstallSSD
  ```

3. Make sure to include $CAFFE_ROOT/python to your PYTHONPATH. This can be done by edeting the line `export PYTHONPATH=$CAFFE_ROOT/python:$PYTHONPATH` to make sure $CAFFE_ROOT is set correctly and add it to your ~/.profile file.


### Models
Unless you want to train the network yourself you have to download the already trained models provided below. Each model folder must be placed in `$CAFFE_ROOT/models/VGGNet/Ascend/`. The names of the models indicate the image input size to the network. Smaller networks run faster but create less accurate detections.  

1. Colored models - networks that distinguish between red, green and tower robots:
* [SSD_Color_300x300](https://drive.google.com/open?id=0B2yoUIxrG4eRUTlLdXJ4N1FIN1U)
* [SSD_Color_420x420](https://drive.google.com/open?id=0B2yoUIxrG4eRUGZaUWhyVURfVTg)
* [SSD_Colored_512x512](https://drive.google.com/open?id=0B2yoUIxrG4eRNkNzSUNNY0xnVkE)

Notice that the colored version of the 512x512 (SSD512) network use the prefix `SSD_Colored_` while the SSD420 and SSD300 are called `SSD_Color_`

2. Earlier versions of the networks did not distinguish between colors and can be found here:
* [SSD_300x300](https://drive.google.com/open?id=0B2yoUIxrG4eRNEhQaFVfU2lhTTg)
* [SSD_512x512](https://drive.google.com/open?id=0B2yoUIxrG4eRR0E0RVRINktnYXM)


### Run the robot detection
The networks can be run on videos or live video from a webcam. 

1. Webcam:
  Depending on the models you are using you have to modify a few lines of code in `AscendCode/ascend_ssd_pascal_webcam.py` to make sure it runs. The `webcam_id` has a default value of 0, but if more than one cammera is connected to the computer you might have to change this. The second camera has webcam_id=1, third camera har webcam_id=2 and so on. Secondly you have to set the `resize_width` and `resize_height` equal to the input image size for the model. SSD300 has both of them set to 300, SSD420 is set to 420 and SSD512 used 512. Thirdly, make sure the `job_name` variable is set correctly. For SSD300 and SSD420 with colors it is `SSD_Color_{}`, SSD512 with colors use `SSD_Colored_{}` while the uncolored ones both use `SSD_{}`. 
  ```Shell
  python AscendCode/ascend_ssd_pascal_webcam.py
  ```

2. Video:
  Depending on the models you are using you have to modify a few lines of code in `AscendCode/ascend_ssd_pascal_video.py` to make sure it runs. You have to set the `resize_width` and `resize_height` equal to the input image size for the model. SSD300 has both of them set to 300, SSD420 is set to 420 and SSD512 used 512. Secondly, make sure the `job_name` variable is set correctly. For SSD300 and SSD420 with colors it is `SSD_Color_{}`, SSD512 with colors use `SSD_Colored_{}` while the uncolored ones both use `SSD_{}`.  
  

All the original SSD code for running and training networks are located in `$CAFFE_ROOT/examples/ssd/` and can be modified to enable speed tests and single image processing. 



### Retrain the model
If you want to retrain the models you should follow the instructions provided in the original [SSD repo](https://github.com/weiliu89/caffe/tree/ssd).

The datasets used to create the existing models will be available soon. 


