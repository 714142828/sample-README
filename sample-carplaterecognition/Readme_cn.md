中文|[English](Readme.md)

# 车牌识别<a name="ZH-CN_TOPIC_0218873008"></a>

开�者�以将本application部署至Atlas 200DK上实现对摄�头数�的实时采集�并对视频中的车辆车牌信�进行预测的功能。�模型影�，精准度较低，如果需��高精度，�以自己训练模型替�。

当�分支中的应用适�**1.32.0.0�以上**版本的[DDK&RunTime](https://ascend.huawei.com/resources)。

## ���件<a name="section137245294533"></a>

部署此Sample�，需�准备好以下环境：

-   已完�Mind Studio的安装。
-   已完�Atlas 200 DK开�者�与Mind Studio的连接，交�编译器的安装，SD�的制作�基本信�的�置等。

## 软件准备<a name="section8534138124114"></a>

�行此Sample�，需�按照此章节获���包，并进行相关的环境�置。

1.  <a name="li953280133816"></a>获���包。
    1.  下载压缩包方�获�。

        将[https://github.com/Atlas200dk/sample-carplaterecognition/tree/1-3x-0-0/](https://github.com/Atlas200dk/sample-carplaterecognition/tree/1-3x-0-0/)仓中的代�以Mind Studio安装用户下载至Mind Studio所在Ubuntu�务器的任�目录，例如代�存放路径为：$HOME/AscendProjects/sample-carplaterecognition。

    2.  命令行使用git命令方�获�。

        在命令行中：$HOME/AscendProjects目录下执行以下命令下载代�。

        **git clone https://github.com/Atlas200dk/sample-carplaterecognition.git --branch 1-3x-0-0**

2.  <a name="li8221184418455"></a>获�此应用中所需�的原始网络模型。

    �考[表 车牌识别应用中使用的模型](#table117203103464)获�此应用中所用到的原始网络模型�其对应的��文件，并将其存放到Mind Studio所在Ubuntu�务器的任�目录，这两个文件必须存放到�一个目录下。例如：$HOME/models/carplaterecognition。

    **表 1**  车牌识别应用中使用的模型

    <a name="table117203103464"></a>
    <table><thead align="left"><tr id="row4859191074617"><th class="cellrowborder" valign="top" width="17.32173217321732%" id="mcps1.2.4.1.1"><p id="p18859111074613"><a name="p18859111074613"></a><a name="p18859111074613"></a>模型�称</p>
    </th>
    <th class="cellrowborder" valign="top" width="9.68096809680968%" id="mcps1.2.4.1.2"><p id="p17859171013469"><a name="p17859171013469"></a><a name="p17859171013469"></a>模型说明</p>
    </th>
    <th class="cellrowborder" valign="top" width="72.997299729973%" id="mcps1.2.4.1.3"><p id="p1385991094614"><a name="p1385991094614"></a><a name="p1385991094614"></a>模型下载路径</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row1985913103461"><td class="cellrowborder" valign="top" width="17.32173217321732%" headers="mcps1.2.4.1.1 "><p id="p14859151016464"><a name="p14859151016464"></a><a name="p14859151016464"></a>car_plate_detection</p>
    </td>
    <td class="cellrowborder" valign="top" width="9.68096809680968%" headers="mcps1.2.4.1.2 "><p id="p108593100461"><a name="p108593100461"></a><a name="p108593100461"></a>车牌检测网络模型。</p>
    <p id="p1785921024614"><a name="p1785921024614"></a><a name="p1785921024614"></a>基于Caffe的Mobilenet-SSD模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="72.997299729973%" headers="mcps1.2.4.1.3 "><p id="p158596106460"><a name="p158596106460"></a><a name="p158596106460"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/object_detect/car_plate_detection" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/object_detect/car_plate_detection</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    <tr id="row08596101464"><td class="cellrowborder" valign="top" width="17.32173217321732%" headers="mcps1.2.4.1.1 "><p id="p178591510164619"><a name="p178591510164619"></a><a name="p178591510164619"></a>car_plate_recognition</p>
    </td>
    <td class="cellrowborder" valign="top" width="9.68096809680968%" headers="mcps1.2.4.1.2 "><p id="p1485911105469"><a name="p1485911105469"></a><a name="p1485911105469"></a>车牌��识别网络模型。</p>
    <p id="p17859191018468"><a name="p17859191018468"></a><a name="p17859191018468"></a>基于Caffe的CNN模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="72.997299729973%" headers="mcps1.2.4.1.3 "><p id="p7859181094619"><a name="p7859181094619"></a><a name="p7859181094619"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/car_plate_recognition" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/car_plate_recognition</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    <tr id="row88591310124617"><td class="cellrowborder" valign="top" width="17.32173217321732%" headers="mcps1.2.4.1.1 "><p id="p685911013465"><a name="p685911013465"></a><a name="p685911013465"></a>vgg_ssd</p>
    </td>
    <td class="cellrowborder" valign="top" width="9.68096809680968%" headers="mcps1.2.4.1.2 "><p id="p1786011016461"><a name="p1786011016461"></a><a name="p1786011016461"></a>目标检测网络模型。</p>
    <p id="p086018109465"><a name="p086018109465"></a><a name="p086018109465"></a>基于Caffe的SSD512模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="72.997299729973%" headers="mcps1.2.4.1.3 "><p id="p1186071044613"><a name="p1186071044613"></a><a name="p1186071044613"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/object_detect/vgg_ssd" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/object_detect/vgg_ssd</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
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
        1.  在Mind Studio�作界�的顶部���中选择**Tools \> Model Convert**，进入模型转�界�。
        2.  在弹出的**Model** **Conversion**�作界�中，进行模型转��置。
            -   Model File选择[步骤2](#li8221184418455)中下载的模型文件，此时会自动匹�到��文件并填写在Weight File中。
            -   Model Name填写为[表1](#table117203103464)对应的**模型�称**。
            -   car\_plate\_detection模型转�时�默认�置如下：

                AIPP�置中的**Input Image Size**分别修改为512�640，此处需�128\*16对�。**Model Image Format**需�修改为BGR888\_U8。

            -   car\_plate\_recognition模型转�时�默认�置如下：

                AIPP�置中的**Input Image Size**分别修改为384�80，此处需�128\*16对�。**Model Image Format**需�修改为BGR888\_U8。

            -   vgg\_ssd模型转�时�默认�置如下：

                **Model Image Format**需�修改为BGR888\_U8。

        3.  �击**OK**开始转�模型。

            car\_plate\_detection�vgg\_ssd模型在转�的时候，会有报错，错误信�如下图所示。

            **图 2**  模型转�错误<a name="fig1842765585311"></a>  
            

            ![](figures/model_facedetection_coversionfailed-27.png)

            此时在DetectionOutput层的Suggestion中选择SSDDetectionOutput，并点击Retry。

            模型转��功�，�缀为.om的离线模型存放地�为：$HOME/modelzoo/xxx/device。

            >![](public_sys-resources/icon-note.gif) **说明：**   
            >-   Mind Studio模型转�中�一步的具体�义和�数说明�以�考[Mind Studio用户手册](https://ascend.huawei.com/doc/mindstudio/)中的“模型转�“章节。  
            >-   XXX表示当�转�的模型�称，如vgg\_ssd.om存放地�为：$HOME/modelzoo/vgg\_ssd/device。  


    -   命令行模�下模型转�。
        1.  以Mind Studio安装用户进入存放原始模型的文件夹。

            **cd $HOME/models/carplaterecognition**

        2.  调用omg工具执行以下命令进行模型转�。

            ```
            ${DDK_HOME}/uihost/bin/omg --output="./XXX" --model="./XXX.prototxt" --framework=0 --ddk_version=${tools_version} --weight="./XXX.caffemodel" --input_shape=`head -1 $HOME/AscendProjects/sample-carplaterecognition/script/shape_XXX` --insert_op_conf=$HOME/AscendProjects/sample-carplaterecognition/script/aipp_XXX.cfg --op_name_map=$HOME/AscendProjects/sample-carplaterecognition/script/reassign_operators
            ```

            >![](public_sys-resources/icon-note.gif) **说明：**   
            >-   input\_shape�insert\_op\_conf�op\_name\_map所需�的文件都在��所在路径下的“sample-carplaterecognition/script�目录下，请根�您实际的��所在路径�置这些文件路径。  
            >-   **XXX**为[表1](#table117203103464)中的模型�称，转�时请替�填入需�转�模型的模型�称。其中car\_plate\_recognition模型转�时�需�op\_name\_map�数，如果没有删除�需�的�数，转�模型时会有报错。  
            >-   �个�数的具体�义��考[Atlas 200 DK用户手册](https://ascend.huawei.com/doc/atlas200dk/)中的“模型转�“章节。  


5.  将转�好的模型文件（.om文件）上传到[步骤1](#li953280133816)中��所在路径的“**sample-carplaterecognition/script**�目录下。

## 编译<a name="section1759513564117"></a>

1.  打开对应的工程。

    以Mind Studio安装用户在命令行中进入安装包解压�的“MindStudio-ubuntu/bin�目录，如：$HOME/MindStudio-ubuntu/bin。执行如下命令�动Mind Studio

    **./MindStudio.sh**

    �动�功�，打开**sample-carplaterecognition**工程，如[图 打开sample-carplaterecognition工程](#fig721144422212)所示。

    **图 3**  打开sample-carplaterecognition工程<a name="fig721144422212"></a>  
    

    ![](figures/zh-cn_image_0218876987.png)

2.  在src/param\_configure.conf文件中�置相关工程信�。

    **图 4**  �置文件路径<a name="fig1557065718252"></a>  
    

    ![](figures/zh-cn_image_0218877806.png)

    该�置文件内容如下：

    ```
    remote_host=
    data_source=
    presenter_view_app_name=
    ```

    -   remote\_host：�置为Atlas 200 DK开�者�的IP地�。
    -   data\_source : �置摄�头所属Channel，�值为Channel-1或者Channel-2，查询摄�头所属Channel的方法请�考[Atlas 200 DK用户手册](https://ascend.huawei.com/doc/Atlas200DK/)中的“如何查看摄�头所属Channel�。
    -   presenter\_view\_app\_name : 用户自定义的在PresenterServer界�展示的View Name，此View Name需�在Presenter Server展示界�唯一，�能为大�写字��数字�“/�的组�，�数至少1�。

    �置示例：

    ```
    remote_host=192.168.1.2
    data_source=Channel-1
    presenter_view_app_name=video
    ```

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   三个�数必须全部填写，�则无法通过编译。  
    >-   注��数填写时�需�使用“�符�。  

3.  执行deploy脚本， 进行�置�数调整�第三方库下载编译 打开Mind Studio工具的Terminal，此时默认在代�主目录下，执行如下命令在��指执行deploy脚本，进行环境部署。如[图 执行deploy脚本](#fig19393122943511)所示。

    **图 5**  执行deploy脚本<a name="fig19393122943511"></a>  
    ![](figures/执行deploy脚本-28.png "执行deploy脚本-28")

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   首次deploy时，没有部署第三方库时会自动下载并编译，耗时�能比较久，请�心等待。�续��新编译时，�会��下载编译，部署如上图所示。  
    >-   deploy时，需�选择与开��通信的主机侧ip，一般为虚拟网��置的ip。如果此ip和开��ip属于�网段，则会自动选择并部署。如果��网段，则需�手动输入与开��通信的主机侧ip�能完�deploy。  

4.  开始编译，打开Mind Studio工具，在工具�中点击**Build \> Build \> Build-Configuration**。如[图6](#fig13819202814301)所示，会在目录下生�build和run文件夹。

    **图 6**  编译�作�生�文件<a name="fig13819202814301"></a>  
    

    ![](figures/977f70e5b743c8ab6267c7d9b93194c.png)

    >![](public_sys-resources/icon-notice.gif) **须知：**   
    >首次编译工程时，**Build \> Build**为�色��点击状�。需�点击**Build \> Edit Build Configuration**，�置编译�数��进行编译。  

5.  <a name="li499911453439"></a>�动Presenter Server。

    打开Mindstudio工具的Terminal，在应用代�存放路径下，执行如下命令在���动carplate recognition应用的Presenter Server主程�。如[图 �动PresenterServer](#fig102142024389)所示。

    **bash run\_present\_server.sh**

    **图 7**  �动PresenterServer<a name="fig102142024389"></a>  
    

    ![](figures/3510ef898c672612c4ac5fa9397c708.png)

    -   当�示“Please choose one to show the presenter in browser\(default: 127.0.0.1\):“时，请输入在�览器中访问Presenter Server�务所使用的IP地�（一般为访问Mind Studio的IP地�）。

        如[图8](#fig73590910118)所示，请在“Current environment valid ip list“中选择通过�览器访问Presenter Server�务使用的IP地�，并输入存储视频解�数�的路径。

        **图 8**  工程部署示�图<a name="fig73590910118"></a>  
        

        ![](figures/827447f108867314d18ff4e4b22d421.png)

    如[图9](#fig19953175965417)所示，表示presenter\_server的�务�动�功。

    **图 9**  Presenter Server进程�动<a name="fig19953175965417"></a>  
    

    ![](figures/de3f85cb841628787ec4718cee44e8e.png)

    使用上图�示的URL登录Presenter Server，仅支�Chrome�览器。IP地�为[图 工程部署示�图](#fig73590910118)�作时输入的IP地�，端��默为7007，如下图所示，表示Presenter Server�动�功。

    **图 10**  主页显示<a name="fig64391558352"></a>  
    ![](figures/主页显示-29.png "主页显示-29")

    Presenter Server�Mind Studio与Atlas 200 DK之间通信使用的IP地�示例如下图所示：

    **图 11**  IP地�示例<a name="fig195318596543"></a>  
    ![](figures/IP地�示例-30.png "IP地�示例-30")

    -   Atlas 200 DK开�者�使用的IP地�为192.168.1.2（USB方�连接）。
    -   Presenter Server与Atlas 200 DK通信的IP地�为UI Host�务器中与Atlas 200 DK在�一网段的IP地�，例如：192.168.1.223。
    -   通过�览器访问Presenter Server的IP地�本示例为：10.10.0.1，由于Presenter Server与Mind Studio部署在�一�务器，此IP地�也为通过�览器访问Mind Studio的IP。


## �行<a name="section6245151616426"></a>

1.  �行车牌识别应用程�

    在Mind Studio工具的工具�中找到Run按钮，点击  **Run \> Run 'sample-carplaterecognition'**  ，如[图12](#fig12953163061713)所示，�执行程�已�在开��执行。

    **图 12**  程��行示�图<a name="fig12953163061713"></a>  
    

    ![](figures/7c9dd1a0a188f9dc2f5f25e4023f965.png)

2.  使用�动Presenter Server�务时�示的URL登录 Presenter Server 网站，详细��考[�动Presenter Server](#li499911453439)。

    等待Presenter Agent传输数�给�务端，�击“Refresh“刷新，当有数�时相应的Channel 的Status��绿色，如[图 Presenter Server界�](#fig113691556202312)所示。

    **图 13**  Presenter Server界�<a name="fig113691556202312"></a>  
    ![](figures/Presenter-Server界�-31.png "Presenter-Server界�-31")

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   Carplate recognition的Presenter Server最多支�10路Channel�时显示，�个  _presenter\_view\_app\_name_  对应一路Channel。  
    >-   由于硬件的�制，�一路支�的最大帧率是20fps，��于网络带宽的影�，帧率会自动适�为较低的帧率进行展示。  

3.  �击�侧对应的View Name链接，比如上图的“video�，查看结果，对于检测到的车牌，会给出车牌�信�。

## �续处�<a name="section1092612277429"></a>

-   **�止车牌识别应用**

    车牌识别应用执行�会处于�续�行状�，若��止车牌识别应用程�，�执行如下�作。

    �击[图 �止车牌识别应用](#fig14326454172518)所示的�止按钮�止车牌识别应用程�。

    **图 14**  �止车牌识别应用<a name="fig14326454172518"></a>  
    

    ![](figures/9381c4c3003c7f2cf5479b0464b177f.png)

    如[图 车牌识别应用已�止](#fig2182182518112)所示应用程�已�止�行

    **图 15**  车牌识别应用已�止<a name="fig2182182518112"></a>  
    

    ![](figures/186ec128ed22c2f0edfabf73aae63dc.png)

-   **�止Presenter Server�务**

    Presenter Server�务�动�会一直处于�行状�，若想�止车牌识别应用对应的Presenter Server�务，�执行如下�作。

    以Mind Studio安装用户在Mind Studio所在�务器中的命令行中执行如下命令查看车牌识别应用对应的Presenter Server�务的进程。

    **ps -ef | grep presenter | grep carplate\_recognition**

    ```
    ascend@ascend-HP-ProDesk-600-G4-PCI-MT:~/sample-carplaterecognition$ ps -ef | grep presenter | grep carplate_recognition
    ascend    7701  1615  0 14:21 pts/8    00:00:00 python3 presenterserver/presenter_server.py --app carplate_recognition
    ```

    如上所示  _7701_  �为车牌识别应用对应的Presenter Server�务的进程ID。

    若想�止此�务，执行如下命令：

    **kill -9** _7701_


