中文|[English](Readme.md)

# 人脸防伪<a name="ZH-CN_TOPIC_0219080565"></a>

开�者�以将本application部署至Atlas 200DK上实现对摄�头数�的实时采集�并通过视频检测是�为真人功能。

当�分支中的应用适�**1.31.0.0�以上**版本的[DDK&RunTime](https://ascend.huawei.com/resources)。

## ���件<a name="section137245294533"></a>

部署此Sample�，需�准备好以下环境：

-   已完�Mind Studio的安装。
-   已完�Atlas 200 DK开�者�与Mind Studio的连接，交�编译器的安装，SD�的制作�基本信�的�置等。

## 软件准备<a name="section081240125311"></a>

�行此Sample�，需�按照此章节获���包，进行相关的环境�置并准备模型文件。

1.  <a name="li953280133816"></a>获���包。
    1.  下载压缩包方�获�。

        将[https://github.com/Atlas200dk/sample-faceantispoofing](https://github.com/Atlas200dk/sample-headposeestimation)仓中的代�以Mind Studio安装用户下载至Mind Studio所在Ubuntu�务器的任�目录，例如代�存放路径为：$HOME/AscendProjects/sample-faceantispoofing。

    2.  命令行使用git命令方�获�。

        在命令行中：$HOME/AscendProjects目录下执行以下命令下载代�。

        **git clone https://github.com/Atlas200dk/sample-faceantispoofing.git --branch 1-3x-0-0**

2.  <a name="li1365682471610"></a>获�此应用中所需�的原始网络模型。

    �考[表1](#table144841813177)获�此应用中所用到的原始网络模型�其对应的��文件，并将其存放到Mind Studio所在Ubuntu�务器的任�目录，这两个文件必须存放到�一个目录下。例如：$HOME/models/faceantispoofing。

    **表 1**  Face Antispoofing中使用模型

    <a name="table144841813177"></a>
    <table><thead align="left"><tr id="row161061318181712"><th class="cellrowborder" valign="top" width="13.61%" id="mcps1.2.4.1.1"><p id="p1410671814173"><a name="p1410671814173"></a><a name="p1410671814173"></a>模型�称</p>
    </th>
    <th class="cellrowborder" valign="top" width="10.03%" id="mcps1.2.4.1.2"><p id="p1106118121716"><a name="p1106118121716"></a><a name="p1106118121716"></a>模型说明</p>
    </th>
    <th class="cellrowborder" valign="top" width="76.36%" id="mcps1.2.4.1.3"><p id="p14106218121710"><a name="p14106218121710"></a><a name="p14106218121710"></a>模型下载路径</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row1710661814171"><td class="cellrowborder" valign="top" width="13.61%" headers="mcps1.2.4.1.1 "><p id="p85671718123118"><a name="p85671718123118"></a><a name="p85671718123118"></a>face_detection</p>
    </td>
    <td class="cellrowborder" valign="top" width="10.03%" headers="mcps1.2.4.1.2 "><p id="p1456731819318"><a name="p1456731819318"></a><a name="p1456731819318"></a>人脸检测网络模型。</p>
    <p id="p256717183312"><a name="p256717183312"></a><a name="p256717183312"></a>此模型是基于Caffe的Resnet10-SSD300模型转��的网络模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.36%" headers="mcps1.2.4.1.3 "><p id="p1956741833120"><a name="p1956741833120"></a><a name="p1956741833120"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/object_detect/face_detection" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/object_detect/face_detection</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    <tr id="row8833411314"><td class="cellrowborder" valign="top" width="13.61%" headers="mcps1.2.4.1.1 "><p id="p65671018123118"><a name="p65671018123118"></a><a name="p65671018123118"></a>depl</p>
    </td>
    <td class="cellrowborder" valign="top" width="10.03%" headers="mcps1.2.4.1.2 "><p id="p9567131833116"><a name="p9567131833116"></a><a name="p9567131833116"></a>�部特�点网络模型。此模型是基于Caffe的VGG-SSD模型转��的网络模型</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.36%" headers="mcps1.2.4.1.3 "><p id="p981712263315"><a name="p981712263315"></a><a name="p981712263315"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/object_detect/head_pose_estimation" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/object_detect/head_pose_estimation</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    </tbody>
    </table>

3.  以Mind Studio安装用户登录Mind Studio所在Ubuntu�务器，确定当�使用的DDK版本�并设置环境��DDK\_HOME，tools\_version，LD\_LIBRARY\_PATH。
    1.  <a name="li61417158198"></a>查询当�使用的DDK版本�。

        �通过Mind Studio工具查询，也�以通过DDK软件包进行获�。

        -   使用Mind Studio工具查询。

            在Mind Studio工程界��次选择“File \> Settings \> System Settings \> Ascend DDK“，弹出如[图 DDK版本�查询](#fig17553193319118)所示界�。

            **图 1**  DDK版本�查询<a name="fig17553193319118"></a>  
            ![](figures/DDK版本�查询-36.png "DDK版本�查询-36")

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
        >-   **_1.31.X.X_**是[a](#li61417158198)中查询到的DDK版本�，需�根�查询结果对应填写，如**1.31.T15.B150**  
        >-   如果此环境��已�添加，则此步骤�跳过。  

        输入:wq!�存退出。

        执行如下命令使环境��生效。

        **source \~/.bashrc**

4.  将原始网络模型转�为适�昇腾AI处�器的模型。
    1.  在Mind Studio�作界�的顶部���中选择**Tools \> Model Convert**，进入模型转�界�。
    2.  在弹出的**Model** **Conversion**�作界�中，进行模型转��置。
        -   Model File选择[步骤2](#li1365682471610)中下载的模型文件，此时会自动匹�到��文件并填写在Weight File中。
        -   Model Name填写为[表1](#table144841813177)中的模型�称。
            1.  face\_detection模型的AIPP�置界�需�将**Model Image Format**修改为BGR888\_U8。其他使用默认值。
            2.  depl模型的AIPP�置界�需�将AIPP关闭。

    3.  转�时，face\_detection模型会出现[图 模型转�错误](#fig2865313121718)中所示的报错信�。

        **图 2**  模型转�错误<a name="fig2865313121718"></a>  
        

        ![](figures/model_facedetection_coversionfailed-37.png)

        此时在**DetectionOutput**层的**Suggestion**中选择**SSDDetectionOutput**，并点击**Retry**。

        模型转��功�，�缀为.om的离线模型存放地�为：$HOME/modelzoo/xxx/device。

        >![](public_sys-resources/icon-note.gif) **说明：**   
        >Mindstudio模型转�中�一步的具体�义和�数说明�以�考[Mind Studio用户手册](https://ascend.huawei.com/doc/mindstudio/)中的“模型转�“章节。  


5.  将转�好的模型文件（.om文件）上传到[步骤1](#li953280133816)中��所在路径下的“**sample-faceantispoofing/script**�目录下。

## 编译<a name="section7994174585917"></a>

1.  打开对应的工程。

    以Mind Studio安装用户在命令行中进入安装包解压�的“MindStudio-ubuntu/bin�目录，如：$HOME/MindStudio-ubuntu/bin。执行如下命令�动Mind Studio。

    **./MindStudio.sh**

    �动�功�，打开**sample-faceantispoofing**工程，如[图 打开faceantispoofing工程](#fig05481157171918)所示。

    **图 3**  打开faceantispoofing工程<a name="fig05481157171918"></a>  
    

    ![](figures/zh-cn_image_0219083850.jpg)

2.  在**src/param\_configure.conf**文件中�置相关工程信�。

    如[图 �置文件路径](#fig0391184062214)所示。

    **图 4**  �置文件<a name="fig0391184062214"></a>  
    

    ![](figures/zh-cn_image_0219083915.png)

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

3.  执行deploy脚本， 进行�置�数调整�第三方库下载编译 打开Mind Studio工具的Terminal，此时默认在代�主目录下，执行如下命令在��指执行deploy脚本，进行环境部署。如[图 执行deploy脚本](#fig22681517439)所示。

    **图 5**  执行deploy脚本<a name="fig22681517439"></a>  
    ![](figures/执行deploy脚本-38.png "执行deploy脚本-38")

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   首次deploy时，没有部署第三方库时会自动下载并编译，耗时�能比较久，请�心等待。�续��新编译时，�会��下载编译，部署如上图所示。  
    >-   deploy时，需�选择与开��通信的主机侧ip，一般为虚拟网��置的ip。如果此ip和开��ip属于�网段，则会自动选择并部署。如果��网段，则需�手动输入与开��通信的主机侧ip�能完�deploy。  

4.  开始编译，打开Mindstudio工具，在工具�中点击**Build \> Build \> Build-Configuration**。会在目录下生�build和run文件夹。

    >![](public_sys-resources/icon-notice.gif) **须知：**   
    >首次编译工程时，**Build \> Build**为�色��点击状�。需�点击**Build \> Edit Build Configuration**，�置编译�数��进行编译。  

5.  <a name="li499911453439"></a>�动Presenter Server。

    打开Mind Studio工具的Terminal，在应用程�代�存放路径下，执行如下命令在���动Face Antispoofingon应用的Presenter Server主程�。

    **bash run\_present\_server.sh**

    当�示“**Please choose one to show the presenter in browser\(default: 127.0.0.1\):**�时，请输入在�览器中访问Presenter Server�务所使用的IP地�（一般为访问Mind Studio的IP地�）。

    如[图 工程部署示�图](#fig999812514814)所示，请在“**Current environment valid ip list**�中选择通过�览器访问Presenter Server�务使用的IP地�。

    **图 6**  工程部署示�图<a name="fig999812514814"></a>  
    

    ![](figures/zh-cn_image_0219084084.jpg)

    如[图7](#fig69531305324)所示，表示presenter\_server的�务�动�功。

    **图 7**  Presenter Server进程�动<a name="fig69531305324"></a>  
    

    ![](figures/zh-cn_image_0219085022.jpg)

    使用上图�示的URL登录Presenter Server，仅支�Chrome�览器。IP地�为[图 工程部署示�图](#fig999812514814)�作时输入的IP地�，端��默为7007，如下图所示，表示Presenter Server�动�功。

    **图 8**  主页显示<a name="fig64391558352"></a>  
    ![](figures/主页显示-39.png "主页显示-39")

    Presenter Server�Mind Studio与Atlas 200 DK之间通信使用的IP地�示例如下图所示：

    **图 9**  IP地�示例<a name="fig1881532172010"></a>  
    ![](figures/IP地�示例-40.png "IP地�示例-40")

    其中：

    -   Atlas 200 DK开�者�使用的IP地�为192.168.1.2（USB方�连接）。
    -   Presenter Server与Atlas 200 DK通信的IP地�为UI Host�务器中与Atlas 200 DK在�一网段的IP地�，例如：192.168.1.223。
    -   通过�览器访问Presenter Server的IP地�本示例为：10.10.0.1，由于Presenter Server与Mind Studio部署在�一�务器，此IP地�也为通过�览器访问Mind Studio的IP。


## �行<a name="section551710297235"></a>

1.  �行Face Antispoofing程�。

    在Mind Studio工具的工具�中找到Run按钮，点击**Run \> Run 'sample-faceantispoofing'**，如[图 程�已执行示�图](#fig93931954162719)所示，�执行程�已�在开�者��行。

    **图 10**  程��行示例<a name="fig93931954162719"></a>  
    

    ![](figures/zh-cn_image_0219085391.jpg)

2.  使用�动Presenter Server�务时�示的URL登录 Presenter Server 网站，详细��考[�动Presenter Server](#li499911453439)。

    等待Presenter Agent传输数�给�务端，�击“Refresh“刷新，当有数�时相应的Channel 的Status��绿色，如[图11](#fig113691556202312)所示。

    **图 11**  Presenter Server界�<a name="fig113691556202312"></a>  
    ![](figures/Presenter-Server界�-41.png "Presenter-Server界�-41")

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   Face Antispoofingon的Presenter Server最多支�10路Channel�时显示，�个  _presenter\_view\_app\_name_  对应一路Channel。  
    >-   由于硬件的�制，�一路支�的最大帧率是20fps，��于网络带宽的影�，帧率会自动适�为较低的帧率进行展示。  

3.  �击�侧对应的View Name链接，比如上图的“video�，查看结果。

## �续处�<a name="section177619345260"></a>

-   **�止Face Antispoofing应用**

    Face Antispoofing应用执行�会处于�续�行状�，若��止Face Antispoofing应用程�，�执行如下�作。

    �击�止按钮�止Face Antispoofing应用程�。如[图 Face Antispoofingon应用已�止](#fig2182182518112)所示应用程�已�止�行。

    **图 12**  Face Antispoofingon应用已�止<a name="fig2182182518112"></a>  
    

    ![](figures/zh-cn_image_0219086288.jpg)

-   **�止Presenter Server�务**

    Presenter Server�务�动�会一直处于�行状�，若想�止Face Antispoofingon应用对应的Presenter Server�务，�执行如下�作。

    以Mind Studio安装用户在Mind Studio所在�务器中的命令行中执行如下命令查看Face Antispoofingon应用对应的Presenter Server�务的进程。

    **ps -ef | grep presenter | grep faceantispoofing**

    ```
    ascend@ascend-HP-ProDesk-600-G4-PCI-MT:~/sample-faceantispoofing$ ps -ef | grep presenter | grep faceantispoofing 
     ascend    7701  1615  0 14:21 pts/8    00:00:00 python3 presenterserver/presenter_server.py --app faceantispoofing 
    ```

    如上所示  _7701_  �为Face Antispoofingon应用对应的Presenter Server�务的进程ID。若想�止此�务，执行如下命令：

    **kill -9** _7701_


