English|[中文](Readme.md)

# Black and White Image Colorization<a name="EN-US_TOPIC_0219108795"></a>

This application runs on the Atlas 200 DK to automatically color black and white images.

The applications in the current version branch adapt to  [DDK&RunTime](https://ascend.huawei.com/resources) **1.32.0.0 and later**.

## Prerequisites<a name="section137245294533"></a>

Before deploying this sample, ensure that:

-   Mind Studio  has been installed.
-   The Atlas 200 DK developer board has been connected to  Mind Studio, the cross compiler has been installed, the SD card has been prepared, and basic information has been configured.

## Software Preparation<a name="section181111827718"></a>

Before running the sample, obtain the source code package and configure the environment as follows:

1.  <a name="li953280133816"></a>Obtain the source code package.
    1.  By downloading the package

        Download the code in the  [https://gitee.com/Atlas200DK/sample-colorization/tree/1.3x.0.0/](https://gitee.com/Atlas200DK/sample-colorization/tree/1.3x.0.0/)  repository to any directory on the Ubuntu server where Mind Studio is located as the Mind Studio installation user. The two files must be stored in the same directory. For example, the code can be stored in  **$HOME/AscendProjects/sample-colorization**.

    2.  By running the  **git**  command

        Run the following command in the  **$HOME/AscendProjects**  directory to download code:

        **git clone https://gitee.com/Atlas200DK/sample-colorization.git --branch 1.3x.0.0**

2.  <a name="li2074865610364"></a>Obtain the source network model required by the application.

    Obtain the source network model and its weight file used in the application by referring to  [Table 1](#table19942111763710)  and save them to the same directory on Ubuntu Server where  Mind Studio  is located, for example,  **$HOME/models/colorization**.

    **Table  1**  Model used in the black and white image colorization application

    <a name="table19942111763710"></a>
    <table><thead align="left"><tr id="row611318123710"><th class="cellrowborder" valign="top" width="18%" id="mcps1.2.4.1.1"><p id="p81141820376"><a name="p81141820376"></a><a name="p81141820376"></a>Model Name</p>
    </th>
    <th class="cellrowborder" valign="top" width="19%" id="mcps1.2.4.1.2"><p id="p13181823711"><a name="p13181823711"></a><a name="p13181823711"></a>Description</p>
    </th>
    <th class="cellrowborder" valign="top" width="63%" id="mcps1.2.4.1.3"><p id="p1717182378"><a name="p1717182378"></a><a name="p1717182378"></a>Download Path</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row1119187377"><td class="cellrowborder" valign="top" width="18%" headers="mcps1.2.4.1.1 "><p id="p4745165253920"><a name="p4745165253920"></a><a name="p4745165253920"></a>colorization</p>
    </td>
    <td class="cellrowborder" valign="top" width="19%" headers="mcps1.2.4.1.2 "><p id="p1874515218391"><a name="p1874515218391"></a><a name="p1874515218391"></a>Black and white image colorization model</p>
    </td>
    <td class="cellrowborder" valign="top" width="63%" headers="mcps1.2.4.1.3 "><p id="p611318163718"><a name="p611318163718"></a><a name="p611318163718"></a>Download the source network model file and its weight file by referring to <strong id="b1666913346147"><a name="b1666913346147"></a><a name="b1666913346147"></a>README.md</strong> at <a href="https://gitee.com/HuaweiAscend/models/tree/master/computer_vision/object_detect/colorization" target="_blank" rel="noopener noreferrer">https://gitee.com/HuaweiAscend/models/tree/master/computer_vision/object_detect/colorization</a>.</p>
    </td>
    </tr>
    </tbody>
    </table>

3.  Log in to Ubuntu Server where Mind Studio is located as the Mind Studio installation user, determine the current DDK version number, and set the environment variables  **DDK\_HOME**,  **tools\_version**,  **LD\_LIBRARY\_PATH**.
    1.  <a name="en-us_topic_0203223294_li61417158198"></a>Query the current DDK version number.

        A DDK version number can be queried by using either Mind Studio or the DDK software package.

        -   Using Mind Studio

            On the project page of Mind Studio, choose  **File \> Settings \> System Settings \> Ascend DDK**  to access  [Querying the DDK version number](#en-us_topic_0203223294_fig17553193319118).

            **Figure  1**  Querying the DDK version number<a name="en-us_topic_0203223294_fig17553193319118"></a>  
            ![](figures/querying-the-ddk-version-number.png "querying-the-ddk-version-number")

            The displayed  **DDK Version**  is the current DDK version number, for example,  **1.31.T15.B150**.

        -   Using the DDK software package

            Obtain the DDK version number based on the DDK package name.

            DDK package name format:  **Ascend\_DDK-\{software version\}-\{interface version\}-x86\_64.ubuntu16.04.tar.gz**

            _Software version_  indicates the DDK software version number.

            For example:

            If the DDK package name is  **Ascend\_DDK-1.31.T15.B150-1.1.1-x86\_64.ubuntu16.04.tar.gz**, the DDK version is  **1.31.T15.B150**.

    2.  Set environment variables.

        **vim \~/.bashrc**

        Run the following commands to add the environment variables  **DDK\_HOME**  and  **LD\_LIBRARY\_PATH**  to the last line:

        **export tools\_version=_1.31.X.X_**

        **export DDK\_HOME=\\$HOME/.mindstudio/huawei/ddk/\\$tools\_version/ddk**

        **export LD\_LIBRARY\_PATH=$DDK\_HOME/lib/x86\_64-linux-gcc5.4**

        >![](public_sys-resources/icon-note.gif) **NOTE:**   
        >-   **_1.31.X.X_**  indicates the DDK version queried in  [a](#en-us_topic_0203223294_li61417158198). Set this parameter based on the query result, for example,  **1.31.T15.B150**.  
        >-   If the environment variables have been added, skip this step.  

        Type  **:wq!**  to save settings and exit.

        Run the following command for the environment variable to take effect:

        **source \~/.bashrc**

4.  Convert the source network model to a model supported by the Ascend AI processor.
    1.  Choose  **Tools \> Model Convert**  from the main menu of  Mind Studio.
    2.  On the  **Model Conversion**  page that is displayed, configure model conversion.
        -   Select the model file downloaded in  [Step 2](#li2074865610364)  for  **Model File**. The weight file is automatically matched and filled in  **Weight File**.
        -   Set  **Model Name**  to the model name  **colorization**  in  [Table 1](#table19942111763710).

            ![](figures/en-us_image_0219108879.png)

        -   The input shape of the colorization model is \(1,3,224,224\). Therefore, the input node parameters must be set to  **1**,  **3**,  **224**, and  **224**  accordingly.

            ![](figures/en-us_image_0219108881.png)

        -   The model input is from channel L of normalized lab images. Therefore, AIPP needs to be disabled.

            ![](figures/en-us_image_0219108885.png)

    3.  Click  **Finish**  to start model conversion.

        After successful conversion, an .om offline model is generated in the  **$HOME/modelzoo/colorization/device**  directory.

        >![](public_sys-resources/icon-note.gif) **NOTE:**   
        >For details about the descriptions of each step and parameters in model conversion, see "Model Conversion" in the  [Mind Studio User Guide](https://ascend.huawei.com/doc/mindstudio/).  


5.  Upload the converted .om model file to the  **sample\_colorization/script**  directory under the source code path in  [Step 1](#li953280133816).

## Build<a name="section3723145213347"></a>

1.  Open the project.

    Go to the directory that stores the decompressed installation package as the Mind Studio installation user in CLI mode, for example,  **$HOME/MindStudio-ubuntu/bin**. Run the following command to start Mind Studio:

    **./MindStudio.sh**

    Open the  **sample\_colorization**  project, as shown in  [Figure 2](#fig05481157171918).

    **Figure  2**  Opening the sample\_colorization project<a name="fig05481157171918"></a>  
    

    ![](figures/en-us_image_0219108999.png)

2.  Configure project information in the  **src/param\_configure.conf**  file.

    **Figure  3**  Configuration file path<a name="fig0391184062214"></a>  
    ![](figures/configuration-file-path-52.png "configuration-file-path-52")

    Content of the configuration file:

    ```
    remote_host=
    ```

    Parameter settings to be manually added:

    **remote\_host**: IP address of the Atlas 200 DK developer board

    Configuration example:

    ```
    remote_host=192.168.1.2
    ```

    >![](public_sys-resources/icon-note.gif) **NOTE:**   
    >-   Do not use double quotation marks \(""\) during parameter settings.  

3.  Run the  **deploy.sh**  script to adjust configuration parameters and download and compile the third-party library. Open the  **Terminal**  window of Mind Studio. By default, the home directory of the code is used. Run the  **deploy.sh**  script in the background to deploy the environment, as shown in  [Figure 4](#fig63536151461).

    **Figure  4**  Running the deploy.sh script<a name="fig63536151461"></a>  
    ![](figures/running-the-deploy-sh-script-53.png "running-the-deploy-sh-script-53")

    >![](public_sys-resources/icon-note.gif) **NOTE:**   
    >-   During the first deployment, if no third-party library is used, the system automatically downloads and builds the third-party library, which may take a long time. The third-party library can be directly used for the subsequent build.  
    >-   During deployment, select the IP address of the host that communicates with the developer board. Generally, the IP address is the IP address configured for the virtual NIC. If the IP address is in the same network segment as the IP address of the developer board, it is automatically selected for deployment. If they are not in the same network segment, you need to manually type the IP address of the host that communicates with the Atlas DK to complete the deployment.  

4.  Start building. Open Mind Studio and choose  **Build \> Build \> Build-Configuration**  from the main menu. The  **build**  and  **run**  folders are generated in the directory.

    >![](public_sys-resources/icon-notice.gif) **NOTICE:**   
    >When you build a project for the first time,  **Build \> Build**  is unavailable. You need to choose  **Build \> Edit Build Configuration**  to set parameters before the build.  

5.  Upload the images to be colored to any directory of the  **HwHiAiUser**  user on the host side.

## Run<a name="section1620073406"></a>

1.  On the toolbar of Mind Studio, click  **Run**  and choose  **Run \> Run 'sample-colorization'**. As shown in  [Figure 5](#fig18918132273612), the executable application is running on the developer board.

    **Figure  5**  Running application<a name="fig18918132273612"></a>  
    ![](figures/running-application-54.png "running-application-54")

    You can ignore the error information reported during the execution because Mind Studio cannot transfer parameters for an executable application. In the preceding steps, the executable application and dependent library files are deployed to the developer board. You need to log in to the developer board in SSH mode and manually execute the files in the corresponding directory. For details, see the following steps.

2.  Log in to the host side as the  **HwHiAiUser**  user in SSH mode on Ubuntu Server where  Mind Studio  is located.

    **ssh HwHiAiUser@**_host\_ip_

    For the Atlas 200 DK, the default value of  _**host\_ip**_  is  **192.168.1.2**  \(USB connection mode\) or  **192.168.0.2**  \(NIC connection mode\).

3.  Go to the path of the executable file of the black and white image colorization application.

    Command example:

    **cd \~/HIAI\_PROJECTS/workspace\_mind\_studio/sample-colorization\_xxx/out**

4.  Run the application.

    Run the  **run\_colorization.py**  script to save the images which are generated by inference to the specified path.

    Command example:

    **python3 run\_colorization.py -i \~/example.jpg -o ./out/**

    -   **-i**: path of the input image. The value can be a directory, indicating that all images in the current directory are used as input. The value can also be used to specify an image.
    -   **-o**: path for storing the colored images.


