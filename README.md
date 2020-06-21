# EverybodyDanceNow reproduced in pytorch

Written by Aman Arya under supervision of Parthiban Srinivasan .<br>
<br>
We train and evaluate on windows 10 in syder 4.1
## About:
Project Title : Any Body Can Dance

Youtube link :  https://www.youtube.com/watch?v=LWEm9bDlVmY&pbjreload=101 
 
Faculty supervisor: Parthiban Srinivasan ( Adjunct Faculty (Artificial Intelligence) at IISER, Bhopal and CEO, Parthys Reverse Informatics )

https://in.linkedin.com/in/parthiban-srinivasan-183608b

Github code: https://github.com/aman-arya/EverybodyDanceNow_reproduce_pytorch

Research paper : https://arxiv.org/pdf/1808.07371.pdf

Presentation : https://drive.google.com/file/d/1suHPXofvexaztPkBwDECmwHiTjiOQhq5/view?usp=sharing  

## Reference:

https://arxiv.org/pdf/1808.07371.pdf

https://github.com/CUHKSZ-TQL/EverybodyDanceNow_reproduce_pytorch

https://carolineec.github.io/everybody_dance_now/

https://getsway.app/

https://people.eecs.berkeley.edu/~efros/

## Pre-trained models and source video
* Download vgg19-dcbb9e9d.pth.crdownload [here](https://drive.google.com/file/d/1JG-pLXkPmyx3o4L33rG5WMJKMoOjlXhl/view?usp=sharing) and put it in `./src/pix2pixHD/models/`  <br>

* Download pose_model.pth [here](https://drive.google.com/file/d/1DDBQsoZ94N4NRKxZbwyEXt7Tz8KqgS_w/view?usp=sharing) and put it in `./src/PoseEstimation/network/weight/`   <br>

* Source video can be download from [here](https://drive.google.com/file/d/1drRBJypNGqOZV9WFutEzDYXkEelUjZXh/view?usp=sharing)

* Download pre-trained vgg_16 for face enhancement [here](https://drive.google.com/file/d/180WgIzh0aV1Aayl_b1X7mIhVhDUcW3b1/view?usp=sharing) and put in `./face_enhancer/`

## Full process
#### Pose2vid network

![](/result/fig1.png)
#### Make source pictures
* Put source video mv.mp4 in `./data/source/`  
* Run `make_source.py`, the label images and coordinate of head will save in `./data/source/test_label_ori/` and `./data/source/pose_souce.npy` (will use in step6). 
* If you want to capture video by camera, you can directly run `./src/utils/save_img.py`
#### Make target pictures
* Put target video mv.mp4 in `./data/target/` 
* Run `make_target.py`, `pose.npy` will save in `./data/target/`, which contain the coordinate of faces (will use in step6).
![](/result/fig3.png)
#### Train and use pose2vid network
* Run `train_pose2vid.py` and check loss and full training process in `./checkpoints/`

* If you break the traning and want to continue last training, set `load_pretrain = './checkpoints/target/` in `./src/config/train_opt.py`
* Run `normalization.py` rescale the label images, you can use two sample images from `./data/target/train/train_label/` and `./data/source/test_label_ori/` to complete normalization between two skeleton size
* Run `transfer.py` and get results in `./result`
#### Face enhancement network

![](/result/fig2.png)
#### Train and use face enhancement network
* Run `./face_enhancer/prepare.py` and check the results in `./data/face/test_sync` and `./data/face/test_real`.
* Run `./face_enhancer/main.py` train face enhancer and run`./face_enhancer/enhance.py` to gain results <br>
This is comparision in original (left), generated image before face enhancement (median) and after enhancement (right). FaceGAN can learn the residual error between the real picture and the generated picture faces.

#### Performance of face enhancement 
![](/result/37500_enhanced_full.png)
![](/result/37500_enhanced_head.png)

#### Gain results
* Run `make_gif.py` and make result pictures to gif picture

![Result](/result/output.gif)

## TODO

- Pose estimation
    - [x] Pose
    - [x] Face
    - [ ] Hand
- [x] pix2pixHD
- [x] FaceGAN
- [ ] Temporal smoothing

## Environments
windows 10 <br>
Python 3.7 <br>
Pytorch 1.0  <br>
OpenCV 3.4.2.17  <br>


