# 数据集

[TOC]

## 构建

我们在进行yolo模型训练之前，需要一定的数据集，也就是大量的**图片**，然后我们需要对图片进行**标注**，并生成**标签**文件，最后进行数据集的**整理**

一下是具体的操作方法

### 1.获取图片

​	1.1 在互联网上获取图片素材，这比较繁琐(不推荐)

​	1.2 获取现成的数据集(别人整理好的，直接扒拉过来)

​		获取数据集的网站

> ​		[Kaggle: Your Machine Learning and Data Science Community](https://www.kaggle.com/datasets)
>
> ​		[数据集-OpenDataLab](https://opendatalab.com/)
>
> ​		[[Roboflow Universe: Open Source Computer Vision Community](https://universe.roboflow.com/))

​	1.3 视频抽帧(openCV)

​		如果你想在视频中获取图片素材，那么可以进行视频截取(抽帧)

​		这边用到了**openCV**这个库来实现视频抽帧功能，并存储到文件夹下

```python
import cv2
video = cv2.VideoCapture("视频路径.mp4")

num = 1
step = 30 #计步器，30帧抽一张
while True:
    ret, frame = video.read()#读帧
    if not ret:
        break
    num +=1
    #进行抽帧(每30帧抽一张)
    if num % step ==0
    	cv2.imwrite("保存图片的路径/"+ str(num)+".jpg",frame) #保存在路径下，更名为遍历的num数字，后缀jpg
```

上述代码运用了openCV来进行视频截帧，并将图片保存到自定义文件夹下，更名为有序排列数字，方便整合。

---

### 2.数据标注

​	这边用到了make sense来进行数据标注

> 网址	[Make Sense](https://www.makesense.ai/)

​	step：getStart—open img—project predict—添加标签—start project—标完后—actions—export annotation—zip格式选yolo

​	如果数据量太大，可以借助预先训练好的模型进行辅助标注

​	Actions—run ai locally(这个网站目前只能加载yoloV5的模型)

---

​	目前推荐使用**roboflow**来进行数据标注

> 网址 
>
> [Workspace Home](https://app.roboflow.com/coffeelake-mwec6)

​	数据集资源和标注都可以在上面搞，还是很方便的，但是需要魔法软件

> [深度学习（10）之Roboflow 使用详解：数据集标注、训练 及 下载-CSDN博客](https://blog.csdn.net/yohnyang/article/details/131353572)

---

### 3.创建数据集文件夹

​	注意按照以下目录结构创建：

```
数据集的文件名demo：
        train(训练集)
            images(图片素材)
            labels(标注数据)
        val(验证集)
            images(截取一部分)
            labels(截取一部分)
		
```

> ​	tips：      1.图片和标签的命名保持一致
>
> ​			2.验证集的素材在训练集中剪切一小部分，用来验证模型

---

---

## 训练

[参考文档]: https://blog.csdn.net/weixin_44765053/article/details/140373295?ops_request_misc=&amp;request_id=&amp;biz_id=102&amp;utm_term=yolov8%E8%AE%AD%E7%BB%83%E6%A8%A1%E5%9E%8B&amp;utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-140373295.142^v100^pc_search_result_base1&amp;spm=1018.2226.3001.4187

### 1.创建datasets

​	在项目文件中创建datasets文件夹，用于存放训练集

### 2.配置yaml参数

​	在训练集根目录下，创建一个data.yaml文件

```yaml
path: your_file_name
train: ../datasets/train/images
val: ../datasets/val/images
test: 

names:
	0: car
	1: person
	......
```

>  配置参数

### 3.编写训练代码

```python
from ultralytics import YOLO

#加载预训练模型
model = YOLO('yolov8n.pt')

#训练模型
model.train(data='data.yaml',workers=0,epochs=300,batch=16)
```

如果训练意外中断，那么可以输入以下命令

`yolo train resume model=path/to/last.pt`



### 4.训练结束

​	训练结束后会在runs目录下生成训练数据，其中就包括训练好的模型，用的话就调用**best.pt**,继续优化就用**last.pt**
