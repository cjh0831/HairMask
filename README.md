# NeuralHaircut hair mask

该工程复制于[NeuralHaircut](https://github.com/SamsungLabs/NeuralHaircut)，为其中预处理数据头发mask，及2d ori代码  
该方法分别使用了[MODNet](https://github.com/ZHKKKe/MODNet)和[CDGNet](https://github.com/tjpulkl/CDGNet)求人体 mask 及 对应头发 mask。

## 运行准备

### 环境依赖

- Python 3.9
- Pytorch 1.13.0
- NVIDIA GPU + CUDA 11.7

### 环境安装

使用 conda 安装新环境
```
conda create -f environment.yaml
```

或在已有 conda 环境上安装
```
conda install pytorch==1.13.0 torchvision==0.14.0 torchaudio==0.13.0 pytorch-cuda=11.7 -c pytorch -c nvidia
conda install matplotlib tqdm 
```

### MODNet 及 CDGNet 下载预训练模型

[MODNet预训练模型](https://drive.google.com/drive/folders/1umYmlCulvIFNaqPjwod1SayFmSRHziyR?usp=sharing)  
将其中的``modnet_photographic_portrait_matting.ckpt``文件下载至``./MODNet/pretrained/``文件夹中  
[CDGNet预训练模型](https://drive.google.com/drive/folders/1E9GutnsqFzF16bC5_DmoSXFIHYuU547L)  
将其中的``LIP_epoch_149.pth``文件下载至``./CDGNet/snapshots/``文件夹中（该文件夹需创建）

### 修改部分包依赖结构

``./CDGNet/networks/CDGNet.py``第12行
```
from utils.attention import CDGAttention, C2CAttention
改为
from CDGNet.utils.attention import CDGAttention, C2CAttention
```

## 运行

scene_path 文件结构
- image (图片文件夹)
- mask (人体 mask 生成文件夹，可不提前创建)
- hair_mask (头发 mask 生成文件夹，可不提前创建)

样例：
```
python calc_masks.py --scene_path ./test
```
