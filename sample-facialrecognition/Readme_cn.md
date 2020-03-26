中文|[English](Readme.md)

# 人脸识别<a name="ZH-CN_TOPIC_0203223340"></a>

开�者�以将本Application部署至Atlas 200 DK上实现人脸注册�并通过摄�头对视频中的人脸信�进行预测，与已注册的人脸进行比对，预测出最�能的用户。

当�分支中的应用适�**1.32.0.0�以上**版本的[DDK&RunTime](https://ascend.huawei.com/resources)。

## ���件<a name="section137245294533"></a>

部署此Sample�，需�准备好以下环境：

-   已完�Mind Studio的安装。
-   已完�Atlas 200 DK开�者�与Mind Studio的连接，交�编译器的安装，SD�的制作�基本信�的�置等。

## 软件准备<a name="section8534138124114"></a>

�行此Sample�，需�按照此章节获���包，并进行相关的环境�置。

1.  <a name="li953280133816"></a>获���包。
    1.  下载压缩包方�获�。

        将[https://github.com/Atlas200dk/sample-facialrecognition/tree/1-3x-0-0/](https://github.com/Atlas200dk/sample-facialrecognition/tree/1-3x-0-0/)仓中的代�以Mind Studio安装用户下载至Mind Studio所在Ubuntu�务器的任�目录，例如代�存放路径为：$HOME/AscendProjects/sample-facialrecognition。

    2.  命令行使用git命令方�获�。

        在命令行中：$HOME/AscendProjects目录下执行以下命令下载代�。

        **git clone https://github.com/Atlas200dk/sample-facialrecognition.git --branch 1-3x-0-0**

2.  <a name="li99811487013"></a>获�此应用中所需�的原始网络模型。

    �考[表1](#table97791025517)获�此应用中所用到的原始网络模型�其对应的��文件，并将其存放到Mind Studio所在Ubuntu�务器的任�目录，这两个文件必须存放到�一个目录下。例如：$HOME/models/facialrecognition。

    **表 1**  Facial Recognition中使用模型

    <a name="table97791025517"></a>
    <table><thead align="left"><tr id="row48791253115"><th class="cellrowborder" valign="top" width="13.309999999999999%" id="mcps1.2.4.1.1"><p id="p187902511114"><a name="p187902511114"></a><a name="p187902511114"></a>模型�称</p>
    </th>
    <th class="cellrowborder" valign="top" width="12.04%" id="mcps1.2.4.1.2"><p id="p148791259118"><a name="p148791259118"></a><a name="p148791259118"></a>模型说明</p>
    </th>
    <th class="cellrowborder" valign="top" width="74.65%" id="mcps1.2.4.1.3"><p id="p987922511111"><a name="p987922511111"></a><a name="p987922511111"></a>模型下载路径</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row38791825912"><td class="cellrowborder" valign="top" width="13.309999999999999%" headers="mcps1.2.4.1.1 "><p id="p0879152519115"><a name="p0879152519115"></a><a name="p0879152519115"></a>face_detection</p>
    </td>
    <td class="cellrowborder" valign="top" width="12.04%" headers="mcps1.2.4.1.2 "><p id="p9879112516111"><a name="p9879112516111"></a><a name="p9879112516111"></a>人脸检测网络模型。</p>
    <p id="p1087912253112"><a name="p1087912253112"></a><a name="p1087912253112"></a>是基于Caffe的Resnet10-SSD300模型转��的网络模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="74.65%" headers="mcps1.2.4.1.3 "><p id="p188801525813"><a name="p188801525813"></a><a name="p188801525813"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/object_detect/face_detection" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/object_detect/face_detection</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    <tr id="row11880162511114"><td class="cellrowborder" valign="top" width="13.309999999999999%" headers="mcps1.2.4.1.1 "><p id="p1388012251117"><a name="p1388012251117"></a><a name="p1388012251117"></a>vanillacnn</p>
    </td>
    <td class="cellrowborder" valign="top" width="12.04%" headers="mcps1.2.4.1.2 "><p id="p1988018251110"><a name="p1988018251110"></a><a name="p1988018251110"></a>人脸特�点标记网络模型。</p>
    <p id="p588013251514"><a name="p588013251514"></a><a name="p588013251514"></a>是基于Caffe的VanillaCNN模型转��的网络模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="74.65%" headers="mcps1.2.4.1.3 "><p id="p28801025319"><a name="p28801025319"></a><a name="p28801025319"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/vanillacnn" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/vanillacnn</a><span>目录中</span>README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    <tr id="row988092511120"><td class="cellrowborder" valign="top" width="13.309999999999999%" headers="mcps1.2.4.1.1 "><p id="p108806251513"><a name="p108806251513"></a><a name="p108806251513"></a>sphereface</p>
    </td>
    <td class="cellrowborder" valign="top" width="12.04%" headers="mcps1.2.4.1.2 "><p id="p68802251019"><a name="p68802251019"></a><a name="p68802251019"></a>特���获�网络模型。</p>
    <p id="p148801125512"><a name="p148801125512"></a><a name="p148801125512"></a>是基于Caffe的SphereFace模型转��的网络模型</p>
    </td>
    <td class="cellrowborder" valign="top" width="74.65%" headers="mcps1.2.4.1.3 "><p id="p128806251116"><a name="p128806251116"></a><a name="p128806251116"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/sphereface" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/sphereface</a><span>目录中</span>README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    </tbody>
    </table>

3.  以Mind Studio安装用户登录Mind Studio所在Ubuntu�务器，确定当�使用的DDK版本�并设置环境��DDK\_HOME，tools\_version，LD\_LIBRARY\_PATH。
    1.  <a name="zh-cn_topic_0203223294_li61417158198"></a>查询当�使用的DDK版本�。

        �通过Mind Studio工具查询，也�以通过DDK软件包进行获�。

        -   使用Mind Studio工具查询。

            在Mind Studio工程界��次选择“File \> Settings \> System Settings \> Ascend DDK“，弹出如[图 DDK版本�查询](#zh-cn_topic_0203223294_fig17553193319118)所示界�。

            **图 1**  DDK版本�查询<a name="zh-cn_topic_0203223294_fig17553193319118"></a>  
            ![](figures/DDK版本�查询.png "DDK版本�查询")

            其中显示的**DDK Version**就是当�使用的DDK版本�，如**1.31.T15.B150**。

        -   通过DDK软件包进行查询。

            通过安装的DDK的包�获�DDK的版本�。

            DDK包的包�格�为：**Ascend\_DDK-\{software version\}-\{interface version\}-x86\_64.ubuntu16.04.tar.gz**

            其中**software version**就是DDK的软件版本�。

            例如：

            DDK包的包�为Ascend\_DDK-1.31.T15.B150-1.1.1-x86\_64.ubuntu16.04.tar.gz，则此DDK的版本�为1.31.T15.B150。

    2.  设置环境��。

        **vim \~/.bashrc**

        执行如下命令在最�一行添加DDK\_HOME�LD\_LIBRARY\_PATH的环境��。

        **export tools\_version=_1.31.X.X_**

        **export DDK\_HOME=\\$HOME/.mindstudio/huawei/ddk/\\$tools\_version/ddk**

        **export LD\_LIBRARY\_PATH=$DDK\_HOME/lib/x86\_64-linux-gcc5.4**

        >![](public_sys-resources/icon-note.gif) **说明：**   
        >-   **_1.31.X.X_**是[a](#zh-cn_topic_0203223294_li61417158198)中查询到的DDK版本�，需�根�查询结果对应填写，如**1.31.T15.B150**  
        >-   如果此环境��已�添加，则此步骤�跳过。  

        输入:wq!�存退出。

        执行如下命令使环境��生效。

        **source \~/.bashrc**

4.  将原始网络模型转�为适�昇腾AI处�器的模型，模型转�有Mind Studio工具转�和命令行转�两�方�。
    -   通过Mind Studio工具进行模型转�。
        1.  在Mind Studio�作界�的顶部���中选择**Tools \> Model Convert**进入模型转�界�。
        2.  在弹出的**Model** **Conversion**�作界�中，进行模型转��置。
            -   Model File选择[步骤2](#li99811487013)中下载的模型文件，此时会自动匹�到��文件并填写在Weight File中。
            -   Model Name填写为[表1](#table97791025517)中对应的**模型�称**。
            -   VanillaCNNModel模型转�时�默认值�置如下：

                -   Nodes�置中的“Input Node:data“中的N值修改为**4**，此�数需�与“graph\_template.config“中的对应模型的“batch\_size“的值��一致，C�H�W��默认值，如[图2](#fig5158834193915)。
                -   AIPP�置中的“Image Preprocess“请设置为**off**。

                **图 2**  VanillaCNNModel模型转�时Nodes�置<a name="fig5158834193915"></a>  
                

                ![](figures/model_facial_1.png)

            -   SpherefaceModel模型转��默认值�置如下：

                -   Nodes�置中的“Input Node:data“中的N:8表示人脸识别程�，�次处�8张人脸，此�数需�与“graph\_template.config�中的对应模型的“batch\_size“的值��一致。
                -   AIPP�置中的“Input Image Format“：输入图片的格�，此处选择RGB888\_U8。
                -   AIPP�置中的“Input Image Size“：因为输入图片格�为RGB8888\_U8，此处�需��128\*16对�，直接使用模型�求的宽和高��，�96与112。
                -   AIPP�置中的“**Model Image Format**�：模型图片的格�，此处选择BGR888\_U8。
                -   AIPP�置中的“**Mean Less**“：此模型训练使用的图片的�值，�从此模型的sphereface\_model.prototxt文件中获�。
                -   AIPP�置中的“**Multiplying Factor**�：此模型训练使用的图片的乘系数，�从此模型的sphereface\_model.prototxt文件中获�，�scale的值。

                **图 3**  SpherefaceModel模型转化时Nodes�置<a name="fig188415461909"></a>  
                

                ![](figures/model_facial_3.png)

                **图 4**  SpherefaceModel模型转化时AIPP�置<a name="fig159362210546"></a>  
                

                ![](figures/model_facial_4.png)

            -   face\_detection模型中**Input Image Size**需�分别修改为384,304， 此处需��128\*16对�。**Model Image Format**需�选择为BGR888\_U8。其他使用默认值。

                **图 5**  face\_detection模型转�时�默认�置<a name="fig525743174114"></a>  
                

                ![](figures/model_facial_5.png)

        3.  �击OK开始模型转�。

            face\_detection模型在转�的时候，会出现如[图6](#fig19683520164211)所示错误。

            **图 6**  模型转�错误<a name="fig19683520164211"></a>  
            

            ![](figures/model_facial_conversionfailed.png)

            此时在**DetectionOutput**层的**Suggestion**中选择**SSDDetectionOutput**，并点击**Retry**。

            模型转��功�，�缀为.om的离线模型存放地�为：$HOME/modelzoo/XXX/device。

            >![](public_sys-resources/icon-note.gif) **说明：**   
            >-   Mind Studio模型转�中�一步的具体�义和�数说明�以�考[Mind Studio用户手册](https://ascend.huawei.com/doc/mindstudio/)中的“模型转�“章节。  
            >-   XXX表示当�转�的模型�称，如face\_detection.om存放地�为：$HOME/modelzoo/face\_detection/device。  


    -   命令行模�下模型转�。
        1.  以Mind Studio安装用户进入存放原始模型的文件夹。

            **cd $HOME/ascend/models/facialrecognition**

        2.  使用omg工具执行以下命令进行模型转�。

            ```
            ${DDK_HOME}/uihost/bin/omg --output="./XXX" --model="./XXX.prototxt" --framework=0 --ddk_version=${tools_version} --weight="./XXX.caffemodel" --input_shape=`head -1 $HOME/AscendProjects/sample-facialrecognition/script/shape_XXX` --insert_op_conf=$HOME/AscendProjects/sample-facialrecognition/script/aipp_XXX.cfg --op_name_map=$HOME/AscendProjects/sample-facialrecognition/script/reassign_operators
            ```

            >![](public_sys-resources/icon-note.gif) **说明：**   
            >-   input\_shape�insert\_op\_conf�op\_name\_map所需�的文件都在��所在路径下的“sample-facialrecognition/script�目录下，请根�您实际的��所在路径�置这些文件路径。  
            >-   **XXX**为[表 Facial Recognition中使用模型](#table97791025517)中的模型�称，转�时请替�为实际的模型�称。  
            >-   vanillacnn模型转�时�需�insert\_op\_conf�op\_name\_map�数，sphereface模型转�时�需�op\_name\_map�数，如果没有删除�需�的�数，转�模型时会报错。  
            >-   �个�数的具体�义��考[Atlas 200 DK用户手册](https://ascend.huawei.com/doc/atlas200dk/)中的“模型转�“章节。  


5.  将转�好的模型文件（.om文件）上传到[步骤1](#li953280133816)中��所在路径的“sample-facialrecognition/script�目录下。

## 编译<a name="section147911829155918"></a>

1.  打开对应的工程。

    以Mind Studio安装用户在命令行中进入安装包解压�的“MindStudio-ubuntu/bin�目录，如：$HOME/MindStudio-ubuntu/bin。执行如下命令�动Mind Studio

    **./MindStudio.sh**

    �动�功�，打开**sample-facialrecognition**工程，如[图7](#fig28591855104218)所示。

    **图 7**  打开sample-facialrecognition工程<a name="fig28591855104218"></a>  
    ![](figures/打开sample-facialrecognition工程.png "打开sample-facialrecognition工程")

2.  在**src/param\_configure.conf**文件中�置相关工程信�。

    如[图8](#fig1338571124515)所示。

    **图 8**  �置文件路径<a name="fig1338571124515"></a>  
    

    ![](figures/facial_open_src.png)

    该�置文件内容如下：

    ```
    remote_host=
    data_source=
    presenter_view_app_name=
    ```

    需�手动添加�数�置：

    -   remote\_host：�置为Atlas 200 DK开�者�的IP地�。
    -   data\_source: �置为摄�头所属Channel，�值为Channel-1或者Channel-2，查询摄�头所属Channel的方法请�考[Atlas 200 DK用户手册](https://ascend.huawei.com/doc/Atlas200DK/)中的“如何查看摄�头所属Channel�。
    -   presenter\_view\_app\_name: 用户自定义的在PresenterServer界�展示的View Name，此View Name需�在Presenter Server展示界�唯一，�能为大�写字��数字�“\_�的组�，�数3\~20。

    �置示例：

    ```
    remote_host=192.168.1.2
    data_source=Channel-1
    presenter_view_app_name=video
    ```

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   三个�数必须全部填写，�则无法通过build。  
    >-   注��数填写时�需�使用“�符�。  

3.  执行deploy脚本， 进行�置�数调整�第三方库下载编译 打开Mind Studio工具的Terminal，此时默认在代�主目录下，执行如下命令在��指执行deploy脚本，进行环境部署。如[图 执行deploy脚本](#fig16909182592016)所示。

    **图 9**  执行deploy脚本<a name="fig16909182592016"></a>  
    ![](figures/执行deploy脚本-0.png "执行deploy脚本-0")

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   首次deploy时，没有部署第三方库时会自动下载并编译，耗时�能比较久，请�心等待。�续��新编译时，�会��下载编译，部署如上图所示。  
    >-   deploy时，需�选择与开��通信的主机侧ip，一般为虚拟网��置的ip。如果此ip和开��ip属于�网段，则会自动选择并部署。如果��网段，则需�手动输入与开��通信的主机侧ip�能完�deploy。  

4.  开始编译，打开Mind Studio工具，在工具�中点击**Build \> Build \> Build-Configuration**。如[图10](#fig1629455494718)所示，会在目录下生�build和run文件夹。

    **图 10**  编译�作�生�文件<a name="fig1629455494718"></a>  
    ![](figures/编译�作�生�文件.png "编译�作�生�文件")

    >![](public_sys-resources/icon-notice.gif) **须知：**   
    >首次编译工程时，**Build \> Build**为�色��点击状�。需�点击**Build \> Edit Build Configuration**，�置编译�数��进行编译。  

5.  <a name="li1364788188"></a>�动Presenter Server

    打开Mind Studio工具的Terminal，在应用代�存放路径下，执行如下命令在���动_facialrecognition_应用的Presenter Server主程�。如[图11](#fig156364995016)所示。

    **bash run\_present\_server.sh**

    **图 11**  �动PresenterServer<a name="fig156364995016"></a>  
    

    ![](figures/facial_run_1.png)

    -   当�示“Please choose one to show the presenter in browser\(default: 127.0.0.1\):“时，请输入在�览器中访问Presenter Server�务所使用的IP地�（一般为访问Mind Studio的IP地�）。
    -   当�示“Please input a absolute path to storage facial recognition data:“时，请输入Mind Studio中存储人脸注册数��解�数�，此路径Mind Studio用户需�有读写��，如果此路径�存在，脚本会自动创建。

    如[图12](#fig157571218181018)所示，请在“Current environment valid ip list“中选择通过�览器访问Presenter Server�务使用的IP地�，并输入存储人脸识别解�数�的路径。

    **图 12**  工程部署示�图<a name="fig157571218181018"></a>  
    

    ![](figures/facial_run_2.png)

    如[图13](#fig123741843161320)所示，表示presenter\_server的�务�动�功。

    **图 13**  Presenter Server进程�动<a name="fig123741843161320"></a>  
    

    ![](figures/facial_runOK.png)

    使用上图�示的URL登录Presenter Server（仅支�Chrome�览器），IP地�为[图12](#fig157571218181018)中输入的IP地�，端��默为7009，如下图所示，表示Presenter Server�动�功。

    **图 14**  主页显示<a name="fig98461795813"></a>  
    ![](figures/主页显示-1.png "主页显示-1")

    Presenter Server�Mind Studio与Atlas 200 DK之间通信使用的IP地�示例如下图所示：

    **图 15**  IP地�示例<a name="fig1627210116351"></a>  
    ![](figures/IP地�示例-2.png "IP地�示例-2")

    其中：

    -   Atlas 200 DK开�者�使用的IP地�为192.168.1.2（USB方�连接）。
    -   Presenter Server与Atlas 200 DK通信的IP地�为UI Host�务器中与Atlas 200 DK在�一网段的IP地�，例如：192.168.1.223。
    -   通过�览器访问Presenter Server的IP地�本示例为：10.10.0.1，由于Presenter Server与Mind Studio部署在�一�务器，此IP地�也为通过�览器访问Mind Studio的IP。


## �行<a name="section1676879104"></a>

1.  �行人脸识别应用程�。

    在Mind Studio工具的工具�中找到Run按钮，点击**Run \> Run 'sample-facialrecognition'**，如[图16](#fig182957429910)所示，�执行程�已�在开�者�执行。

    **图 16**  程�已执行示�图<a name="fig182957429910"></a>  
    

    ![](figures/facial_run3.png)

2.  使用�动Presenter Server�务时�示的URL登录 Presenter Server 网站，详细��考[�动Presenter Server](#li1364788188)  ,仅支�Chrome�览器。

    Presenter Server展示界�如[图17](#fig1189774382115)所示。

    **图 17**  Presenter Server界�<a name="fig1189774382115"></a>  
    ![](figures/Presenter-Server界�-3.png "Presenter-Server界�-3")

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   Facial Recognition的Presenter Server最多支�2路Channel�时显示，�个  _presenter\_view\_app\_name_  对应一路Channel。  
    >-   由于硬件的�制，�一路支�的最大帧率是20fps，��于网络带宽的影�，帧率会自动适�较低的帧率进行显示。  

3.  进行人脸注册。
    1.  点击“Face Library“页签，在界�中输入“Username“。

        **图 18**  人脸注册界�<a name="fig12445181112163"></a>  
        ![](figures/人脸注册界�.png "人脸注册界�")

    2.  �击“Browse“按钮，上传人脸图�，人脸图��剪时尽�按照“Example Photo“的比例设置。

    1.  点击Submit按钮上传若上传失败，�以更改�剪比例。

4.  人脸识别以�比对。

    进入“App List“页签，在界�中点击对应的“App Name“，例如  _video_  ，若有人脸出现在摄�头中，且与已注册人脸匹�一致，则会出现对应人员姓��相似度的标注。


## �续处�<a name="section1092612277429"></a>

-   **�止人脸识别应用**

    Facial Recognition应用执行�会处于�续�行状�，若��止Facial Recognition应用程�，�执行如下�作。

    �击[图19 �止Facial Recognition应用](#fig12461162791610)所示的�止按钮�止Facial Recognition应用程�。

    **图 19**  �止Facial Recognition应用<a name="fig12461162791610"></a>  
    

    ![](figures/facial_stopping.png)

    如[图20](#fig5786125319165)所示应用程�已�止�行

    **图 20**  Facial Recognition应用已�止<a name="fig5786125319165"></a>  
    

    ![](figures/facial_stopped.png)

-   **�止Presenter Server�务**

    Presenter Server�务�动�会一直处于�行状�，若想�止人脸识别应用对应的Presenter Server�务，�执行如下�作。

    以Mind Studio安装用户在Mind Studio所在�务器中执行如下命令查看人脸识别应用对应的Presenter Server�务的进程。

    **ps -ef | grep presenter | grep facial\_recognition**

    ```
    ascend@ascend-HP-ProDesk-600-G4-PCI-MT:~/sample-facialrecognition$ ps -ef | grep presenter | grep facial_recognition
    ascend 22294 20313 22 14:45 pts/24?? 00:00:01 python3 presenterserver/presenter_server.py --app facial_recognition
    ```

    如上所示  _22294_  �为人脸识别应用对应的Presenter Server�务的进程ID。

    若想�止此�务，执行如下命令：

    **kill -9** _22294_


