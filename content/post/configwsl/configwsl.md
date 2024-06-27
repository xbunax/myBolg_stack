---
title: "Configwsl"
description: 
date: 2024-03-24T11:37:50+08:00
image: https://raw.githubusercontent.com/xbunax/blogImg/main/202403241154248.webp 
math: 
license: 
categories: [
"wsl",
"anaconda",
]
hidden: false
toc: true
comments: true
draft: false
---

微软在拥抱开源社区后推出`wsl`极大提升了Windows的开发体验，相比双系统`wsl`可以动态分配存储空间和内存，并且搭配`vscode`可以获得几乎原生`Linux`的开发体验。

在微软更新`wsl2`之后，现在可以与Windows宿主机共用host，不同再去获取`wsl2`的动态IP，每次都要手动设置代理，更加方便开发了。

本篇博文主要是记录一下在`wsl2`中配置深度学习环境。
***

## Install wsl2

+ 要安装`wsl2`首先要在系统服务中打开`hyper-V`虚拟化以及`Linux sub system`。
+ 在Windows应用商店中搜索`Ubuntu`直接安装就可以了。

> + 因为`wsl2`默认安装在C盘，所以可以在poweshell中用`wsl`命令将`Linux`子系统打包成`tar`或者镜像文件，然后export到另外的分区中。

## Config wsl2

+ 首先启动需要设置好`username`和`passwd`

+ 我个人使用`zsh`搭配`oh my zsh`美化比较多。可以使用`apt`安装
```
  sudo apt update
  sudo apt install zsh
  sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
+ 接下来安装深度学习必备的`python`环境，`anaconda`作为`python`的环境管理有点太重了，推荐使用`miniconda`
```
  wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh 
  bash Miniconda3-latest-Linux-x86_64.sh
```
+ 如果要使用GPU加速，还需要安装`CUDA-TOOlkit`以及`NVIDIA Driver`，这部分工具链已经很完善了，微软也提供了完善的[官方文档](https://learn.microsoft.com/en-us/windows/ai/directml/gpu-cuda-in-wsl)。

  1.首先安装`NVIDIA Driver`，这个可以直接在`NVIDIA`官网上找到，安装与自己GPU型号对应的驱动即可
  > TIPS: 安装的时候选择Windows版驱动即可。
  
  2.接着安装`CUDA`支持
```
  sudo apt-key del 7fa2af80 #去除旧的GPG key 

  wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-wsl-ubuntu.pin
  sudo mv cuda-wsl-ubuntu.pin /etc/apt/preferences.d/cuda-repository-pin-600
  wget https://developer.download.nvidia.com/compute/cuda/12.4.0/local_installers/cuda-repo-wsl-ubuntu-12-4-local_12.4.0-1_amd64.deb
  sudo dpkg -i cuda-repo-wsl-ubuntu-12-4-local_12.4.0-1_amd64.deb
  sudo cp /var/cuda-repo-wsl-ubuntu-12-4-local/cuda-*-keyring.gpg /usr/share/keyrings/
  sudo apt-get update
  sudo apt-get -y install cuda-toolkit-12-4
```
  3.确认安装是否完成
  ```
  nvcc -v #查看nvcc编译器是否安装
  nvidia-smi #查看gpu状态
  ```
  接下来安装一下`pytorch`，即
  ```
  conda install pytorch torchvision torchaudio pytorch-cuda=12.1 -c pytorch -c nvidia # 这里使用cuda12.1
  ```
  安装完成后可以在`python`中用`torch.cuda.is_available()`查看是否可以调用`GPU`加速。
  










