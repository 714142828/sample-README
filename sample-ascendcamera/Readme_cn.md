中文|[English](Readme.md)

# Ascend Camera<a name="ZH-CN_TOPIC_0203223312"></a>

Ascend Camera主�功能是通过Atlas 200 DK开�者�上的摄�头采集数�，�过DVPP转�为jpg，最终�存为文件或者远程输出。

当�分支中的应用适�**1.32.0.0�以上**版本的[DDK&RunTime](https://ascend.huawei.com/resources)。

## ���件<a name="section137245294533"></a>

部署此Sample�，需�准备好以下环境：

-   已完�Mind Studio的安装。
-   已完�Atlas 200 DK开�者�与Mind Studio的连接，交�编译器的安装，SD�的制作�基本信�的�置等。

## 软件准备<a name="section8534138124114"></a>

�行此Sample�，需�按照此章节获���包，并进行相关的环境�置。

1.  获���包。
    1.  下载压缩包方�获�。

        将[https://github.com/Atlas200dk/sample-ascendcamera/tree/1-3x-0-0/](https://github.com/Atlas200dk/sample-ascendcamera/tree/1-3x-0-0/)仓中的代�以Mind Studio安装用户下载至Mind Studio所在Ubuntu�务器的任�目录，例如代�存放路径为：$HOME/sample-ascendcamera。

    2.  命令行使用git命令方�获�。

        在命令行中：$HOME/AscendProjects目录下执行以下命令下载代�。

        **git clone https://github.com/Atlas200dk/sample-facialrecognition.git --branch 1-3x-0-0**

2.  以Mind Studio安装用户登录Mind Studio所在Ubuntu�务器，确定当�使用的DDK版本�并设置环境��DDK\_HOME，tools\_version，LD\_LIBRARY\_PATH。
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



## 编译<a name="section11947911019"></a>

1.  打开对应的工程。

    以Mind Studio安装用户进入安装包解压�的“MindStudio-ubuntu/bin�目录，如：$HOME/MindStudio-ubuntu/bin，执行如下命令�动Mind Studio。

    **./MindStudio.sh**

    �动�功�，打开  **sample-ascendcamera**  工程，如图所示。

    **图 2**  打开sample-camera工程<a name="fig1696912234714"></a>  
    

    ![](figures/打开工程项目-摄�头.png)

2.  在**src/param\_configure.conf**文件中�置相关工程信�。

    **图 3**  �置文件路径<a name="fig10430135171116"></a>  
    

    ![](figures/ascendcamera_src.png)

    该�置文件内容如下：

    ```
    remote_host=
    ```

    需�手动添加�数�置：

    -   remote\_host：�置为Atlas 200 DK开�者�的IP地�。

    �置示例：

    ```
    remote_host=192.168.1.2
    ```

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >注��数填写时�需�使用“�符�。  

3.  执行deploy脚本， 进行�置�数调整�第三方库下载编译 打开Mind Studio工具的Terminal，此时默认在代�主目录下，执行如下命令在��指执行deploy脚本，进行环境部署。如[图 执行deploy脚本](#fig9298102581519)所示。

    **图 4**  执行deploy脚本<a name="fig9298102581519"></a>  
    ![](figures/执行deploy脚本-4.png "执行deploy脚本-4")

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   首次deploy时，没有部署第三方库时会自动下载并编译，耗时�能比较久，请�心等待。�续��新编译时，�会��下载编译，部署如上图所示。  
    >-   deploy时，需�选择与开��通信的主机侧ip，一般为虚拟网��置的ip。如果此ip和开��ip属于�网段，则会自动选择并部署。如果��网段，则需�手动输入与开��通信的主机侧ip�能完�deploy。  

4.  开始编译，打开Mind Studio工具，在工具�中点击**Build \> Build \> Build-Configuration**。如[图5](#fig5350165415161)所示，会在目录下生�build和run文件夹。

    **图 5**  编译�作�生�文件<a name="fig5350165415161"></a>  
    

    ![](figures/ascendcamera_build.png)

    >![](public_sys-resources/icon-notice.gif) **须知：**   
    >首次编译工程时，**Build \> Build**为�色��点击状�。需�点击**Build \> Edit Build Configuration**，�置编译�数��进行编译。  

5.  <a name="li043217442034"></a>�动Presenter Server。

    打开Mind Studio工具的Terminal，在应用代�存放路径下，执行如下命令在���动Ascend Camera应用的Presenter Server主程�。如[图6](#fig815812478221)所示。

    **bash run\_present\_server.sh**

    **图 6**  �动PresenterServer<a name="fig815812478221"></a>  
    

    ![](figures/ascend_camera_present_1.png)

    当�示“Please choose one to show the presenter in browser\(default: 127.0.0.1\):“时，请输入在�览器中访问Presenter Server�务所使用的IP地�（一般为访问Mind Studio的IP地�。）

    如[图7](#fig20890201582816)所示，请在“Current environment valid ip list“中选择通过�览器访问Presenter Server�务使用的IP地�。

    **图 7**  工程部署示�图<a name="fig20890201582816"></a>  
    

    ![](figures/ascend_camera_present_2.png)

    如[图8](#fig143112216312)所示，表示presenter\_server的�务�动�功。

    **图 8**  Presenter Server进程�动<a name="fig143112216312"></a>  
    

    ![](figures/ascendcamera_present_3.png)

    使用上图�示的URL登录Presenter Server，IP地�为[图7](#fig20890201582816)中输入的IP地�，端��默为7003，如下图所示，表示Presenter Server�动�功。

    **图 9**  主页显示<a name="fig3338812171913"></a>  
    ![](figures/主页显示-5.png "主页显示-5")

    Presenter Server�Mind Studio与Atlas 200 DK之间通信使用的IP地�示例如下图所示：

    **图 10**  IP地�示例<a name="fig633991291914"></a>  
    ![](figures/IP地�示例-6.png "IP地�示例-6")

    -   Atlas 200 DK开�者�使用的IP地�为192.168.1.2（USB方�连接）。
    -   Presenter Server与Atlas 200 DK通信的IP地�为UI Host�务器中与Atlas 200 DK在�一网段的IP地�，例如：192.168.1.223。
    -   通过�览器访问Presenter Server的IP地�本示例为：10.10.0.1，由于Presenter Server与Mind Studio部署在�一�务器，此IP地�也为通过�览器访问Mind Studio的IP。


## �行<a name="section123001119164920"></a>

�行Ascend Camera应用程�。

在Mind Studio工具的工具�中找到Run按钮，点击  **Run \> Run 'sample-ascendcamera'**，在开���行程�，如[图11](#fig19482184244914)所示。

**图 11**  程�执行示�图<a name="fig19482184244914"></a>  


![](figures/ascend_camera_run.png)

>![](public_sys-resources/icon-note.gif) **说明：**   
>报错信�忽略，因为IDE无法为�执行程�传�，上述步骤是将�执行程�与�赖的库文件部署到开��，需�ssh登录到开��至相应的目录文件下手动执行，具体请�考以下步骤。  

## 媒体信�离线�存<a name="section16681395119"></a>

1.  在Mind Studio所在Ubuntu�务器中，以HwHiAiUser用户SSH登录到开�者�。

    **ssh HwHiAiUser@192.168.1.2**

    对于Atlas 200 DK，host\_ip默认为192.168.1.2（USB连接）或者192.168.0.2（NIC连接）。

    对于AI加速云�务器，host\_ip�为当�Mind Studio所在�务器的IP地�。

2.  进入Ascend Camera的�执行文件所在路径。例如执行如下命令。

    **cd \~/HIAI\_PROJECTS/workspace\_mind\_studio/sample\_ascendcamera\_5b4f8b24/out**

3.  例如执行**workspace\_mind\_studio\_sample\_ascendcamera**命令进行媒体信�离线�存。

    从摄�头获�图片并�存为jpg文件，如果已�存在��文件则覆盖。

    **./workspace\_mind\_studio\_sample\_ascendcamera -i -c 1 -o  /localDirectory/filename.jpg --overwrite**

    -   -i：代表获�jpg格�的图片。
    -   -c：表示摄�头所在的channel，此�数有“0�和“1�两个选项，“0“对应“Camera1“，“1“对应“Camera2“，如果�填写，默认为“0�。查询摄�头所属Channel的方法请�考[Atlas 200 DK使用指�](https://ascend.huawei.com/doc)中的“如何查看摄�头所属Channel�。
    -   -o：表示文件存储�置，此处localDirectory为本地已存在的文件夹�称，filename.jpg为�存的图片�称，�用户自定义。

        >![](public_sys-resources/icon-note.gif) **说明：**   
        >此路径HwHiAiUser需�有�读写��。  

    -   --overwrite：覆盖已存在的��文件。

    其他详细�数请执行  **./workspace\_mind\_studio\_sample\_ascendcamera**  命令或者  **./workspace\_mind\_studio\_sample\_ascendcamera  --help**  命令��帮助信�。
    


## 通过Presenter Server播放实时视频<a name="section20204154716116"></a>

1.  在Mind Studio所在Ubuntu�务器中，以HwHiAiUser用户SSH登录到开�者�。

    **ssh HwHiAiUser@192.168.1.2**

2.  进入Ascend Camera的�执行文件所在路径。例如执行如下命令。

    **cd \~/HIAI\_PROJECTS/workspace\_mind\_studio/sample\_ascendcamera\_5b4f8b24/out**

3.  例如执行下命令将通过摄�头�获的视频传输到Presenter Server。

    **./workspace\_mind\_studio\_sample\_ascendcamera -v -c 1  -t 60 --fps 20 -w 704 -h 576 -s  _192.168.1.223_:7002/presenter\_view\_app\_name**

    -   -v：代表获�摄�头的视频，用�在Presenter Server端展示。
    -   -c：表示摄�头所在的channel，此�数有“0�和“1�两个选项，“0“对应“Camera1“，“1“对应“Camera2“，如果�填写，默认为“0�。查询摄�头所属Channel的方法请�考[Atlas 200 DK用户手册](https://ascend.huawei.com/doc/Atlas200DK/)中的“如何查看摄�头所属Channel�。
    -   -t：表示获�60s的视频文件，如果�指定此�数，则获�视频文件直至程�退出。
    -   --fps：表示存储视频的帧率，�值范围为1\~20，如果�设置此�数，则默认存储的视频帧率为10fps。
    -   -w：表示存储视频的宽。
    -   -h：表示存储视频的高。
    -   -s��的值_ 192.168.1.223_  为Presenter中7002端�对应的IP地�（如[步骤5](#li043217442034)中�动Presenter Server回显显示，�为与Atlas 200 DK开�者�通信的IP地�），7002为Ascendcamera应用对应的Presenter Server�务器的默认端��。
    -   _presenter\_view\_app\_name_：为在Presenter Server端展示的“View Name“，用户自定义，需���唯一，�能为大�写字��数字�“\_�的组�，�数3\~20。

    其他详细�数请执行  **./workspace\_mind\_studio\_sample\_ascendcamera**  命令或者  **./workspace\_mind\_studio\_sample\_ascendcamera  --help**  命令��帮助信�。

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   Ascend Camera的Presenter Server最多支�10路Channel�时显示，�个presenter\_view\_app\_name 对应一路Channel。  
    >-   由于硬件的�制，�一路支�的最大帧率是20fps，��于网络带宽的影�，帧率会自动适�为较低的帧率进行展示。  


## �续处�<a name="section856641210261"></a>

Presenter Server�务�动�会一直处于�行状�，若想�止Ascend Camera应用对应的Presenter Server�务，�执行如下�作。

以Mind Studio安装用户在Mind Studio所在�务器中的的命令行中执行如下命令查看Ascend Camera应用对应的Presenter Server�务的进程。

**ps -ef | grep presenter | grep display**

```
ascend@ascend-HP-ProDesk-600-G4-PCI-MT:~/sample-ascendcamera$ ps -ef | grep presenter | grep display
ascend 5758 20313 0 14:28 pts/24?? 00:00:00 python3 presenterserver/presenter_server.py --app display
```

如上所示  _5758_  �为Ascend Camera应用对应的Presenter Server�务的进程ID。

若想�止此�务，执行如下命令：

**kill -9** _5758_

