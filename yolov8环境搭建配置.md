# yolov8(Ultralytics)环境搭建配置

## anaconda

- 下载anaconda

- 配置虚拟环境，python指定为3.9，名称为yolov8

  `conda create -n yolov8 python=3,9`

- 配置清华源

  `pip install -i https://pypi.tuna.tsinghua.edu.cn/simple some-package`

##  pytorch

- https://pytorch.org/
- 注意选择cuda11.8以及GPU(N卡)
- 直接用pip下载到conda中的虚拟环境即可
- CUDA选装

### ultralytics安装

- https://github.com/ultralytics/ultralytics
- 这里使用的是pip源码安装(注意版本兼容)
  - 在github下载好源码后，保存到本地
  - 在anaconda虚拟环境下cd进入源码根目录
  - `pip install -e .`

### jupyterlab和tensorboard库

- pip安装到conda环境里

