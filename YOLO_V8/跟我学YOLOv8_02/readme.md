## 手把手在Anaconda的虚拟环境中运行和学习YOLOv8

为什么要Anaconda的虚拟环境中呢？主要是我们大家的Ubuntu装有了Prometheus或其他项目，所以为了预防一个不熟悉的新项目对原有环境的破坏
，我们选择虚拟环境，同时一个全新的环境可以帮助我们更好了解这个新项目。
# 1、安装Anaconda和PyCharm 
这个就不用多说了吧 

# 2、创建虚拟环境

 1.  **windows下打开Anaconda Prompt**
 2.  **创建名为yolov8的虚拟环境：** 

```python
conda create -n yolov8 python=3.7
```
 3.  **查看conda中已创建的环境：**
 
```python
conda env list
```

 4. **打开新建环境yolov8：**
```python
conda activate yolov8
```
# 3、安装pytorch

1. **检查是否安装pytorch：**<br>

 
在yolov8环境下输入：
```python
python
import torch
import torchvision
torch.cuda.is_available()
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/84267878ef2442e2a231d68924f2cc23.png)<br>
如果输出为False则要安装pytorch

 2. **检查CUDA版本：** <br>
 
在windows的cmd下输入：
```python
nvidia-smi
```
输出的第一行就能看见CUDA的版本，这里为10.2
![在这里插入图片描述](https://img-blog.csdnimg.cn/c7ed9a7eee5147f7968ac68d0195a2b2.png)


3.  **安装pytorch：**<br>
版本要求推荐pytorch==1.12.0+ <br>
 
### CUDA 10.2
```python
conda install pytorch1.12.1 torchvision0.13.1 torchaudio==0.12.1 cudatoolkit=10.2 -c pytorch
```
### CUDA 11.3

```python
conda install pytorch==1.12.1 torchvision==0.13.1 torchaudio==0.12.1 cudatoolkit=11.3 -c pytorch
```

### CUDA 11.6

```python
conda install pytorch==1.12.1 torchvision==0.13.1 torchaudio==0.12.1 cudatoolkit=11.6 -c pytorch -c conda-forge
```

### CPU Only

```python
conda install pytorch==1.12.1 torchvision==0.13.1 torchaudio==0.12.1 cpuonly -c pytorch
```
# 4、下载yolov8源码
https://github.com/ultralytics/ultralytics <br>
![在这里插入图片描述](https://img-blog.csdnimg.cn/a0f49418fea645c3869277a2cf48cb70.png)
<br>下载到电脑后解压
# 5、设置PyCharm <br>
在PyCharm中新建项目，并打开源码的项目文件，并在setting中按照刚刚查看的conda环境来选择python Interpreter(解释器):<br>
![在这里插入图片描述](https://img-blog.csdnimg.cn/912c0832ac0f47ff8e963d64a3dfec03.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/0358d5861ec34c589a5c32f1c7e32183.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/cd8efe9873eb41889e6b9d57e33e5279.png)


最后在pycharm的终端Terminal中出现(yolov8)的前缀即成功

![在这里插入图片描述](https://img-blog.csdnimg.cn/aab18981f0384c0bac0c4ecb3e93d4bf.png)

# 6、安装依赖  <br>
在pycharm终端Terminal中（代码目录下）安装依赖：

```python
pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
```

```python
python setup.py install
```
setup.py安装后会输出比较多的信息，主要看最后是否输出Finished processing即可
![在这里插入图片描述](https://img-blog.csdnimg.cn/fb170bcec9384ba582a4c1b6f4231f61.png)
# 7、训练数据集 <br>
在下载后的项目文件夹中找到名为default的执行文件
![](https://img-blog.csdnimg.cn/1115195d5dc84611a37e09a82c6e8e01.png)
 <br>和官方不同，这里可以选择直接在配置文件中更改参数，会更简单便捷 <br>
打开后如图所示： <br>
![在这里插入图片描述](https://img-blog.csdnimg.cn/bd51704ee55e437fa02bcb980ed6b6de.png)

 <br>在配置文件中，我修改了3个参数，分别是model（模型）、data（数据集）、workers（数据装载时cpu所使用的线程数），分别把它们来自内容根目录的路径复制粘贴到上面的配置文件中 <br>
这里使用的参数：<br>
1. model：yolov8n.yaml  <br>
路径复制方式如下图所示，把路径复制粘贴到执行文件中 <br>
![在这里插入图片描述](https://img-blog.csdnimg.cn/7d993077726e4ae1b5c293ac876e7ad1.png)
2. data：coco128.yaml <br>
这里我先使用了官方的数据集，同样复制路径粘贴到执行文件中 <br>![在这里插入图片描述](https://img-blog.csdnimg.cn/219c30ea61b14e899710e50eec393669.png)
3. workers：4 <br>
这里我把workers改为了4个 <br>

改好参数后，保存执行文件，在Pycharm的Terminal终端下（即代码目录下），输入:

```python
cfg-ultralytics/yolo/configs/default.yaml
```
(后缀即为执行文件的路径）<br>
一切就绪时，这时候就开始训练了：<br>![在这里插入图片描述](https://img-blog.csdnimg.cn/68183cc1ba1f453f86a6dc2adaa59496.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/cc243b9953324f9e8244b2b01ca80315.png)
<br>
历经4.25个小时，完成训练：<br>

![在这里插入图片描述](https://img-blog.csdnimg.cn/9f4d6f5bd80645f197415f80fc597e84.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/f610435e07544664809edf3c9ae0d6e9.png)

训练好之后 ，它会把所有识别好的图片放在新的文件夹里，下图是识别出来的部分图片
<img width="942" alt="d95a770d55ca468fdd6aa78adb89516" src="https://user-images.githubusercontent.com/68007558/213872642-0b7366fe-a8cc-4830-bb83-2fa030bf59c6.png">

<img width="938" alt="9fd827c5b92de0efabe1e54c103a0e6" src="https://user-images.githubusercontent.com/68007558/213872630-66f4b28f-180b-4b8d-be46-307c71cb85ee.png">


<img width="722" alt="cdb74d541e855bc011f9a76ac2e6d96" src="https://user-images.githubusercontent.com/68007558/213872653-23678ebd-4fe5-4d42-be50-4a9d2dc92f48.png">

<img width="719" alt="c897acd1d4fd4fb830a7d0587a09eba" src="https://user-images.githubusercontent.com/68007558/213872656-238dc81c-a434-4876-bbe7-08f877e0f368.png">

