# 内网win server 2012r2上配置darknet踩坑记

## 0. 长话短说

作者亚历山大AB推荐vcpkg一次性把依赖和darknet安装，类似于pip和conda的效果，但是我的电脑是内网机器，这条路行不通。

所以只能离线安装各种包，然后编译darknet。 作者推荐用他写的build.ps1编译(这个应该是基于cmake工具),但是我没有成功,我最终在vs工程里面编译成功,踩了不少坑.

## 1. 安装requirments 

1) 需要安装vs2019或者2017, 我2017和2019都下载了,但是最后用2017编译的(感谢教练帮忙下载vs离线cache哈哈哈哈)

2) 安装opencv设置环境变量

3) 安装cmake


## 2. 由于需要cuda visual studio intergration 来使vs编译使用cuda编译器,所以官方建议先装vs 然后再安装cuda.

我照做重新卸载安装了cuda,但cuda10.0依然默认用vs 2015编译了,

所以cuda visual studio intergration还是和vs 2015关联起来了,所以这一步对我来说算是白折腾了


## 3 既然第2步没有卵用,所以查资料看如何让vs 2017识别cuda,  

 答案是添加 CUDACXX和 CUDA_TOOLKIT_ROOT_DIR 环境变量来让vs找到cuda

## 4 开始编译 

### 4.1 使用powershell脚本傻瓜式编译
使用默认build.ps1脚本编译(这个应该是用cmake工具链编译的),始终找不到cuda.
网上说安装ninja并设置使用ninja编译,但是尝试了也没用


### 4.2 使用vs手动编译

#### 4.2.1 darknet.sln编译

darknet源码包解压,在build/darknet目录下修改vc++工程属性配置文件darknet.vcxproj与cuda相关内容:

1)cuda版本改成10.0,这是当前安装版本

2)删掉cumpute-86 和sm_86相关配置参数, 因为显卡不支持, RTX30系显卡采用sm_86只有cuda11.1才支持

##### 4.2.1.1 vs2017打开工程编译

首先编辑工程属性来进一步配置opencv路径

参考这个:

https://note.youdao.com/ynoteshare1/index.html?id=04fb326760a726f23cbd9ae8ff6b1fc6&type=note

然后在release x64下编译成功


##### 4.2.1.2 初步测试
在build/darknet/x64下运行darknet.exe显示cuda和opencv都正常使用

但是现在只编译了`darknet.sln`，要想使用yolo目标检测的话还需要编译`yolo_cpp_dll.sln`，要不然会报错，血的教训！！！！

#### 4.2.2 yolo_cpp_dll.sln编译

同darknet的编译，做好cuda配置项修改，添加opencv路径即可


## 5 后续应用

基于以上经验，在外网win server 2019中再次配置darknet。

1）首先尝试了vcpkg

vcpkg可以把darknet相关依赖包全部管理。在配置完成vcpkg后：

`vcpkg search darknet`

可以看到仓库列出了darknet。安装full表示将依赖全部安装，包括opencv和cudnn等：

`vcpkg install darknet[full]:x64-windows`

由于下载源都在github等外网，下载速度非常慢，因此在cmd窗口配置了http_proxy代理来加速下载。一切顺利，直到下载安装opencv4/opencv，build报错。在vcpkg github issue中找到可能的解决方法：单独用aria2下载安装opencv：

./vcpkg install opencv:x64-windows --x-use-aria2

下载安装一切顺利，之后继续安装darknet，安装后位于vcpkg的package下面，测试：

```
PS C:\vcpkg-master\packages\darknet_x64-windows\tools\darknet> .\darknet.exe detector
 GPU isn't used
 Used AVX
 Used FMA & AVX2
 OpenCV isn't used - data augmentation will be slow
```

以上输出说明darknet编译时候没有用到cuda nvcc编译器，也没有找到opencv路径。好吧，放弃vcpkg。

2）尝试使用build.ps1脚本安装

抛开vcpkg，利用官网exe安装了opencv，配置了环境变量，安装darknet：

`.\build.ps1`

build时候cmake找不到opencv的`OpenCVConfig.cmake`文件，所以编译成功后darknet不能使用opencv，darknet主要使用opencv来进行训练时数据增生。

cmake提示两种解决方案：

一是`CMAKE_MODULE_PATH`下包含`findOpenCV.cmake`，该路径在darknet项目根目录的`cmake\Modules`下面，发现这下面包含类似`findCUDNN.cmake`的文件，但是没有`findOpenCV.cmake`文件，这个文件编写很复杂，放弃了自己编写；

cmake提供的第二种解决方案是利用`OpenCVconfig.cmake`，这个文件在opencv build目录下，但是我早先设置的`OpenCV_Dir`路径为`build\x64\vc14`，于是重新设置到`build\`下，但是还是找不到，经查阅发现需要将路径的反斜杠替换为`/`，晕！