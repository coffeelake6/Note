# 			Typora的激活教程

## 激活

安装路径：**Typora\resources\page-dist\static\js**

​	找到**LicenseIndex**文件

​	记事本打开这个文件，ctrl定位到

​	`**e.hasActivated="true"==e.hasActivated**`

​	替换为

​	`**e.hasActivated="true"=="true"**`

---

## 关闭激活弹窗

安装路径：**Typora\resources\page-dist\license.html**

​	ctrl+f定位到：

​	**`</body></html>`**

​	替换为

​	**`</body><script>window.οnlοad=function(){setTimeout(()=>{window.close();},5);}</script></html>`**

---

## 去除未激活提示

安装路径： **Typora\resources\locales\zh-Hans.lproj\Panel.json** 

​	json文件记事本打开

​	**"UNREGISTERED":"未激活"，**>>>**"UNREGISTERED":" "**

 