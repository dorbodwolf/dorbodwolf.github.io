# 1.语义分割任务的挑战

参考[Zhang Bin's Blog](https://zhangbin0917.github.io/2018/06/03/Encoder-Decoder-with-Atrous-Separable-Convolution-for-Semantic-Image-Segmentation/)  
参考[知乎you62580](https://zhuanlan.zhihu.com/p/56454327)  
参考[博客园-飞翔的荷兰人F](https://www.cnblogs.com/FLYMANJB/p/10126854.html)  

连续的卷积和池化有利于网络学习到更加抽象的特征表示，但是会造成特征分辨率降低，对于语义分割任务来说这样会损失很多细节  

### 1.1 encoder-decoder结构  
encoder-decoder结构是Deeplabv3+模型的总体结构。encoder-decoder结构翻译成编码器-解码器结构，该结构应用于seq2seq问题，其缺点是编码过程容易损失信息。编码，就是将输入序列转化为一个固定长度的向量；解码，就是将之前生成的固定向量再转化成输出序列。  

编码过程中，特征图的空间维度逐步减小，所以在较深的编码层输出中可以更容易捕获长距信息。解码过程中，对象细节和空间维度逐步恢复。  

SegNet,U-NET,RefineNet都采用了编码-解码结构，这类模型在目标检测任务中同样常见。  

### 1.2 一些多尺度概念  
（陈高星语录:以前做图像处理的时候，多尺度能解决好多问题，就是因为多尺度符合人类的视觉原理。由大到小，由粗到细，综合分析。）  

图像金字塔：小尺度的输入可以捕获长距内容，大尺度的输入可以捕获小对象的细节，组合各个尺度的特征图合并形成多尺度特征。  

空间金字塔池化：池化过程中捕获多尺度的上下文信息。空间金字塔池化首次在2014年引入SPPNET目标检测任务中，证实了通过重采样在单一尺度提取的卷积特征来实现任意尺度区域准确有效的分类。

**现给出空间金字塔池化的一种形式：对于输入为wxh的特征图，通过重采样获得4x4 2x2 1x1共三种尺寸的特征图总共21个块，对每个块执行最大值池化，获得21维的固定长度向量**

膨胀卷积：膨胀卷积（atrous convolution）最早在1989年被M. Holschneider等人用在小波变换中。DeepLabV3开始使用膨胀卷积来解决语义分割的问题，发现膨胀卷积对于语义图像分割很有用，利用膨胀卷积可以控制特征的分辨率而无需学习新的参数。  

# 2.膨胀卷积用于语义分割任务

### 2.1 膨胀卷积用于密集特征提取和视域扩大 

#### （1）密集特征提取
语义分割是一类密集预测任务。膨胀卷积在最初的Deeplab中就用于减少显著的下采样（downsampling）程度。  
利用带孔的膨胀filter来卷积原始分辨率的图像，孔的位置填充0值，计算时候只需要关注非0的值，所以实际的filter参数个数和每个位置的运算数都保持不变，但是这样很明显我们能够轻松控制输出特征的空间分辨率。  

#### （2）视域扩大
小的视域能够捕获准确的局部信息，而大的视域能够捕获上下文关联信息。膨胀卷积可以用在任何DCNN层中来调节视域，通过控制膨胀参数`r`的大小可以帮助我们找到合适大小的视域，笔者在DeepLab-LargeFOV模型中将r=12用在VGG-16的`fc6`层中，获得了显著的性能提升。  

### 2.2 基于膨胀空间金字塔池化的多尺度图像表达

笔者列举了两种多尺度图像表达的方法。一种方法是训练多个并行的DCNN，这些分支共享参数。通过双线性插值来合并并行的特征图并融合他们，每个位置的预测值选取置信度最高的分支的对应值，但是这种方式会成倍的增加计算量？另一种方法就是基于膨胀卷积的空间金字塔池化。  

笔者采用多个并行的拥有不同采样率`r`的膨胀卷积层来实现空间金字塔池化。每个分支基于对应采样率`r`提取的特征在各自分支被处理，最后融合各个分支来生成最终结果。该方法英文名**atrous spatial pyramid pooling**，简称**DeepLabASPP**，该方法加入了DeepLab-LargeFOV模型中。

### 2.3 膨胀卷积和Xception

在DeepLabV3+中将膨胀卷积用于深度可分离卷积中。  

### 2.4 膨胀卷积的实现方法

膨胀卷积的第一种实现方法是通过补零来放大采样filter，也可以通过稀疏抽样输入特征图来达到效果，笔者在Caffe中实现了这个方法；第二种实现方法是（没看懂。。。），该方法在TensorFlow框架中实现。  

# 3.条件随机场在语义分割任务的应用