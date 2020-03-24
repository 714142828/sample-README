中文|[English](Readme.md)

# 语义分割网络应用（Python）<a name="ZH-CN_TOPIC_0228757085"></a>

本Application支��行在Atlas 200 DK上，实现了erfnet网络的推�功能并输出带有推�结果的图片。

当�分支中的应用适�**1.3.0.0**与**1.32.0.0�以上**版本的[DDK&RunTime](https://ascend.huawei.com/resources)。

## ���件<a name="section137245294533"></a>

部署此Sample�，需�准备好以下环境：

-   已完�Mind Studio的安装。

-   已完�Atlas 200 DK开�者�与Mind Studio的连接，SD�的制作�编译环境的�置等。
-   由于需��置开���网，默认设置为USB连接，开��地�为192.168.1.2

## 软件准备<a name="section8534138124114"></a>

�行此应用�，需�按照此章节进行相关的环境�置并获���包。

1.  <a name="li953280133816"></a>获���包。
    1.  下载压缩包方�获�。

        将[https://github.com/Atlas200dk/sample-segmentation-python](https://github.com/Atlas200dk/sample-classification-python)仓中的代�以Mind Studio安装用户下载至Mind Studio所在Ubuntu�务器的任�目录，例如代�存放路径为：$HOME/sample-segmentation-python。

    2.  命令行使用git命令方�获�。

        在命令行中：$HOME/AscendProjects目录下执行以下命令下载代�。

        **git clone https://github.com/Atlas200dk/sample-segmentation-python.git**

2.  获�此应用中所需�的网络模型。

    �考[表 语义分割网络应用\(python\)使用模型](#table1119094515272)获�此应用中所用到的原始网络模型�其对应的��文件，并将其存放到Mind Studio所在Ubuntu�务器的任�目录，例如：$HOME/ascend/models/sample-segmentation-python。

    **表 1**  语义分割网络应用\(python\)使用模型

    <a name="table1119094515272"></a>
    <table><thead align="left"><tr id="row677354502719"><th class="cellrowborder" valign="top" width="12.15%" id="mcps1.2.4.1.1"><p id="p167731845122717"><a name="p167731845122717"></a><a name="p167731845122717"></a>模型�称</p>
    </th>
    <th class="cellrowborder" valign="top" width="17.53%" id="mcps1.2.4.1.2"><p id="p277317459276"><a name="p277317459276"></a><a name="p277317459276"></a>模型说明</p>
    </th>
    <th class="cellrowborder" valign="top" width="70.32000000000001%" id="mcps1.2.4.1.3"><p id="p9773114512270"><a name="p9773114512270"></a><a name="p9773114512270"></a>模型下载路径</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row3122314144215"><td class="cellrowborder" valign="top" width="12.15%" headers="mcps1.2.4.1.1 "><p id="p1910619166207"><a name="p1910619166207"></a><a name="p1910619166207"></a>erfnet</p>
    </td>
    <td class="cellrowborder" valign="top" width="17.53%" headers="mcps1.2.4.1.2 "><p id="p2010681612020"><a name="p2010681612020"></a><a name="p2010681612020"></a>图片语义分割推�模型。</p>
    <p id="p1710615162207"><a name="p1710615162207"></a><a name="p1710615162207"></a>是基于Caffe的erfnet模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="70.32000000000001%" headers="mcps1.2.4.1.3 "><p id="p910617162206"><a name="p910617162206"></a><a name="p910617162206"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/segmentation/erfnet" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/segmentation/erfnet</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    </tbody>
    </table>

3.  将原始网络模型转�为适�昇腾AI处�器的模型。
    1.  在Mind Studio�作界�的顶部���中选择**Tools \> Model Convert**，进入模型转�界�。
    2.  在弹出的**Model Conversion**�作界�中，Model File与Weight File分别选择[步骤1](#li953280133816)中下载的模型文件和��文件。
        -   **Model Name**填写为[表 语义分割网络应用\(python\)使用模型](#table1119094515272)中对应的**模型�称**。
        -   erfnet模型转�时中AIPP�置中的**Model Image Format**  选择BGR888\_U8，关闭MeanLess选项
        -   其他�数��默认值。

    3.  �击OK开始转�模型。

        1.1.0.0和1.3.0.0版本模型转��功�，�缀为.om的离线模型存放地�为：**$HOME/tools/che/model-zoo/my-model/xxx**。

        1.31.0.0�以上版本模型转��功�，�缀为.om的离线模型存放地�为：**$HOME/modelzoo/xxx/device/xxx.om**。

    4.  将转�好的模型文件（.om文件）上传到[步骤1](#li953280133816)中��所在路径下的“sample-segmentation-python/segmentationapp/models�目录下。


## 环境部署<a name="section218113616146"></a>

1.  应用代�拷�到开��。

    以Mind Studio安装用户进入语义分割网络应用\(python\)代�所在根目录，如：$HOME/sample-segmentation-python，执行以下命令将应用代�拷�到开��。

    **scp -r ../sample-segmentation-python/ HwHiAiUser@192.168.1.2:/home/HwHiAiUser/HIAI\_PROJECTS**

    �示password时输入开��密�，开��默认密�为**Mind@123**，如[图 应用代�拷�](#zh-cn_topic_0219036254_fig1660453512014)。

    **图 1** **应用代�拷�**<a name="zh-cn_topic_0219036254_fig1660453512014"></a>  
    

    ![](figures/zh-cn_image_0228836881.png)

    在Mind Studio所在Ubuntu�务器中，以HwHiAiUser用户SSH登录到Host侧。

    **ssh HwHiAiUser@192.168.1.2**

    切�到root用户，开��中root用户默认密�为**Mind@123**。

    **su root**

2.  �置开���网。

    请�考[https://github.com/Atlas200dk/sample-README/tree/master/DK\_NetworkConnect](https://github.com/Atlas200dk/sample-README/tree/master/DK_NetworkConnect)  ，进行开��网络连接�置。

3.  安装环境�赖。�

    请�考[https://github.com/Atlas200dk/sample-README/tree/master/DK\_Environment](https://github.com/Atlas200dk/sample-README/tree/master/DK_Environment)  ，进行环境�赖�置。


## 程��行<a name="section6245151616426"></a>

1.  切�HwHiAiUser用户，并进入语义分割网络应用代�所在目录。

    **su HwHiAiUser**

    **cd \~/HIAI\_PROJECTS/sample-segmentation-python/segmentationapp**

2.  执行应用程�。

    执行**segmentation.py**脚本会将推�结果在执行终端直接打�显示。

    命令示例如下所示：

    **python segmentation.py**

    执行�功�效果如[图 推��功示�图](#fig1863053617417)所示。

    **图 2**  推��功示�图<a name="fig1863053617417"></a>  
    

    ![](figures/zh-cn_image_0228757232.png)

3.  执行结果查看。

    执行结果�存在当�目录下的Result目录下，需�在Atlas200DK中用以下命令将结果拷�到Ubuntu�务器中查看推�结果图片。

    **scp -r username@host\_ip:/home/username/HIAI\_PROJECTS/sample-classification-python/Result \~**

    -   username：开��用户﻿�，默认为HwHiAiUser。
    -   host\_ip：开��ip，USB连接一般为192.168.1.2.网线连接时一般为192.168.0.2。

    **命令示例：**

    **scp -r HwHiAiUser@192.168.1.2:/home/HwHiAiUser/HIAI\_PROJECTS/sample-classification-python/Result \~**

    该命令会把推�结果拷�到Mindstudio安装用户的家目录中，�以直接查看。


## 相关说明<a name="section1092612277429"></a>

-   **语义分割网络应用（Python）的�程说明如下**：
    1.  从cityimage目录下读�jpeg图片。
    2.  将读�的jpeg图片调用opencv resize到1024\*512，并转��YUV420SP。
    3.  将转��的YUV420SP图片数��入Matrix进行推�。demo采用的是erfnet网络，推�结果是�个�素点的19个分类的置信度
    4.  �处�阶段，�个�素点选�最高置信度的分类，在图片上对��分类进行涂色。涂色�图片存放在Result目录下。

-   **语义分割网络应用（Python）的文件架构说明如下**：
    -   cityimage：存放输入图片
    -   segmentation.py：主程�
    -   jpegHandler.py：jpeg图片处�，如resize�色域转�等
    -   models：存放模型网络
    -   Result：存放标注�的图片


