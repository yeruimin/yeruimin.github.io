---
title: 深度学习框架安装
categories: [homework]
comments: true
---

一些参考资料：
+ [pytorch-ljj](https://github.com/info-ruc/Web-20)
+ [Anaconda配置虚拟环境](https://zhuanlan.zhihu.com/p/94744929)

## 配置一个环境

进入Anaconda Prompt：

+ 查看当前所有环境

```linux
conda info -e
```
+ 激活虚拟环境

```linux
conda activate [*环境名*]
```
---
## 配置Tensorflow

安装对应版本的Keras和Tensorflow

**本机说明**：tensorflow安装版本为cpu-2.2.0,搭配Keras为2.3.1

+ 查看tensorflow版本：

```python
import tensorflow as tf
#查看tensorflow版本
tf.__version__
#查看tensorflow路径
tf.__path__
```

---
## 配置Jupyter Notebook

配置虚拟环境下的Jupyter Notebook

利用ipykernel包配置Jupyter Notebook的kernel

每次需要调用 **Pyhton[conda env:tensorflow2]**

---
## 配置Pytorch

### 安装CUDA
+ 查看CUDA版本

在CMD中输入：
```linux
nvcc --version
```
鉴于没有GPU，就不安装CUDA了，直接装CPU版本的吧

+ 安装CPU版本

[pytorch官网](https://pytorch.org/)

在官网上选择对应的CPU版本

```linux
conda install pytorch torchvision torchaudio cpuonly -c pytorch
```