# 1 服务器上安装docker
## 1.1 ssh安全连接服务器
## 1.2 在服务器安装docker
## 1.3 测试docker hello-word例子验证安装
输出以下消息说明docker安装成功  

Hello from Docker!  
This message shows that your installation appears to be working correctly.  

To generate this message, Docker took the following steps:  
 1. The Docker client contacted the Docker daemon.  
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.(amd64)  
 3. The Docker daemon created a new container from that image which runs the executable that produces the output you are currently reading.  
 4. The Docker daemon streamed that output to the Docker client, which sent it to your terminal.  

Docker使用客户端-服务器架构。Docker 客户端与Docker 守护进程进行对话，该守护进程完成了构建，运行和分发Docker容器的繁重工作。Docker客户端和守护程序可以 在同一系统上运行，也可以将Docker客户端连接到远程Docker守护程序。Docker客户端和守护程序在UNIX套接字或网络接口上使用REST API进行通信。  

# ２ ArcGIS Server站点架构
##  2.1 ArcGIS Server站点组件构成
Web 服务器 - 托管 Web 应用程序，并为 ArcGIS Server 提供可选的安全和负载平衡优势。  
Web Adaptor - 将 ArcGIS Server 与企业级 Web 服务器相集成，从而将收到的请求发送给多台 GIS 服务器计算机。  
GIS 服务器 - 用于处理发布到 GIS Web 服务的请求。GIS 服务器可绘制地图、运行工具、提供影像、同步数据库、投影几何、搜索数据以及执行 ArcGIS 所提供的其他众多操作。  
## 2.2 ArcGIS Server插件式架构
您可能会发现有必要在 ArcGIS Server 站点中配置多个 GIS 服务器，以防止某个 GIS 服务器不可用时出现宕机。当某个 GIS 服务器转为离线时（无论是否经过计划），Web Adaptor 仍可以继续将收到的请求分发到站点中的其他 GIS 服务器上。此外，在添加和移除 GIS 服务器时其他 GIS 服务器都可以检测到，从而创建一种在云环境下运转良好的插件式架构。  
## 2.3 由 GIS 服务器启动的进程
您可以在任何处于启动状态并参与到站点中的 GIS 服务器计算机上看到下列操作系统进程。  
三个 java 进程;  
每个运行中的服务实例均对应一个 arcsoc 进程。例外：地理处理服务每个运行中的实例都对应两个 arcsoc 进程;  
一个 rmid 进程;  
一个 xvfb 进程;  
一个 wineserver 进程;  
一个 explorer.exe 进程;  

# ３ 在docker下部署arcgis server
## 3.1 下载arcgis server安装包和认证文件
## 3.2 上传下载的文件到服务器
## 3.3 在服务器下编写dockerfile用于在docker下部署arcgis server
```
FROM centos:6

MAINTAINER xzdbd <xzdbd@sina.com>

COPY ./* /tmp/

RUN yum install -y net-tools && \
    yum install -y fontconfig && \
    yum install -y freetype && \
    yum install -y gettext && \
    yum install -y libXfont && \
    yum install -y mesa-libGL && \
    yum install -y mesa-libGLU && \
    yum install -y Xvfb && \
    /usr/sbin/useradd --create-home --home-dir /usr/local/arcgis --shell /bin/bash arcgis

USER arcgis

ENV HOME /usr/local/arcgis

RUN tar xvzf /tmp/ArcGIS_for_Server_Linux_103_142158.tar.gz -C /tmp/ && \
	/tmp/ArcGISServer/Setup -m silent -l yes -a /tmp/Adv_Ent_Svr_103.ecp

EXPOSE 1098 4000 4001 4002 4003 4004 6006 6080 6099 6443	

USER root

RUN rm /tmp/ArcGIS_for_Server_Linux_103_142158.tar.gz && \
	rm -rf /tmp/ArcGISServer

CMD /bin/bash	
```
## 3.4 创建docker 镜像
`docker build -f dockerfile .  `
## 3.5 运行一个容器
`docker run -it -v /folder:/folder -p 6080:6080 【image-id】    `  
这里的-p参数是将容器的端口发布到宿主机    
-v参数是与宿主机的共享文件夹，用于在发布影像服务前拷贝影像使用,这样可以避免在发布的时候拷贝数据  
第一次run以后，之后只需要start和stop容器来开启和关闭即可　　
通过`docker start [container-id]`之后可能未进入终端，通过`docker exec -it [container-id] /bin/bash`命令进入即可
### 启动和诊断服务
运行容器后进入虚拟环境系统中，开启和关闭arcgis服务、诊断服务运行、进行必要的配置文件管理  
诊断服务在安装目录下运行：`./tools/serverdiag/serverdiag`  
## 3.6 访问位于docker下的arcgis服务
### 通过manager访问
在宿主机或者任何内网机器通过内网IP（ http://domain:6080/arcgis/manager ）来访问服务器管理程序，进行服务发布和管理
### 通过desktop访问
arccatlog里面访问

