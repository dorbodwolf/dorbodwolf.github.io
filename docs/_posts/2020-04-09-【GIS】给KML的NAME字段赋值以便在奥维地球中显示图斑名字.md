
奥维互动地球的免费版本不能导入shp格式，而奥维又不支持geojson格式，因此大家习惯将Google的kml/kmz格式数据导入其中。  

要想在奥维中显示每个矢量要素（图斑）的名字，必须给KML的NAME字段赋值。  

下图展示了在qgis中将shapefile数据通过右键-导出另存为kml的字段信息，可以看到导出的kml数据除了保留原有属性表字段外，还增加了一些字段，最前面的字段是Name，这个字段决定了在奥维互动🌍中图斑显示的名称，这个字段默认为空。我们将tbbh字段的值赋给这个字段最简单的方法是使用字段计算器，但是试了几个windows和macos下的qgis3版本后发现无法保存字段编辑结果。最后解决办法是下载qgis的KML Tools插件来对KML图层做一处理后再导出。qgis中搜索在线插件并添加插件的方式这里不叙述。  

![数据探查](https://gist.github.com/dorbodwolf/b129f17ea518ccf480a54035156632dd/raw/aa42a368f30ea5f90cb404ac741df79991e9561f/WechatIMG14.png)

安装成功kml tools插件后，可以使用【qgis主界面】——【vector】——【KML tools】——【expand html description field】工具对Name字段进行扩展如下图：  

![数据探查](https://gist.github.com/dorbodwolf/b129f17ea518ccf480a54035156632dd/raw/aa42a368f30ea5f90cb404ac741df79991e9561f/1586415781428.jpg)

扩展Name字段后生成新的图层，在这个图层的属性表上使用属性表计算器将tbbh的字段值赋值给Name字段，保存编辑导出数据即可。这样奥维地球就可以查看每个图斑的图斑号。  

![数据探查](https://gist.github.com/dorbodwolf/b129f17ea518ccf480a54035156632dd/raw/aa42a368f30ea5f90cb404ac741df79991e9561f/1586416001590.jpg)

我们使用的插件来自美国国家安全局，感兴趣可以看看kmltools插件的代码，以便自己可以做一些定制：https://github.com/NationalSecurityAgency/qgis-kmltools-plugin  
