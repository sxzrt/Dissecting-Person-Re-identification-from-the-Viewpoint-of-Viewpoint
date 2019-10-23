## Synthesising images based on the PersonX system


The PersonX dataset is generated by the synthetic data engine PersonX that can synthesise images under controllable cameras and environment. For researching viewpoint, six backgrounds are used in this version (as shown in the following figure), including three pure color backgrounds and three scene backgrounds. There are 1266 hand-crafted identities (547 females and 719 males) and each identety has 36 viewpoints (sampled every <a href="https://www.codecogs.com/eqnedit.php?latex=0^{\circ}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?10^{\circ}" title="10^{\circ}" /></a> from <a href="https://www.codecogs.com/eqnedit.php?latex=0^{\circ}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?0^{\circ}" title="0^{\circ}" /></a> to <a href="https://www.codecogs.com/eqnedit.php?latex=0^{\circ}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?350^{\circ}" title="350^{\circ}" /></a> ).

![fig1](https://github.com/sxzrt/Dissecting-Person-Re-identification-from-the-Viewpoint-of-Viewpoint/blob/master/images/fig1.jpg)  

## Table of Contents

- [Link of the Dataset](#link-of-the-dataset)
	- [Data of CVPR19 ](#data-of-cvpr19)
	- [Data of a new baseline ](#data-of-a-new-baseline)
- [Instructions of the System](#instructions-of-the-system)
- [Guide of Getting Images](#guide-of-getting-images)

****
## Link of the Dataset
### Data of cvpr19 
3D identetie models of PersonX and images of above 6 backgrounds can be downloaded from the following links:<br>
* Baidu Yun Drive: 
	* 3d model of person [link](https://pan.baidu.com/s/1oi9ObdnktrXe5ShiwIspSw)
	* images of six backgrounds [link](https://pan.baidu.com/s/1DyUWMKxLPHbiEs9RuKq7xA)<br>
* Google Drive: 
	* 3d model of person [link](https://pan.baidu.com/s/1oi9ObdnktrXe5ShiwIspSw)
	* images of six backgrounds [link](https://drive.google.com/open?id=17QlzY6ai84SkrCmCOzemPMx9FjWyBPW8)<br>

Directories & Files of images
```shell
PersonX_v1
├── 1/ # this number is coresponds with the background shown in above figure.
│   ├── bounding_box_test/
│   │      ├── 0001_c1s1_01.jpg
│   │	   ├── 0001_c1s1_02.jpg
│   │      └── 0001_c1s1_03.jpg
│   ├── bounding_box_train/
│   │      ├── 0004_c1s1_01.jpg
│   │	   ├── 0004_c1s1_02.jpg
│   │      └── 0004_c1s1_03.jpg
│   └── query/
│          ├── 0001_c1s1_32.jpg
│    	   ├── 0002_c1s1_02.jpg
│          └── 0003_c1s1_15.jpg   
├── 2~6/ 
│   └── ...
└── readme.txt
```

### Data of a new baseline
This datatet also contains 6 cameras, but it is more chanllending than the data used in CVPR19. The data and results will come soon!

Name of the image

Taking "0001_c1s1_33.jpg" as an example: 
*  0001 is the id of the person
*  c1   is the id of the camera (background)
*  s1   has no special meaning
*  33   is the viewpoint of the person


## Instructions of the System
The package can be imported into any program of Unity directly. 
*  The version of Unity used in this work is [2018.1.8 f1 Personal](https://unity3d.com/unity/whatsnew/unity-2018.1.8) that can be downloaded from the [Unity Website](https://unity3d.com/).
*  "PersonX1266.unitypackage" is a Unity package that contains the original 3D models of the identities. it can be imported into the project by double-click. 
*  The scenes (backgrounds) can be selected or designed based on your demand and there are many free sources in Unity Asset Store. If you want to use the scenes used in this work, please send an email to xxsunzrt@gmail.com.

## Guide of Getting Images

We have supplied a example of a controller "example-controllerc.unitypackage" that can make the person to rotate and can capture the images automatically.

#### 1. Import the Game_Manager_Demo into your project (*e.g.,* new project)

<div align=left><img src="https://github.com/sxzrt/Instructions-of-the-PersonX-dataset/blob/master/images/1.png" width="800" /></div>


#### 2. Add the controller (Game_Manager_Demo) into the project and run it
* deleting the original camera in the new projet 
* dragging the Game_Manager_Demo into the SampleScene. 
* running ▶️ and getting the images of a person with different viewpoints

<div align=left><img src="https://github.com/sxzrt/Instructions-of-the-PersonX-dataset/blob/master/images/v1.gif" width="800" /></div>

Components in Game_Manager_Demo
```shell
Game_Manager_Demo
├── PeoplePosition  # control the position, rotation interval of the person
│   
│     
├── Camara # capture images of person without background
│ 
│ 
└── Main Camera # capture images of person 
```
 
 Main Camera and Camera are used to generate a pair of images that have cintains the same person in same position. One is    without background, which is used to caculate the bounding box of the person:



#### 3. Notice


 **!!**  the property of people and two cameras:

* The layer of all person is role;
* The culling mask of Camera is role (only)，so images captured by Camera contains the person without background;
* The culling mask of Main Camera is Everything.
 
 
 **!!**  two paths:


* The name of the path containing the person models shoud be "Resources" (iyou can directly import our unitypackage);

* The 24th line of Manager.cs is the path to save the generated images, which is better **not** to be the sub-path of the project (because  Unity will import the generating images, which will slow the generation process.).
 

**!!**  the ID of the first person:
    
* To matching of the frames between two cameras, the first inputted person will loss one image. Therefore, we use ID 0 (a copy of ID 1) to initial the process, which dose not count towards the 1266 identities. 


**!!**  the version of Unity:
    
* High version of unity, such as 2019.2.6.f1, may cause the loss of motion of person, so please choose a suitable version Unity. 

#### 4. The script crop_bbox.m can be used to get bounding boxes of person, crop and rename images.

**** 
If you use this dataset in your research, please kindly cite our work as, <br>
```
@inproceedings{sun2019dissecting,
	title={Dissecting Person Re-identification from the Viewpoint of Viewpoint},
	author={Sun, Xiaoxiao and Zheng, Liang},
	booktitle={CVPR},
	year={2019}
}
```
