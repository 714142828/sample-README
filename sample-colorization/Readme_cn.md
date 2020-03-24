中文|[English](Readme.md)

# 黑白图�上色<a name="ZH-CN_TOPIC_0219108795"></a>

本应用支��行在Atlas 200 DK上，实现了对黑白图�自动上色的功能。

当�分支中的应用适�**1.32.0.0�以上**版本的[DDK&RunTime](https://ascend.huawei.com/resources)。

## ���件<a name="section137245294533"></a>

部署此Sample�，需�准备好以下环境：

-   已完�Mind Studio的安装。
-   已完�Atlas 200 DK开�者�与Mind Studio的连接，交�编译器的安装，SD�的制作�基本信�的�置等。

## 软件准备<a name="section181111827718"></a>

�行此Sample�，需�按照此章节获���包，并进行相关的环境�置。

1.  <a name="li953280133816"></a>获���包。
    1.  下载压缩包方�获�。

        将[https://github.com/Atlas200dk/sample-colorization/tree/1-3x-0-0/](https://github.com/Atlas200dk/sample-colorization/tree/1-3x-0-0/)仓中的代�以Mind Studio安装用户下载至Mind Studio所在Ubuntu�务器的任�目录，这两个文件必须存放到�一个目录下。例如代�存放路径为：$HOME/AscendProjects/sample-colorization。

    2.  命令行使用git命令方�获�。

        在命令行中：$HOME/AscendProjects目录下执行以下命令下载代�。

        **git clone https://github.com/Atlas200dk/sample-colorization.git --branch 1-3x-0-0**

2.  <a name="li2074865610364"></a>获�此应用中所需�的原始网络模型。

    �考[表 黑白图�上色应用使用模型](#table19942111763710)获�此应用中所用到的原始网络模型�其对应的��文件，并将其存放到Mind Studio所在Ubuntu�务器的任�目录，这两个文件必须存放到�一个目录下。例如：$HOME/models/colorization。

    **表 1**  黑白图�上色应用使用模型

    <a name="table19942111763710"></a>
    <table><thead align="left"><tr id="row611318123710"><th class="cellrowborder" valign="top" width="11.959999999999999%" id="mcps1.2.4.1.1"><p id="p81141820376"><a name="p81141820376"></a><a name="p81141820376"></a>模型�称</p>
    </th>
    <th class="cellrowborder" valign="top" width="8.07%" id="mcps1.2.4.1.2"><p id="p13181823711"><a name="p13181823711"></a><a name="p13181823711"></a>模型说明</p>
    </th>
    <th class="cellrowborder" valign="top" width="79.97%" id="mcps1.2.4.1.3"><p id="p1717182378"><a name="p1717182378"></a><a name="p1717182378"></a>模型下载路径</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row1119187377"><td class="cellrowborder" valign="top" width="11.959999999999999%" headers="mcps1.2.4.1.1 "><p id="p4745165253920"><a name="p4745165253920"></a><a name="p4745165253920"></a>colorization</p>
    </td>
    <td class="cellrowborder" valign="top" width="8.07%" headers="mcps1.2.4.1.2 "><p id="p1874515218391"><a name="p1874515218391"></a><a name="p1874515218391"></a>黑白图�上色模型</p>
    </td>
    <td class="cellrowborder" valign="top" width="79.97%" headers="mcps1.2.4.1.3 "><p id="p611318163718"><a name="p611318163718"></a><a name="p611318163718"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/object_detect/colorization" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/object_detect/colorization</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
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
    1.  在Mind Studio�作界�的顶部���中选择**Tools \> Model Convert**，进入模型转�界�。
    2.  在弹出的**Model Conversion**�作界�中，进行模型转��置。
        -   Model File选择[步骤2](#li2074865610364)中下载的模型文件，此时会自动匹�到��文件并填写在Weight File中。
        -   Model Name填写为[表1](#table19942111763710)对应的**模型�称**：colorization。

            ![](figures/zh-cn_image_0219108879.png)

        -   colorization模型输入shape为\(1,3,224,224\)，所以输入节点�数需�设置为1,3,224,224。

            ![](figures/zh-cn_image_0219108881.png)

        -   模型输入为归一化的Lab图�的L通�数�，所以需�关闭aipp。

            ![](figures/zh-cn_image_0219108885.png)

    3.  �击Finish开始转�模型。

        模型转��功�，�缀为.om的离线模型存放地�为：$HOME/modelzoo/colorization/device。

        >![](public_sys-resources/icon-note.gif) **说明：**   
        >Mindstudio模型转�中�一步的具体�义和�数说明�以�考[Mind Studio用户手册](https://ascend.huawei.com/doc/mindstudio/)中的“模型转�“章节。  


5.  将转�好的模型文件（.om文件）上传到[步骤1](#li953280133816)中��所在路径下的“**sample\_colorization/script**�目录下。

## 编译<a name="section3723145213347"></a>

1.  打开对应的工程。

    以Mind Studio安装用户在命令行中进入安装包解压�的“MindStudio-ubuntu/bin�目录，如：$HOME/MindStudio-ubuntu/bin。执行如下命令�动Mind Studio。

    **./MindStudio.sh**

    �动�功�，打开**sample\_colorization**工程，如[图 打开sample\_colorization工程](#fig05481157171918)所示。

    **图 2**  打开sample\_colorization工程<a name="fig05481157171918"></a>  
    

    ![](figures/zh-cn_image_0219108999.png)

2.  在**src/param\_configure.conf**文件中�置相关工程信�。

    **图 3**  �置文件路径<a name="fig0391184062214"></a>  
    ![](figures/�置文件路径-54.png "�置文件路径-54")

    该�置文件内容如下：

    ```
    remote_host=
    ```

    需�手动添加�数�置：

    remote\_host：Atlas 200 DK开�者�的IP地�。

    �置示例：

    ```
    remote_host=192.168.1.2
    ```

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   注��数填写时�需�使用“�符�。  

3.  执行deploy脚本， 进行�置�数调整�第三方库下载编译 打开Mind Studio工具的Terminal，此时默认在代�主目录下，执行如下命令在��指执行deploy脚本，进行环境部署。如[图 执行deploy脚本](#fig63536151461)所示。

    **图 4**  执行deploy脚本<a name="fig63536151461"></a>  
    ![](figures/执行deploy脚本-55.png "执行deploy脚本-55")

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   首次deploy时，没有部署第三方库时会自动下载并编译，耗时�能比较久，请�心等待。�续��新编译时，�会��下载编译，部署如上图所示。  
    >-   deploy时，需�选择与开��通信的主机侧ip，一般为虚拟网��置的ip。如果此ip和开��ip属于�网段，则会自动选择并部署。如果��网段，则需�手动输入与开��通信的主机侧ip�能完�deploy。  

4.  开始编译，打开Mindstudio工具，在工具�中点击**Build \> Build \> Build-Configuration**。会在目录下生�build和run文件夹。

    >![](public_sys-resources/icon-notice.gif) **须知：**   
    >首次编译工程时，**Build \> Build**为�色��点击状�。需�点击**Build \> Edit Build Configuration**，�置编译�数��进行编译。  

5.  将需�上色的图片上传至Host侧任一属组为HwHiAiUser用户的目录。

## �行<a name="section1620073406"></a>

1.  在Mindstudio工具的工具�中找到Run按钮，点击  **Run \> Run 'sample-colorization’**，如[图 程�已执行示�图](#fig18918132273612)所示，�执行程�已�在开��执行。

    **图 5**  程�已执行示�图<a name="fig18918132273612"></a>  
    ![](figures/程�已执行示�图-56.png "程�已执行示�图-56")

    以上报错信�请忽略，因为Mind Studio无法为�执行程�传�，上述步骤是将�执行程�与�赖的库文件部署到开�者�，此步骤需�ssh登录到开�者�至相应的目录文件下手动执行，具体请�考以下步骤。

2.  在Mind Studio所在Ubuntu�务器中，以HwHiAiUser用户SSH登录到Host侧。

    **ssh HwHiAiUser@**_host\_ip_

    对于Atlas 200 DK，host\_ip默认为192.168.1.2（USB连接）或者192.168.0.2（NIC连接）。

3.  进入黑白图�上色应用的�执行文件所在路径。

    命令举例如下：

    **cd \~/HIAI\_PROJECTS/workspace\_mind\_studio/sample-colorization\_xxx/out**

4.  执行应用程�。

    执行**run\_colorization.py**脚本会将推�生�的图片�存至指定路径。

    命令示例如下所示：

    **python3 run\_colorization.py -i \~/example.jpg -o ./out/**

    -   -i：输入图片的路径，�以是目录，表示当�目录下所有图片都作为输入；也�以指定具体图片。
    -   -o：上色�的图片�存路径


