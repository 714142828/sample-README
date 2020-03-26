中文|[English](Readme.md)

# 密集人群人数统计<a name="ZH-CN_TOPIC_0219059426"></a>

开�者将本应用部署至Atlas 200 DK或者AI加速云�务器上实现对本地mp4文件或者RTSP视频�进行解�，对视频帧中的人群图�进行人头数�的预测，并将预测的结果信���至Presenter Server端进行展示。

当�分支中的应用适�**1.32.0.0�以上**版本的[DDK&RunTime](https://ascend.huawei.com/resources)。

## ���件<a name="section137245294533"></a>

部署此Sample�，需�准备好以下环境：

-   已完�Mind Studio的安装。
-   已完�Atlas 200 DK开�者�与Mind Studio的连接，交�编译器的安装，SD�的制作�基本信�的�置等。

## 软件准备<a name="section8534138124114"></a>

�行此Sample�，需�按照此章节获���包，并进行相关的环境�置。

1.  <a name="li953280133816"></a>获���包。
    1.  下载压缩包方�获�。

        将[https://github.com/Atlas200dk/sample-crowdcounting/tree/1-3x-0-0/](https://github.com/Atlas200dk/sample-facedetection/tree/1-3x-0-0/)仓中的代�以Mind Studio安装用户下载至Mind Studio所在Ubuntu�务器的任�目录，例如代�存放路径为：$HOME/AscendProjects/sample-crowdcounting。

    2.  命令行使用git命令方�获�。

        在命令行中：$HOME/AscendProjects目录下执行以下命令下载代�。

        **git clone https://github.com/Atlas200dk/sample-crowdcounting.git --branch 1-3x-0-0**

2.  <a name="li8221184418455"></a>获�此应用中所需�的原始网络模型。

    �考[表 crowd\_counting中使用的模型](#table117203103464)获�此应用中所用到的原始网络模型，并将其存放到Mind Studio所在Ubuntu�务器的任�目录。例如：$HOME/models/crowdcounting。

    **表 1**  crowd\_counting中使用的模型

    <a name="table117203103464"></a>
    <table><thead align="left"><tr id="row4859191074617"><th class="cellrowborder" valign="top" width="17.32173217321732%" id="mcps1.2.4.1.1"><p id="p18859111074613"><a name="p18859111074613"></a><a name="p18859111074613"></a>模型�称</p>
    </th>
    <th class="cellrowborder" valign="top" width="9.68096809680968%" id="mcps1.2.4.1.2"><p id="p17859171013469"><a name="p17859171013469"></a><a name="p17859171013469"></a>模型说明</p>
    </th>
    <th class="cellrowborder" valign="top" width="72.997299729973%" id="mcps1.2.4.1.3"><p id="p1385991094614"><a name="p1385991094614"></a><a name="p1385991094614"></a>模型下载路径</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row88591310124617"><td class="cellrowborder" valign="top" width="17.32173217321732%" headers="mcps1.2.4.1.1 "><p id="p13106121801715"><a name="p13106121801715"></a><a name="p13106121801715"></a>crowd_counting</p>
    </td>
    <td class="cellrowborder" valign="top" width="9.68096809680968%" headers="mcps1.2.4.1.2 "><p id="p13106171831710"><a name="p13106171831710"></a><a name="p13106171831710"></a>密集人群人数统计网络模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="72.997299729973%" headers="mcps1.2.4.1.3 "><p id="p110671813170"><a name="p110671813170"></a><a name="p110671813170"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/object_detect/crowd_counting" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/object_detect/crowd_counting</a>目录中README.md下载原始网络模型文件。</p>
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

4.  将原始网络模型转�为适�昇腾AI处�器的模型。
    1.  在Mind Studio�作界�的顶部���中选择**Tools \> Model Convert**，进入模型转�界�。
    2.  在弹出的**Model** **Conversion**�作界�中，进行模型转��置。
        -   Model File选择[步骤2](#li8221184418455)中下载的模型文件。
        -   Model Name填写为[表1](#table117203103464)对应的**模型�称**。
        -   crowd\_counting模型转�时的�默认�置如：[图2 crowd\_counting模型转�](#fig8912228135419)。
        -   其他��默认值

            **图 2**  crowd\_counting模型转�<a name="fig8912228135419"></a>  
            

            ![](figures/zh-cn_image_0219068294.png)

            ![](figures/zh-cn_image_0219068655.png)

    3.  �击**OK**开始转�模型。

        模型转��功�，�缀为.om的离线模型存放地�为：$HOME/modelzoo/crowd\_counting/device。

        >![](public_sys-resources/icon-note.gif) **说明：**   
        >-   Mind Studio模型转�中�一步的具体�义和�数说明�以�考[Mind Studio用户手册](https://ascend.huawei.com/doc/mindstudio/)中的“模型转�“章节。  


5.  将转�好的模型文件（.om文件）上传到[步骤1](#li953280133816)中��所在路径的“**sample-crowdcounting/script**�目录下。

## 编译<a name="section1759513564117"></a>

1.  打开对应的工程。

    以Mind Studio安装用户在命令行中进入安装包解压�的“MindStudio-ubuntu/bin�目录，如：$HOME/MindStudio-ubuntu/bin。执行如下命令�动Mind Studio

    **./MindStudio.sh**

    �动�功�，打开**sample-crowdcounting**工程。

2.  在src/param\_configure.conf文件中�置相关工程信�。

    **图 3**  �置文件路径<a name="fig1557065718252"></a>  
    

    ![](figures/zh-cn_image_0219071560.png)

    该�置文件内容如下：

    ```
    remote_host=
    presenter_view_app_name=
    video_path_of_host=
    rtsp_video_stream=
    ```

    需�手动添加�数�置:

    -   remote\_host：�置为Atlas 200 DK开�者�的IP地�。
    -   presenter\_view\_app\_name: 用户自定义的在PresenterServer界�展示的View Name，此View Name需�在Presenter Server展示界�唯一，�能为大�写字��数字�“\_�的组�，�数3\~20。
    -   video\_path\_of\_host：�置为HOST侧的视频文件的�对路径。
    -   rtsp\_video\_stream：�置为RTSP视频�的URL。

    视频文件�置示例如下：

    ```
    remote_host=192.168.1.2
    presenter_view_app_name=video
    video_path_of_host=/home/HwHiAiUser/car.mp4
    rtsp_video_stream=
    ```

    Rtsp视频��置示例如下：

    ```
    remote_host=192.168.1.2
    presenter_view_app_name=video
    video_path_of_host=
    rtsp_video_stream=rtsp://192.168.2.37:554/cam/realmonitor?channel=1&subtype=0
    ```

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   �数remote\_host和presenter\_view\_app\_name：必须全部填写，�则无法通过build。  
    >-   注�所填�数�用使用“�。  
    >-   �数video\_path\_of\_host和rtsp\_video\_stream必须至少填写一项。  
    >-   当�RTSP视频��支�rtsp://ip:port/path格�，如果需�使用其它格�的url，需�把video\_decode.cpp中的IsValidRtsp函数去除，或者直接返回true，跳过正则表达�匹�。  
    >-   本样例中�供的RTSP�地���以直接使用。如果需�使用RTSP，请在本地使用live555或其它方�制作RTSP视频�，并且�以在VLC中播放。然�将本地制作好的RTSP视频�的URL填入�置文件的相应�数中，���行。  

3.  执行deploy脚本， 进行�置�数调整�第三方库下载编译 打开Mind Studio工具的Terminal，此时默认在代�主目录下，执行如下命令在��指执行deploy脚本，进行环境部署。如[图 执行deploy脚本](#fig202009167369)所示。

    **图 4**  执行deploy脚本<a name="fig202009167369"></a>  
    ![](figures/执行deploy脚本-32.png "执行deploy脚本-32")

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   首次deploy时，没有部署第三方库时会自动下载并编译，耗时�能比较久，请�心等待。�续��新编译时，�会��下载编译，部署如上图所示。  
    >-   deploy时，需�选择与开��通信的主机侧ip，一般为虚拟网��置的ip。如果此ip和开��ip属于�网段，则会自动选择并部署。如果��网段，则需�手动输入与开��通信的主机侧ip�能完�deploy。  

4.  开始编译，打开Mind Studio工具，在工具�中点击**Build \> Build \> Build-Configuration**。会在目录下生�build和run文件夹。

    >![](public_sys-resources/icon-notice.gif) **须知：**   
    >首次编译工程时，**Build \> Build**为�色��点击状�。需�点击**Build \> Edit Build Configuration**，�置编译�数��进行编译。  

5.  <a name="li499911453439"></a>�动Presenter Server。

    打开Mindstudio工具的Terminal，在应用代�存放路径下，执行如下命令在���动Crowd Counting应用的Presenter Server主程�。如[图 �动PresenterServer](#fig102142024389)所示。

    **bash run\_present\_server.sh**

    **图 5**  �动PresenterServer<a name="fig102142024389"></a>  
    

    ![](figures/zh-cn_image_0219072221.png)

    -   当�示“Please choose one to show the presenter in browser\(default: 127.0.0.1\):“时，请输入在�览器中访问Presenter Server�务所使用的IP地�（一般为访问Mind Studio的IP地�）。

        如[图6](#fig73590910118)所示，请在“Current environment valid ip list“中选择通过�览器访问Presenter Server�务使用的IP地�，并输入存储视频解�数�的路径。

        **图 6**  工程部署示�图<a name="fig73590910118"></a>  
        

        ![](figures/zh-cn_image_0219072532.png)

    如[图7](#fig19953175965417)所示，表示presenter\_server的�务�动�功。

    **图 7**  Presenter Server进程�动<a name="fig19953175965417"></a>  
    

    ![](figures/zh-cn_image_0219072725.png)

    使用上图�示的URL登录Presenter Server，仅支�Chrome�览器，IP地�为[图6](#fig73590910118)中输入的IP地�，端��默为7007，如下图所示，表示Presenter Server�动�功。

    **图 8**  主页显示<a name="fig129539592546"></a>  
    ![](figures/主页显示-33.png "主页显示-33")

    Presenter Server�Mind Studio与Atlas 200 DK之间通信使用的IP地�示例如下图所示：

    **图 9**  IP地�示例<a name="fig195318596543"></a>  
    ![](figures/IP地�示例-34.png "IP地�示例-34")

    -   Atlas 200 DK开�者�使用的IP地�为192.168.1.2（USB方�连接）。
    -   Presenter Server与Atlas 200 DK通信的IP地�为UI Host�务器中与Atlas 200 DK在�一网段的IP地�，例如：192.168.1.223。
    -   通过�览器访问Presenter Server的IP地�本示例为：10.10.0.1，由于Presenter Server与Mind Studio部署在�一�务器，此IP地�也为通过�览器访问Mind Studio的IP。

6.  密集人群人数统计应用支�解�本地视频和RTSP视频�。
    -   如果需�解�本地视频，需�将视频文件传到Host侧。

        例如将视频文件crowd.mp4上传到Host侧的“/home/HwHiAiUser/“目录下。

        >![](public_sys-resources/icon-note.gif) **说明：**   
        >支�H264与H265格�的MP4文件，如果MP4文件需�剪辑，建议使用开�工具ffmpeg，使用其他工具剪辑的视频文件ffmpeg工具�能�支�解�。  

    -   如果仅解�RTSP视频�，本步骤�跳过。


## �行<a name="section6245151616426"></a>

1.  �行Crowd Counting程�

    在Mind Studio工具的工具�中找到Run按钮，点击**Run \> Run 'sample-crowdcounting'**，如[图10](#fig12953163061713)所示，�执行程�已�在开��执行。

    **图 10**  程��行示�图<a name="fig12953163061713"></a>  
    

    ![](figures/zh-cn_image_0219073392.png)

2.  使用�动Presenter Server�务时�示的URL登录 Presenter Server 网站，详细��考[�动Presenter Server](#li499911453439)。

    等待Presenter Agent传输数�给�务端，�击“Refresh�刷新，当有数�时相应的Channel 的Status��绿色，如[图 Presenter Server界�](#fig69382913311)所示

    **图 11**  Presenter Server界�<a name="fig69382913311"></a>  
    ![](figures/Presenter-Server界�-35.png "Presenter-Server界�-35")

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   Crowd Counting的Presenter Server最多支�10路Channel�时显示，�个  _presenter\_view\_app\_name_  对应一路Channel。  
    >-   由于硬件的�制，�一路支�的最大帧率是20fps，��于网络带宽的影�，帧率会自动适�为较低的帧率进行展示。  

3.  �击�侧对应的View Name链接，比如上图的“video�，查看结果。

## �续处�<a name="section1092612277429"></a>

-   **�止Crowd Counting应用**

    Crowd Counting应用执行�会处于�续�行状�，若��止Crowd Counting应用程�，�执行如下�作。

    �击�止按钮�止Crowd Counting应用程�。如[图 Crowd Counting应用程��行结�](#fig464152917203)所示应用程�已�止�行

    **图 12**  Crowd Counting应用程��行结�<a name="fig464152917203"></a>  
    

    ![](figures/zh-cn_image_0219075771.png)

-   **�止Presenter Server�务**

    Presenter Server�务�动�会一直处于�行状�，若想�止Crowd Counting应用对应的Presenter Server�务，�执行如下�作。

    以Mind Studio安装用户在Mind Studio所在�务器中的命令行中执行如下命令查看Crowd Counting应用对应的Presenter Server�务的进程。

    **ps -ef | grep presenter | grep crowd\_counting**

    ```
    ascend@ascend-HP-ProDesk-600-G4-PCI-MT:~/sample-crowdcounting$ ps -ef | grep presenter | grep crowd_counting 
     ascend    7701  1615  0 14:21 pts/8    00:00:00 python3 presenterserver/presenter_server.py --app crowd_counting
    ```

    如上所示  _7701_  �为crowd\_counting应用对应的Presenter Server�务的进程ID。

    若想�止此�务，执行如下命令：

    **kill -9** _7701_