# 4 服务发布
## 4.1 发布服务注意事项
### （1）管理器发布服务
管理器只允许将服务定义 (.sd) 文件发布到服务器。如果要发布其他类型的 GIS 资源，请使用 ArcGIS for Desktop。有关完整的说明，请参阅如何发布服务。
### （2）发布时复制数据
默认情况下，ArcGIS Server 允许发布者在发布时打包服务源数据并将其复制到服务器。如果您担心服务器中积累过多数据，或希望发布者引用已注册数据库和文件夹中的数据，则可以阻止数据复制。在 ArcGIS Server Manager 中配置此设置。
请牢记禁用数据复制后，发布者将需要将其数据注册到 ArcGIS Server 站点后再进行发布。Esri 建议将一组经认可的源位置注册到 ArcGIS Server 站点，并将这些位置传达给发布者。另请注意，如果禁用数据复制，则进行发布时要素服务数据将不会被复制到管理数据库。有关详细信息，请参阅关于将您的数据注册到 ArcGIS Server。
### （3）关于影像数据存放位置
发布影像服务时，会将服务定义和所有数据都转移到服务器上。相对于在服务器上移动和复制数据，建议您采用以下任一做法：  
·确保数据位于一个已注册到服务器中的共享驱动器上。例如，如果要发布一个镶嵌数据集，请利用这一共享位置上的数据在共享位置中创建镶嵌数据集。  
·确保在服务器上复制数据。例如，镶嵌数据集中所使用的数据在服务器上注册位置中所处的文件夹结构位置与在本地计算机上的文件夹结构位置相同。  
### （4）准备影像服务
还需要确保服务器可访问数据；否则，在发布影像服务时，数据将被转移到服务器上。建议将数据位置注册到上面提到的服务器，以避免复制数据或为较大的数据集合制作副本。  
### （5）影像服务形式
使用 ArcGIS Server 发布影像服务与发布所有其他类型的服务相似。默认情况下，始终使用影像服务功能发布影像服务，此外，还可以选择 WMS 功能和 WCS 功能。用户可以连接到这些服务，就像连接到任何其他已发布的 ArcGIS Server 服务一样。  
### (6) 特别注意
When you publish an image service, the service definition and all the data will be moved onto the server. This can be time consuming since most raster data and mosaic datasets can be very large. Unless you are publishing a small amount of data, it is recommended that you do one of the following:  
Ensure that the data is on a shared drive registered with the server. For example, if you will be publishing a mosaic dataset, create it in this shared location with data from the shared location.  
Ensure that the data is duplicated (replicated) on the server. For example, the data you use in the mosaic dataset exists in the same folder structure location in a registered location on the server, just as it does on your local machine.  
## 4.2 发布影像服务的数据存储组织方案
### (1)所有数据在一个共享位置
这也许是最佳的数据组织结构。这种情形下，所有东西都在同一个地方存放，并且在本地和服务器都可以访问到这个位置。您需要在服务器上注册该位置，并在“ 目录”窗口（或ArcCatalog）中连接到该位置，以共享来自该位置的数据作为图像服务。由于没有数据移动，这也是一种快速的发布方式。
### （2）复制所有数据
这种情况下，数据存储在两个位置，一个由服务器访问，另一个在Catalog中连接。当server在云端或者在linux系统下通常选择这种方式。这种情况下要确保本地的数据和服务器可访问的备份要始终保持一致，包括镶嵌数据集的内部文件路径也要一致。  
发布之前，确保将本地和服务器位置注册为重复位置，并且确保数据已经复制且路径正确。这样服务器就知道位置已经复制，它将不会移动任何数据，这就和场景1一致，发布也会很快。
### （3）没有注册的数据位置
这种情况下在发布时候直接复制数据到服务器，对于GB级别的数据发布会效率很低，因为打包和移动数据会很耗时间。如果您无权访问服务器所使用的位置或者发布的数据集小则可以使用这种方式
### （4）只有源数据位于注册位置
针对镶嵌数据集的发布。在此情景中，源数据位置与镶嵌数据集位置不同。此源数据位置可以是共享的或重复的。
# 5 Cache services
## 5.1 Map service caches
您可以选择在发布服务时立即创建切片（适用于小型缓存），也可以选择在发布后自行构建缓存（适用于要在地理上限制大规模构建的缓存量的大型缓存）。  
## 5.2 Image service caches
影像服务缓存可改善客户端应用程序中影像服务的性能。对影像服务进行缓存时，服务器会在不同级别上预先生成切片，在这种情况下，获取这些切片的速度要比每次从 ArcGIS Server 发出请求时处理镶嵌数据集或栅格数据集的输入数据的速度更快。影像服务缓存的一个重要方面是：它不提供动态处理的影像，而是先对影像进行预处理来创建缓存切片，然后提供这些缓存切片。  
对影像服务进行缓存时，您最终会得到一个具有双重用途的影像服务，并且可根据其用途来进行访问。一种用途是以切片服务形式提供对影像的最快访问。另一种用途是提供对数据的访问，以用于查询、下载、访问各个项并在处理和分析中使用。  
### 5.2.1 怎样创建缓存？
缓存不会自动进行。首先，您必须将一个镶嵌数据集或栅格数据集共享为影像服务。接下来，您需要设置一些缓存属性。然后，您就可以开始创建缓存。  
缓存影像服务时，影像服务会按多个预定义的比例级别或像素大小来生成一组影像切片，类似于地图服务的缓存过程。这样用户可快速进行放大和缩小，但只可按匹配的比例进行。  
如果数据经常变化（如经常更新），则可使用缓存工具来定期更新缓存。您甚至可以将更新设置为自动进行。  
#### 切片方案-Tiling scheme
针对缓存创建所选择的比例级别和所设置的属性都属于切片方案。切片方案应与可能要与其进行集成的其他图层保持一致。例如，您可以选择使用 ArcGIS Online、Google 地图和 Bing 地图等熟知的切片方案，以便可以将您的缓存内容轻松地叠加在这些在线制图服务上，您也可以自行创建在自己的 Web 应用程序内保持一致的切片方案。每个缓存都有一个切片方案文件可在创建新缓存时直接导入，以确保所有缓存都使用相同的切片大小和比例。  
如果您的切片方案与应用程序中其他图层使用的切片方案不符，则可能无法看见缓存的图层。这是因为与 ArcMap 不同，Web 客户端通常无法重采样您的数据以在其他级别上显示这些数据。  
#### 切片的限制
缓存在具有诸多优点的同时也会产生一些开销。创建缓存切片需要时间和服务器开销，同时还需要使用硬件来存储这些切片。如果出现要编辑源数据（如镶嵌数据集）这样的情况，您还需要进行缓存更新。如果您的应用程序提供以大比例显示的较大区域的影像，您可能会发现构建并维护缓存所需的时间和存储空间超过了它的性能优势。 
##### 按需缓存
按需缓存可以解决上面所说时间和服务器开销
### 5.2.2  创建影像服务缓存
* 选择切片方案：在发布服务时候提供切片方案，如果为了和在线资源兼容，最好利用其缓存方案  
* 选择是否立即进行切片：选择发布时切片或者发布后切片都可以  
* 如果缓存较大，建议在缓存最大比例时最好只对那些最可能访问的所选感兴趣区域手动构建缓存。如果缓存较小，在发布时自动构建整个缓存则会更加容易。  
* 如果选择自动构建缓存，将在此时开始构建。通过在 ArcMap 中查看地理处理结果 窗口，您可检查构建进度。  
* 如果选择手动构建缓存，则在目录 窗口中右键单击服务，然后单击管理缓存 > 管理切片。然后，将显示管理地图服务器缓存切片工具，此工具可根据所选的比例和感兴趣区构建缓存切片。  
#### 高级设置
包括比例等级、缓存目录、发布时缓存的感兴趣区域、切片格式及压缩比例以及**按需创建切片**  
##### 其他高级设置
在缓存－高级设置－高级中打开对话框进行设置，这里面包括是否允许客户端导出切片，如果选择允许的话，要明白这对服务器性能的影响以及超出客户端机器负荷的风险。  

