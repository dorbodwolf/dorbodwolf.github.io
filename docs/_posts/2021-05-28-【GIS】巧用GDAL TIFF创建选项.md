# 1 简介

gdal支持众多栅格驱动器，GeoTIFF就是其中最常用的，TIFF格式有很多创建选项（Create Option），在代码中和脚本中可以指定这些创建选项来自定义TIFF文件输出。在GDAL自带脚本中可以通过`-co`选项来添加创建选项。

# 2 脚本实例--镶嵌时应用

利用Google earth engine线上做地物分类，分类结果下载到本地是分幅存储的，需要镶嵌起来，保存结果想要尽可能压缩来提高存储效率。

### 版本1

不做压缩，直接输出，会占用空间很大。

`python3 -m gdal_merge -ot Byte -of GTiff -o F:/曹县666.tif`

### 版本2

输出结果做lzw压缩，可以有效节省空间。

许多人没有意识到，压缩方案在很大程度上取决于要处理的数据，在一个数据上运行良好的方案可能会在下一个很差。

但是由于我们不想给世界负担太多压缩方案，需要一种自适应方案，不求最好，但求在绝大多数图像上表现的不错，LZW具有这样的品质。


`python3 -m gdal_merge -ot Byte -of GTiff -co COMPRESS=LZW  -o F:/曹县666.tif`


### 版本3

某些图像首先经过一个处理，其中每个像素值都用像素和前一个像素之间的差值代替，则可以使用LZW编码更好地压缩它们，在二维上执行这种差值计算可以帮助更多图像。

这就是LZW压缩中的PREDICTOR算法。

但是，使用这种额外的预处理后，许多图像的压缩效果并不理想，并且对于大量图像而言，压缩率实际上更差。因此，默认PREDICTOR值为1即不做这个预处理。

实验中尝试了PREDICTOR=2压缩效果提升不大。

`python3 -m gdal_merge -ot Byte -of GTiff -co COMPRESS=LZW -co PREDICTOR=2 -o F:/曹县666.tif`


### 版本4

Tiled Multi-Resolution (or Tiled Pyramidal) TIFF是简单的多页分幅 TIFF 图像, 每一种分辨率存储一个图层。 

这是一种标准的TIFF扩展，很多软件都支持。libtiff函数库也支持这种tiff的读写，因此可以在gdal中使用。

Tiled Pyramidal TIFF 图像 也可以使用 LZW这样的无损压缩或者JPEG这样的无损压缩。

实验中添加了`TILED`标签后压缩比显著提升。

`python3 -m gdal_merge -ot Byte -of GTiff -co COMPRESS=LZW -co PREDICTOR=2 -co TILED=YES -o F:/曹县666.tif`


# 3 代码中使用--压缩输出

下面是一个封装的压缩输出的例子，直接调用gdal的包函数Warp()，还支持多线程处理

```python
import gdal

def compressTifLZW(outraster, inraster):
    options=gdal.WarpOptions(
            creationOptions=["COMPRESS=LZW"], # creationOptions之压缩选项设置
            multithread=True # 多线程
            )
    gdal.Warp(outraster, inraster, options=options)

```

如果想在脚本中使用这个功能，在-co参数指定压缩即可

# 4 参考资料

https://gis.stackexchange.com/a/258215/88333

https://forum.xnview.com/viewtopic.php?p=104569&sid=839f082ea7e26ca900a7b5db75ae9ad4#p104569

https://www.fileformat.info/format/tiff/corion-lzw.htm

https://gdal.org/programs/gdal_merge.html

https://gdal.org/programs/gdalwarp.html

https://gdal.org/drivers/raster/gtiff.html
