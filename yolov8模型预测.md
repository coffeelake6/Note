# yolov8模型预测

官方文档：

​	[Predict - Ultralytics YOLO Docs](https://docs.ultralytics.com/modes/predict/#inference-arguments)

```python
from ultralytics import YOLO #从ultralytics库导入YOLO类

yolo = YOLO("./yolov8n.pt",task="detect")#实例YOLO对象，指定模型

result = yolo(source="path") #指定路径（img,videos,screen,VideoCapture"0"）
```

在**ultralytics/cfg**目录下，有一个**default.yaml**文件，里面有很多**train settings**，其次在ultralytics官网也可以查询

---

### 预测可视化

```python
plt.imshow(result[0].plot()[:,:,::-1])
```

show出来默认是BGR格式，所以需要转换成RGB [:,:,::-1]

---

### 讲解一下result[0] “预测结果”

​	在使用YOLO模型进行目标检测时，`result`是一个包含所有检测结果的列表或集合。这些结果通常是多个检测框（bounding boxes），每个框可能对应不同的物体检测到的结果。

`result[0]`表示提取第一张图像的检测结果。因为我们只处理了一张图像

（`source="ultralytics/assets/dog.png"`），所以`result[0]`就是这张图像的检测结果

---

### result[0].plot() 

​	调用 `plot()` 方法时，它会处理 `result[0]` 中的数据，生成一个可视化的图像

​	与`plt.plot()`一个思路

---

### 获取检测数据[list]

​	yolo检测到的数据会返回一个list值，里面包含很多数据，其中`boxes`属性包含了检测到的所有目标物体的边界框信息。

​	如果想获取边界框的数据，则可以如下操作：

​	1.`result[0].boxes.xywh.cpu().numpy()`它会返回一个numpy数组格式的数据

​	2.`xywh` 表示边界框的坐标以及其宽度和高度

​	3.如果检测是在 GPU 上执行的，那么相关数据会在 GPU 的内存中。`cpu()` 方法用于将这个张量从 GPU 内存转移到 CPU 内存，以便于后续处理或转化为 Numpy 格式。这样可以确保在普通的 Python 环境中能够顺利使用该数据。

​	4.`numpy()` 方法被调用以将张量转换为 NumPy 数组。NumPy 数组在数据处理和分析中更加通用，因此这一转换使得我们能够用更标准的方式来处理和分析边界框数据。