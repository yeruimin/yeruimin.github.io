---
title: 深度学习框架安装
categories: [homework]
comments: true
---

一些参考资料：
+ [pytorch-ljj](https://github.com/info-ruc/Web-20)
+ [Anaconda配置虚拟环境](https://zhuanlan.zhihu.com/p/94744929)
+ [Jupyter Notebook 自动代码补全插件](https://blog.csdn.net/weixin_37595559/article/details/81540482)
+ [jupyter Notebook加目录](https://cloud.tencent.com/developer/article/1407815#:~:text=%E5%90%AF%E5%8A%A8%20Jupyter%20Notebook%EF%BC%8C%E5%BC%80%E5%90%AF%E7%9B%AE%E5%BD%95%20%20%E4%B8%8A%E9%9D%A2%E4%B8%A4%E4%B8%AA%E6%AD%A5%E9%AA%A4%E9%83%BD%E6%B2%A1%E6%8A%A5%E9%94%99%E5%90%8E%EF%BC%8C%E5%90%AF%E5%8A%A8%20Jupyter%20Notebook%EF%BC%8C%E4%B8%8A%E9%9D%A2%E9%80%89%E9%A1%B9%E6%A0%8F%E4%BC%9A%E5%87%BA%E7%8E%B0%20Nbextensions,Jupyter%20Lab%20%E7%9A%84%20GitHub%20%E3%80%82.%20%E6%9C%AC%E6%96%87%E5%8F%82%E4%B8%8E%20%E8%85%BE%E8%AE%AF%E4%BA%91%E8%87%AA%E5%AA%92%E4%BD%93%E5%88%86%E4%BA%AB%E8%AE%A1%E5%88%92%20%EF%BC%8C%E6%AC%A2%E8%BF%8E%E6%AD%A3%E5%9C%A8%E9%98%85%E8%AF%BB%E7%9A%84%E4%BD%A0%E4%B9%9F%E5%8A%A0%E5%85%A5%EF%BC%8C%E4%B8%80%E8%B5%B7%E5%88%86%E4%BA%AB%E3%80%82.)
+ [jupyter环境打开](https://blog.csdn.net/weixin_43682519/article/details/109852577)
+ [jupyter kernel问题](https://blog.csdn.net/weixin_43682519/article/details/109852577)
## 配置一个环境

进入Anaconda Prompt：

+ 查看当前所有环境

```shell
conda info -e
```
+ 创建虚拟环境

```shell
conda create -n [*环境名*] python=3.7
```
+ 激活虚拟环境

```shell
conda activate [*环境名*]
```

+ 退出虚拟环境

```shell
conda deactivate [*环境名*]
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

+ 安装Jupyter notebook代码自动补全插件：

在需要自动补全代码的环境（Anaconda Prompt）下，需要关闭jupyter notebook：

+ 安装nbextensions：

```shell
pip install jupyter_contrib_nbextensions
jupyter contrib nbextension install --user
```
+ 安装nbextensions_configurator

```shell
pip install jupyter_nbextensions_configurator
jupyter nbextensions_configurator enable --user
```

+ **遇到问题**：安装成功后在base环境下可以正常使用，在tensorflow2环境下出现异常：
+ **解决方案**：

原因：两个环境下的jupyter notebook 版本不同；从anaconda中改虚拟环境的版本。

+ jupyter notebook加目录


---
## 配置Pytorch

### 安装CUDA
+ 查看CUDA版本

在CMD中输入：
```shell
nvcc --version
```
鉴于没有GPU，就不安装CUDA了，直接装CPU版本的吧

+ 安装CPU版本

[pytorch官网](https://pytorch.org/)

在官网上选择对应的CPU版本

```shell
conda install pytorch torchvision torchaudio cpuonly -c pytorch
```

+ 加载pytorch

```python
import torch
```
