中文|[English](Readme.md)

# 密集人群人数统计（Python）<a name="ZH-CN_TOPIC_0228757087"></a>

开�者将本应用部署至Atlas 200 DK或者AI加速云�务器上实现对本地mp4文件或者RTSP视频�进行解�，对视频帧中的人群图�进行人头数�的预测，并将预测的结果信���至Presenter Server端进行展示。

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

        将[https://github.com/Atlas200dk/sample-crowdcounting-python](https://github.com/Atlas200dk/sample-crowdcounting-python)仓中的代�以Mind Studio安装用户下载至Mind Studio所在Ubuntu�务器的任�目录，例如代�存放路径为：$HOME/sample-crowdcounting-python。

    2.  命令行使用git命令方�获�。

        在命令行中：$HOME/AscendProjects目录下执行以下命令下载代�。

        **git clone https://github.com/Atlas200dk/sample-crowdcounting-python.git**

2.  <a name="li12291771229"></a>获�此应用中所需�的网络模型。

    �考[表 密集人群人数统计\(python\)使用模型](#table1119094515272)获�此应用中所用到的原始网络模型�其对应的��文件，并将其存放到Mind Studio所在Ubuntu�务器的任�目录，例如：$HOME/ascend/models/crowdcounting-python。

    **表 1**  密集人群人数统计\(python\)使用模型

    <a name="table1119094515272"></a>
    <table><thead align="left"><tr id="row677354502719"><th class="cellrowborder" valign="top" width="12.85%" id="mcps1.2.4.1.1"><p id="p167731845122717"><a name="p167731845122717"></a><a name="p167731845122717"></a>模型�称</p>
    </th>
    <th class="cellrowborder" valign="top" width="12.04%" id="mcps1.2.4.1.2"><p id="p277317459276"><a name="p277317459276"></a><a name="p277317459276"></a>模型说明</p>
    </th>
    <th class="cellrowborder" valign="top" width="75.11%" id="mcps1.2.4.1.3"><p id="p9773114512270"><a name="p9773114512270"></a><a name="p9773114512270"></a>模型下载路径</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row3122314144215"><td class="cellrowborder" valign="top" width="12.85%" headers="mcps1.2.4.1.1 "><p id="p13106121801715"><a name="p13106121801715"></a><a name="p13106121801715"></a>crowd_counting</p>
    </td>
    <td class="cellrowborder" valign="top" width="12.04%" headers="mcps1.2.4.1.2 "><p id="p13106171831710"><a name="p13106171831710"></a><a name="p13106171831710"></a>密集人群人数统计网络模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="75.11%" headers="mcps1.2.4.1.3 "><p id="p110671813170"><a name="p110671813170"></a><a name="p110671813170"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/object_detect/crowd_counting" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/object_detect/crowd_counting</a>目录中README.md下载原始网络模型文件。</p>
    </td>
    </tr>
    </tbody>
    </table>

3.  将原始网络模型转�为适�昇腾AI处�器的模型。
    1.  在Mind Studio�作界�的顶部���中选择**Tools \> Model Convert**，进入模型转�界�。
    2.  在弹出的**Model Conversion**�作界�中，Model File与Weight File分别选择[步骤2](#li12291771229)中下载的模型文件和��文件。
        -   **Model Name**填写为[表 检测网络应用\(python\)使用模型](#table1119094515272)对应的**模型�称**。
        -   **Input\_shape中name填写为input\_1，NHWC分别填写为1�768�1024�1。**
        -   **Input Image Format 选择 RGB888\_U8**。
        -   **关闭Model Image Format。**
        -   **Mean Less分别填写为127.5�127.5�127.5。**
        -   **Multiplying Factor分别填写为0.0078125�0.0078125�0.0078125。**
        -   **其他��默认值。**

    3.  �击OK开始转�模型。

        1.1.0.0和1.3.0.0版本模型转��功�，�缀为.om的离线模型存放地�为：**$HOME/tools/che/model-zoo/my-model/xxx**。

        1.31.0.0�以上版本模型转��功�，�缀为.om的离线模型存放地�为：**$HOME/modelzoo/xxx/device/xxx.om**。

    4.  将转�好的模型文件（.om文件）上传到[步骤1](#li953280133816)中��所在路径下的“sample-crowdcounting-python/model�目录下。

4.  以Mind Studio安装用户登录Mind Studio所在Ubuntu�务器，并设置环境��DDK\_HOME。

    **vim \~/.bashrc**

    1.  1.3.0.0版本执行如下命令在最�一行添加DDK\_HOME�LD\_LIBRARY\_PATH的环境��。

        **export DDK\_HOME=$HOME/tools/che/ddk/ddk**

        **export LD\_LIBRARY\_PATH=$DDK\_HOME/uihost/lib**

    2.  1.31.0.0�以上版本执行如下命令在最�一行添加环境��

        **export tools\_version=_1.31.X.X_**

        **export DDK\_HOME= \\$HOME/.mindstudio/huawei/ddk/\\$tools\_version/ddk**

        **export LD\_LIBRARY\_PATH= \\$DDK\_HOME/lib/x86\_64-linux-gcc5.4:\\$DDK\_HOME/uihost/lib**

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   1.31.0.0�以上版本环境��设置时1.31.X.X为DDK版本�，�以通过安装的DDK的包�获�，如DDK包的包�为Ascend\_DDK-1.31.T15.B150-1.1.1-x86\_64.ubuntu16.04.tar.gz，则此DDK的版本�为1.31.T15.B150。  
    >-   如果此环境��已�添加，则此步骤�跳过。  

    输入:wq!�存退出。

    执行如下命令使环境��生效。

    **source \~/.bashrc**


## 环境�置<a name="section1637464117139"></a>

**注：开��上hiai库�opencv库�相关�赖已安装�跳过此步骤。**

1.  �置开���网。

    请�考[https://github.com/Atlas200dk/sample-README/tree/master/DK\_NetworkConnect](https://github.com/Atlas200dk/sample-README/tree/master/DK_NetworkConnect)  ，进行开��网络连接�置。

2.  安装环境�赖。�

    请�考[https://github.com/Atlas200dk/sample-README/tree/master/DK\_Environment](https://github.com/Atlas200dk/sample-README/tree/master/DK_Environment)  ，进行环境�赖�置。


## 部署<a name="section1872516528910"></a>

1.  以Mind Studio安装用户进入crowdcounting-python应用代�所在根目录，如：$HOME/sample-crowdcounting-python。
2.  <a name="li9634105881418"></a>执行部署脚本，进行工程环境准备，Presenter Server�务器的�置等�作，其中Presenter Server用于接收Application��过�的数�并通过�览器进行结果展示。

    **bash deploy.sh** _host\_ip_

    -   _host\_ip_：Atlas 200 DK开�者�的IP地�。

    命令示例：

    **bash deploy.sh 192.168.1.2**

    当�示“Please choose one to show the presenter in browser\(default: 127.0.0.1\):“时，请输入在�览器中访问Presenter Server�务所使用的IP地�（一般为虚拟网�的IP地�。）

    请在“Current environment valid ip list“中选择通过�览器访问Presenter Server�务使用的IP地�。

3.  <a name="li156931456596"></a>�动Presenter Server。

    执行如下命令在���动密集人群人数统计应用的Presenter Server主程�。

    **bash start\_presenterserver.sh**

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >执行此脚本会先�死��的其他Presenter Server进程。��无正在执行的进程会�示presenter server not in process；��有正在执行的进程会�示presenter server stop success。  

    如[图 Presenter Server进程�动](#fig69531305324)所示，表示presenter\_server的�务�动�功。

    **图 1**  Presenter Server进程�动<a name="fig69531305324"></a>  
    ![](figures/Presenter-Server进程�动-65.png "Presenter-Server进程�动-65")

    使用上图�示的URL登录Presenter Server，仅支�Chrome�览器。IP地�为[步骤2](#li9634105881418)中输入的IP地�，端��默为7007，如下图所示，表示Presenter Server�动�功。

    **图 2**  主页显示<a name="fig64391558352"></a>  
    ![](figures/主页显示-66.png "主页显示-66")

    Presenter Server�Mind Studio与Atlas 200 DK之间通信使用的IP地�示例如下图所示：

    **图 3**  IP地�示例<a name="fig1881532172010"></a>  
    ![](figures/IP地�示例-67.png "IP地�示例-67")

    其中：

    -   Atlas 200 DK开�者�使用的IP地�为192.168.1.2（USB方�连接）。
    -   Presenter Server与Atlas 200 DK通信的IP地�为UI Host�务器中与Atlas 200 DK在�一网段的IP地�，例如：192.168.1.223。
    -   通过�览器访问Presenter Server的IP地�本示例为：10.10.0.1，由于Presenter Server与Mind Studio部署在�一�务器，此IP地�也为通过�览器访问Mind Studio的IP。

4.  crowdcounting-python应用支�解�本地视频和RTSP视频�。
    -   如果需�解�本地视频，需�将视频文件传到Host侧。

        例如将视频文件crowd.mp4上传到Host侧的“/home/HwHiAiUser/sample“目录下。

        >![](public_sys-resources/icon-note.gif) **说明：**   
        >支�H264与H265格�的MP4文件，如果MP4文件需�剪辑，建议使用开�工具ffmpeg，使用其他工具剪辑的视频文件ffmpeg工具�能�支�解�。  

    -   如果仅解�RTSP视频�，本步骤�跳过。


## �行<a name="section6245151616426"></a>

1.  在Mind Studio所在Ubuntu�务器中，以HwHiAiUser用户SSH登录到Host侧。

    **ssh HwHiAiUser@192.168.1.2**

2.  在HwHiAiUser用户下进入应用代�所在目录。

    **cd \~/HIAI\_PROJECTS/sample-crowdcounting-python**

3.  执行应用程�。

    **python main.py** _channel_

    -   _channel:_ 输入的视频文件�或者RTSP�地�

    视频文件�行的命令示例如下所示：

    **python main.py /home/HwHiAiUser/sample/crowd.mp4**

    RTSP视频�的命令示例如下所示：

    **python main.py rtsp://192.168.2.37:554/cam/realmonitor?channel=1&subtype=0**

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >�使用ctrl+c�止程�  

4.  使用�动Presenter Server�务时�示的URL登录 Presenter Server 网站，详细��考[�动Presenter Server](#li156931456596)。

    等待Presenter Agent传输数�给�务端，�击“Refresh“刷新，当有数�时相应的Channel 的Status��绿色，如[图 Presenter Server界�](#fig113691556202312)所示。

    **图 4**  Presenter Server界�<a name="fig113691556202312"></a>  
    ![](figures/Presenter-Server界�-68.png "Presenter-Server界�-68")

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   Presenter Server最多支�10路Channel�时显示，�个  _presenter\_view\_app\_name_  对应一路Channel。  
    >-   由于硬件的�制，�一路支�的最大帧率是20fps，��于网络带宽的影�，帧率会自动适�为较低的帧率进行展示。  

5.  �击�侧对应的View Name链接，比如上图的“video�，查看结果。

