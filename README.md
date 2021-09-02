# 2D-target-detection-Bleach-vs-Naruto
《死神VS火影》| 试用YOLOv5完整体验自建数据集，训练模型，参数调优，最后实现2D目标检测的全过程。

## DEMO

![results](https://i.loli.net/2021/09/02/xOJHVcTq8W7fgUQ.png)

![val_batch0_labels](https://i.loli.net/2021/09/02/Jlog7weRvmDTfhr.jpg)

[→ see more demo ](https://www.wolai.com/pHSh6Uuc9x1wwC2GSiLtyf?theme=light)

## Background

NIIT暑期实习大作业

## Install

### Download Project

直接Clone项目即可，推荐使用Pycharm启动工程。

![image-20210902100143483](https://i.loli.net/2021/09/02/4wczdFmJ61BUpyb.png)

### Download Game [optional]

获取《死神vs火影 3.3》FLASH游戏本体

链接：https://pan.baidu.com/s/1gjYlIzwjsYKDt8-cq1AqhA 
提取码：5dyt 

### Download BVN-Network [optional]

获取欠优化的序列模型，可直接用于预测任务

链接：https://pan.baidu.com/s/12Re3w9V56z-J-0LGCPK_IQ 
提取码：digz 

### Download Database [optional]

获取作者手动标注的数据集（未经数据增强）；包含录制的游戏视频及分割成帧的游戏图片，视频分割成帧的`.py`脚本，官方贴图（人物模型），images图片数据集及其对应的labels标注集（使用make-sense导出）

链接：https://pan.baidu.com/s/1o64LCXUk9LR85ipCR9-cSw 
提取码：7qqa 

## Usage

Clone项目后，请标记`database`、`game`目录为“排除”，`network`为“运行根”。

以`./network`为运行根启动`Terminal`，执行`detect.py`进行预测：

```shell
# /2D-target-detection-Bleach-vs-Naruto/network>
python detect.py
```

执行结果存放在`./network/runs/detect/exp[number]`中。

## Project Tree

如下所示为本项目的工程目录。

```python
2D-target-detection-Bleach-vs-Naruto
 ├── database
 │   ├── captures
 │   ├── images
 │   ├── labels
 │   └── role_map
 ├── game
 │   └── 死神vs火影3.3
 ├── LICENSE
 ├── network
 │   ├── data
 │   ├── detect.py
 │   ├── export.py
 │   ├── hubconf.py
 │   ├── LICENSE
 │   ├── models
 │   ├── requirements.txt
 │   ├── runs
 │   ├── train.py
 │   ├── utils
 │   └── val.py
 └── README.md
```

- `./database`存放训练数据

  - `./database/captures`：游戏录屏文件的存放目录
  - `./database/images`：游戏录屏文件切割成帧后的图片存放目录
  - `./database/labels`：图片帧的标注集（与images一一对应）

  - `./database/role_map`：预存放的游戏人物贴图，包含角色一户（卍解）以及漩涡鸣人

- `./game`存放《死神vs火影3.3》FLASH游戏本体

  Windows 客户端直接运行`./game/死神vs火影3.3/launch.exe`进入游戏。

- `./network`目录仿制`YOLOv5`编排

  - `./network/data`存放需要执行预测任务的素材（如：图片、视频）

    - `./network/data/images`：需要执行预测任务的图片存放目录
    - `./network/data/video`：需要执行预测任务的视频存放目录
    - `./network/data/BleachVsNaruto.yaml`：引导模型训练所用数据集路径的配置文件

  - `./network/models`存放yolo基准模型参数

  - `./network/utils`存放构建网络的必要工具

  - `./network/runs`存放网络运行缓存

    - `./network/runs/detect`：由`detect.py`预测任务产生的输出，与所选择的`./network/data/`资源一一对应

    - `./network/runs/train`：由`train.py`训练任务产生的输出，存放导出的模型、网络收敛图以及各种评价指标图

      `./network/runs/train/bvn-base/weights/`中存放了欠优化的序列模型，可直接用于预测任务。

  - `./network/detect.py`预测任务的启动接口

  - `./network/train.py`训练任务的启动接口
