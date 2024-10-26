# Anaconda虚拟环境更改目录

---

## 好好看好好学

我的电脑为例

​	`C:\Users\CoffeeLake\.condarc`

```
envs_dirs:
 	- D:\Anaconda3\envs
```

把上面这个搞进去，绝对路径自己选

---

然后

点env的属性——编辑——选中users——权限全开

---

### 一些指令

---

创建虚拟环境

`conda create -n demo python=version`

进入虚拟环境

`conda activate demo`

查看虚拟环境

`conda env list`

删除虚拟环境

`conda remove -n demo --all`

下载

`conda install example`