# 6 日常维护(塔式工作站登录操作) 
(1)登录服务器   
`ssh hncg@192.168.18.232` 输入密码登入   
(2)查看docker容器运行状况(root下)    
`docker ps`  查看当前运行的容器   
`docker ps -a`  查看所有容器，包括停止的。看docker运行情况     
当下无运行的容器,ID为`27fd907cbf1a`的容器是我们要找的容器  
```
root@hncg-PowerEdge-T630:/home/hncg# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
root@hncg-PowerEdge-T630:/home/hncg# docker ps -a
CONTAINER ID        IMAGE                  COMMAND                  CREATED             STATUS                      PORTS               NAMES
fe58e8c10575        nvidia/cuda:9.0-base   "nvidia-smi"             3 months ago        Created                                         nervous_johnson
27fd907cbf1a        499f1f49fadd           "/bin/sh -c /bin/bash"   4 months ago        Exited (137) 4 weeks ago                        admiring_keldysh
02b384ad0e9c        499f1f49fadd           "/bin/sh -c /bin/bash"   4 months ago        Exited (137) 4 months ago                       trusting_khorana
191140aeb23d        hello-world            "/hello"                 4 months ago        Exited (0) 4 months ago                         mystifying_faraday
```
(3)使容器运行    
`docker start 27fd907cbf1a`  
(4)进入容器检查arcgis server运行状况  
进入容器虚拟机 `docker exec -it 27fd907cbf1a /bin/bash`  
切换到server安装目录 `cd usr/local/arcgis/server/`  
切换用户为arcgis `su arcgis`  
运行诊断工具 `./tools/serverdiag/serverdiag`  
发现arcgis核心服务报了警告,怀疑server没有启动  
```
[root@27fd907cbf1a server]# ./tools/serverdiag/serverdiag 
========================================================================
                   ArcGIS for Server Diagnostic Tool
                                  10.3
                         Hostname: 27fd907cbf1a
========================================================================
This script must be run by the installation owner (arcgis).
[root@27fd907cbf1a server]# su arcgis
[arcgis@27fd907cbf1a server]$ ./tools/serverdiag/serverdiag 
========================================================================
                   ArcGIS for Server Diagnostic Tool
                                  10.3
                         Hostname: 27fd907cbf1a
========================================================================

 DIAG000: Check for installation as root                       [PASSED]
 DIAG001: Check for 64-bit architecture                        [PASSED]
 DIAG002: Check OS version                                     [PASSED]
 DIAG003: Check hostname for invalid characters                [PASSED]
 DIAG004: Check installed packages                             [PASSED]
 DIAG005: Check system limits                                  [PASSED]
 DIAG006: Check OS patches                                     [PASSED]
 DIAG008: Check HTTP port                                      [PASSED]
 DIAG009: Check HTTPS port                                     [PASSED]
 DIAG010: Check Xvfb ports                                     [PASSED]
 DIAG020: Check hostname IP address mismatches                 [PASSED]
 DIAG026: Check processes for ArcGIS core services             [WARNING]

------------------------------------------------------------------------
There were 0 failure(s) and 1 warning(s) found:

```
尝试利用脚本启动server `bash startserver.sh`显示OK  
```
[arcgis@27fd907cbf1a server]$ bash startserver.sh 
Attempting to start ArcGIS Server... 
[  OK  ]
```
再次运行诊断工具 ` ./tools/serverdiag/serverdiag `发现异常排除  
```
[arcgis@27fd907cbf1a server]$ ./tools/serverdiag/serverdiag 
========================================================================
                   ArcGIS for Server Diagnostic Tool
                                  10.3
                         Hostname: 27fd907cbf1a
========================================================================

 DIAG000: Check for installation as root                       [PASSED]
 DIAG001: Check for 64-bit architecture                        [PASSED]
 DIAG002: Check OS version                                     [PASSED]
 DIAG003: Check hostname for invalid characters                [PASSED]
 DIAG004: Check installed packages                             [PASSED]
 DIAG005: Check system limits                                  [PASSED]
 DIAG006: Check OS patches                                     [PASSED]
 DIAG008: Check HTTP port                                      [PASSED]
 DIAG009: Check HTTPS port                                     [PASSED]
 DIAG010: Check Xvfb ports                                     [PASSED]
 DIAG020: Check hostname IP address mismatches                 [PASSED]
 DIAG026: Check processes for ArcGIS core services             [PASSED]

------------------------------------------------------------------------
There were 0 failure(s) and 0 warning(s) found:
```
(5)查看管理员界面确定运行情况  
<http://192.168.18.232:6080/arcgis/manager/>  
