---
layout:       post
title:        "第一篇测试文章"
author:       "Zhou"
header-style: text
catalog:      true
tags:
    - Python

---

> Author: Zhou Yafei

## 目录

[TOC]

相对应版本查找：[Tensorflow与Python、CUDA、cuDNN的版本对应表](https://blog.csdn.net/ly869915532/article/details/124542362)

1. 安装GPU加速计算工具包cuda&cudnn
	1. 下载
		[NVIDIA的cuda下载地址](https://developer.nvidia.com/cuda-toolkit-archive)
		[NVIDIA的cudnn下载地址](https://developer.nvidia.com/rdp/cudnn-archive)
	2. 配置
		将cudnn的压缩包解压到用户文件夹`XXX`下，然后将绝对路径`XXX\cudnn8.9.6.50\bin`添加到系统环境变量中。 
		
	
	> 注意：最好使用用户文件夹来存放cudnn。
	
2. 安装python对应的扩展包

```bash
conda create -n xxxEnv python=3.10 # -y
```

```bash
conda activate xxxEnv
pip install tensorflow-gpu==2.10.0
pip install -U ipython
# pip install jupyter
```
3. 验证安装结果

```bash
source activate xxxEnv
ipython


In [5]: tf.test.is_gpu_available()
2023-12-17 18:02:41.815322: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1616] Created device /device:GPU:0 with 3497 MB memory:  -> device: 0, name: NVIDIA GeForce RTX 3060 Laptop GPU, pci bus id: 0000:01:00.0, compute capability: 8.6
Out[5]: True 

In [6]: tf.config.list_physical_devices('GPU')
Out[6]: [PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')]
```

如果`tf.test.is_gpu_available()`输出为`True`则表示能成功使用GPU加速计算。
如果`tf.config.list_physical_devices('GPU')`输出的列表不为空则表示检测到了可用GPU。

## 可用版本

| Package        | version |
| :------------- | :------ |
| cuda           | 11.2    |
| cudnn          | 8.9.6   |
| python         | 3.10.13 |
| tensorflow-gpu | 2.10.0  |




---
## 参考链接
[Tensorflow-gpu安装教程（Win11, Anaconda3，Python3.9）](https://blog.csdn.net/weixin_43412762/article/details/129824339)