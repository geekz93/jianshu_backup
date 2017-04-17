## 设置参数
- **打开abaqus**
运行：C:\SIMULIA\Abaqus\Commands\abq_cae_open.bat
- **建立模型**
Create Model Database下选择with standard/Explicit Model
建立一个part，在弹出对话框中修改命名，其它默认，continue
![](http://upload-images.jianshu.io/upload_images/3022282-b838b53a319eb717.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
拉伸一个实体，3d建模都类似操作
![](http://upload-images.jianshu.io/upload_images/3022282-b84c54fe52526cb8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- **设置材料**
密度    弹模     伯松比
2.85e-9 206000 0.33
![](http://upload-images.jianshu.io/upload_images/3022282-fb4deb9c77afff15.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
自定义名词，在General中设置材料的密度Density，在Mechanical中设置形变Elasticity->Elastic（设置弹性模量和伯松比）**这些量在软件中的单位是什么?**
![](http://upload-images.jianshu.io/upload_images/3022282-05a949caed25f8f3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- **建立section**
先使create，按默认设置创建，再在section的manager中选择创建的section再选择dismiss。（不知道为什么这样做，可能是为assign作准备）
![](http://upload-images.jianshu.io/upload_images/3022282-10a0f61c1470909c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- **将section与建立的part关联**
Assign -> section，点击刚刚建立的模型，输入名称 -> done
![](http://upload-images.jianshu.io/upload_images/3022282-b10a4a1c4cad5503.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- **建立Assembly**
Module->Assembly建立一个实例
![](http://upload-images.jianshu.io/upload_images/3022282-08604bc1eaa5a018.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- **step**
![](http://upload-images.jianshu.io/upload_images/3022282-a229978d69d1ce03.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
选择Dynamic Explict，在弹出的框中设置时间段，和时间增量，设置好后dismiss（**这里的设置应该和后面的仿真动画有关**）
![](http://upload-images.jianshu.io/upload_images/3022282-356c83c57d13fa41.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](http://upload-images.jianshu.io/upload_images/3022282-3e65a37da505186e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- **画线框**
目的：线框的交点为后面放置传感器的位置
选择一个面作图
![](http://upload-images.jianshu.io/upload_images/3022282-3dc792f32a43ab2d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- **设置传感器**
Tools -> Set -> Manager -> Create，输入名称后，在刚刚画的线框上选择一个交点，作为传感器的放置位置，完成后按dismiss
- **添加负载——设置头波信号**
Amplitude -> Tabular -> Continue
![](http://upload-images.jianshu.io/upload_images/3022282-6d32d84b0e6186f9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
选择Total time，导入数据（**头波信号**）这里的数据与step中设置的时间有什么关系？
![](http://upload-images.jianshu.io/upload_images/3022282-dd32a458f305d709.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- **添加负载——设置负载位置**
双击Loads，弹出对话框按默认设置continue
![](http://upload-images.jianshu.io/upload_images/3022282-c1df4183acac9675.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
在图中选择一点作为负载的作用点，设置方向，在Amplitude中选择刚刚设置的Amp-1
![](http://upload-images.jianshu.io/upload_images/3022282-0b30f1ea4345ca8e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- **设置网格**
![](http://upload-images.jianshu.io/upload_images/3022282-53b7359caf999f44.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](http://upload-images.jianshu.io/upload_images/3022282-96e25f6ee07cae75.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- **设置Job**
![](http://upload-images.jianshu.io/upload_images/3022282-969e4d3ae05a935c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
在导航兰中选择Field Output Requests -> 双击下面的F-Output-1 编辑
![](http://upload-images.jianshu.io/upload_images/3022282-1a9c279950c21ed4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
在History Output Requests中设置H-Output-1，双击History Output Requests新建另外两个H-Output，记录3个传感器的数据
![](http://upload-images.jianshu.io/upload_images/3022282-921a96afad6ef6c3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
**建立Job-1**
进行计算的最后配置，配置使用多少个核，计算的精度，配置完了，点击submit就开始进行计算了，漫长的等待......
![](http://upload-images.jianshu.io/upload_images/3022282-9e14e6f463a21c44.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](http://upload-images.jianshu.io/upload_images/3022282-6dd6f06f78b42f4c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 查看计算结果
在job manager中点击result切换到结果显示界面
先选择U3，再配置成黑白颜色
![](http://upload-images.jianshu.io/upload_images/3022282-1f00ea8655e84292.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](http://upload-images.jianshu.io/upload_images/3022282-a782d9964e8dd85d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
设置Feature edges
![](http://upload-images.jianshu.io/upload_images/3022282-0e23ab12182d90d4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- **显示动画**
![](http://upload-images.jianshu.io/upload_images/3022282-dc6879026af3fa1a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- **显示彩色动画**
![](http://upload-images.jianshu.io/upload_images/3022282-98a677bc9d89b2ad.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- **查看时域图**
![](http://upload-images.jianshu.io/upload_images/3022282-6360797ad8370eb4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- **保存数据**
step1：
![](http://upload-images.jianshu.io/upload_images/3022282-4837899469bfd525.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
step2：Report -> XY -> OK
![](http://upload-images.jianshu.io/upload_images/3022282-4b98cb5355fcca4b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
step3：保存为abaqus.rpt文件，用记事本打开就可以看到数据
![](http://upload-images.jianshu.io/upload_images/3022282-90e3af2668bab233.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

50e-9 ~ 150E-6
