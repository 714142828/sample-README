English|[中文](Readme_cn.md)

# Classification Network Application \(C++\)<a name="EN-US_TOPIC_0203223265"></a>

This application can run on the Atlas 200 DK or the AI acceleration cloud server to implement inference on a common classification network and output the first  _n_  inference results.

The applications in the current version branch adapt to  [DDK&RunTime](https://ascend.huawei.com/resources) **1.32.0.0 and later**.

## Prerequisites<a name="section137245294533"></a>

Before deploying this sample, ensure that:

-   Mind Studio  has been installed.
-   The Atlas 200 DK developer board has been connected to  Mind Studio, the cross compiler has been installed, the SD card has been prepared, and basic information has been configured.

## Software Preparation<a name="section181111827718"></a>

Before running the sample, obtain the source code package and configure the environment as follows:

1.  <a name="li953280133816"></a>Obtain the source code package.
    1.  By downloading the package

        Download the code in the  [https://github.com/Atlas200dk/sample-classification/tree/1-3x-0-0/](https://github.com/Atlas200dk/sample-classification/tree/1-3x-0-0/)  repository to any directory on the Ubuntu server where Mind Studio is located as the Mind Studio installation user. The two files must be stored in the same directory. For example, the code can be stored in  **$HOME/AscendProjects/sample-classification**.

    2.  By running the  **git**  command

        Run the following command in the  **$HOME/AscendProjects**  directory to download code:

        **git clone https://github.com/Atlas200dk/sample-classification.git --branch 1-3x-0-0**

2.  <a name="li29641938112018"></a>Obtain the source network model required by the application.

    Obtain the source network model and its weight file used in the application by referring to  [Table 1](#table1119094515272)  and save them to the same directory on Ubuntu Server where  Mind Studio  is located, for example,  **$HOME/models/classification**.

    **Table  1**  Models used in the general  **classification**  network application

    <a name="table1119094515272"></a>
    <table><thead align="left"><tr id="row677354502719"><th class="cellrowborder" valign="top" width="21%" id="mcps1.2.4.1.1"><p id="p167731845122717"><a name="p167731845122717"></a><a name="p167731845122717"></a>Model Name</p>
    </th>
    <th class="cellrowborder" valign="top" width="23%" id="mcps1.2.4.1.2"><p id="p277317459276"><a name="p277317459276"></a><a name="p277317459276"></a>Description</p>
    </th>
    <th class="cellrowborder" valign="top" width="56.00000000000001%" id="mcps1.2.4.1.3"><p id="p9773114512270"><a name="p9773114512270"></a><a name="p9773114512270"></a>Download Path</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row3122314144215"><td class="cellrowborder" valign="top" width="21%" headers="mcps1.2.4.1.1 "><p id="p14407251134314"><a name="p14407251134314"></a><a name="p14407251134314"></a>alexnet</p>
    </td>
    <td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.4.1.2 "><p id="p116141194720"><a name="p116141194720"></a><a name="p116141194720"></a>Image classification inference model.</p>
    <p id="p86191184712"><a name="p86191184712"></a><a name="p86191184712"></a>It is a AlexNet model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.00000000000001%" headers="mcps1.2.4.1.3 "><p id="p67311330479"><a name="p67311330479"></a><a name="p67311330479"></a>Download the source network model file and its weight file by referring to<strong id="b1034018421764"><a name="b1034018421764"></a><a name="b1034018421764"></a> README.md</strong> at <a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/alexnet" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/alexnet</a>.</p>
    </td>
    </tr>
    <tr id="row2399521134819"><td class="cellrowborder" valign="top" width="21%" headers="mcps1.2.4.1.1 "><p id="p3400192113488"><a name="p3400192113488"></a><a name="p3400192113488"></a>caffenet</p>
    </td>
    <td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.4.1.2 "><p id="p5645133234810"><a name="p5645133234810"></a><a name="p5645133234810"></a>Image classification inference model.</p>
    <p id="p14645153244816"><a name="p14645153244816"></a><a name="p14645153244816"></a>It is a CaffeNet model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.00000000000001%" headers="mcps1.2.4.1.3 "><p id="p1537844912482"><a name="p1537844912482"></a><a name="p1537844912482"></a>Download the source network model file and its weight file by referring to<strong id="b62781122719"><a name="b62781122719"></a><a name="b62781122719"></a> README.md</strong> at <a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/caffenet" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/caffenet</a>.</p>
    </td>
    </tr>
    <tr id="row3773114518271"><td class="cellrowborder" valign="top" width="21%" headers="mcps1.2.4.1.1 "><p id="p17738455277"><a name="p17738455277"></a><a name="p17738455277"></a>densenet</p>
    </td>
    <td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.4.1.2 "><p id="p16773124511270"><a name="p16773124511270"></a><a name="p16773124511270"></a>Image classification inference model.</p>
    <p id="p2773745162718"><a name="p2773745162718"></a><a name="p2773745162718"></a>It is a DenseNet121 model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.00000000000001%" headers="mcps1.2.4.1.3 "><p id="p187731945132715"><a name="p187731945132715"></a><a name="p187731945132715"></a>Download the source network model file and its weight file by referring to<strong id="b1799182010714"><a name="b1799182010714"></a><a name="b1799182010714"></a> README.md</strong> at <a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/densenet" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/densenet</a>.</p>
    </td>
    </tr>
    <tr id="row137731845122710"><td class="cellrowborder" valign="top" width="21%" headers="mcps1.2.4.1.1 "><p id="p477316457275"><a name="p477316457275"></a><a name="p477316457275"></a>googlenet</p>
    </td>
    <td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.4.1.2 "><p id="p197731456270"><a name="p197731456270"></a><a name="p197731456270"></a>Image classification inference model.</p>
    <p id="p1877394515274"><a name="p1877394515274"></a><a name="p1877394515274"></a>It is a GoogLeNet model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.00000000000001%" headers="mcps1.2.4.1.3 "><p id="p197738453275"><a name="p197738453275"></a><a name="p197738453275"></a>Download the source network model file and its weight file by referring to<strong id="b43191836877"><a name="b43191836877"></a><a name="b43191836877"></a> README.md</strong> at <a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/googlenet" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/googlenet</a>.</p>
    </td>
    </tr>
    <tr id="row977374512716"><td class="cellrowborder" valign="top" width="21%" headers="mcps1.2.4.1.1 "><p id="p1977324512272"><a name="p1977324512272"></a><a name="p1977324512272"></a>inception_v2</p>
    </td>
    <td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.4.1.2 "><p id="p14773445122712"><a name="p14773445122712"></a><a name="p14773445122712"></a>Image classification inference model.</p>
    <p id="p877311459270"><a name="p877311459270"></a><a name="p877311459270"></a>It is an Inception V2 model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.00000000000001%" headers="mcps1.2.4.1.3 "><p id="p16773145162719"><a name="p16773145162719"></a><a name="p16773145162719"></a>Download the source network model file and its weight file by referring to<strong id="b1689165415711"><a name="b1689165415711"></a><a name="b1689165415711"></a> README.md</strong> at <a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/inception_v2" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/inception_v2</a>.</p>
    </td>
    </tr>
    <tr id="row429165985115"><td class="cellrowborder" valign="top" width="21%" headers="mcps1.2.4.1.1 "><p id="p1050712711523"><a name="p1050712711523"></a><a name="p1050712711523"></a>inception_v3</p>
    </td>
    <td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.4.1.2 "><p id="p18641141115218"><a name="p18641141115218"></a><a name="p18641141115218"></a>Image classification inference model.</p>
    <p id="p06411511105213"><a name="p06411511105213"></a><a name="p06411511105213"></a>It is an Inception V3 model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.00000000000001%" headers="mcps1.2.4.1.3 "><p id="p1241971612520"><a name="p1241971612520"></a><a name="p1241971612520"></a>Download the source network model file and its weight file by referring to<strong id="b91541571817"><a name="b91541571817"></a><a name="b91541571817"></a> README.md</strong> at <a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/inception_v3" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/inception_v3</a>.</p>
    </td>
    </tr>
    <tr id="row6482142185210"><td class="cellrowborder" valign="top" width="21%" headers="mcps1.2.4.1.1 "><p id="p12508168115214"><a name="p12508168115214"></a><a name="p12508168115214"></a>inception_v4</p>
    </td>
    <td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.4.1.2 "><p id="p8785612105217"><a name="p8785612105217"></a><a name="p8785612105217"></a>Image classification inference model.</p>
    <p id="p47851512105212"><a name="p47851512105212"></a><a name="p47851512105212"></a>It is an Inception V4 model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.00000000000001%" headers="mcps1.2.4.1.3 "><p id="p1028761705212"><a name="p1028761705212"></a><a name="p1028761705212"></a>Download the source network model file and its weight file by referring to<strong id="b1192510212080"><a name="b1192510212080"></a><a name="b1192510212080"></a> README.md</strong> at <a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/inception_v4" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/inception_v4</a>.</p>
    </td>
    </tr>
    <tr id="row77732045152717"><td class="cellrowborder" valign="top" width="21%" headers="mcps1.2.4.1.1 "><p id="p0773114572715"><a name="p0773114572715"></a><a name="p0773114572715"></a>mobilenet_v1</p>
    </td>
    <td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.4.1.2 "><p id="p11774645162715"><a name="p11774645162715"></a><a name="p11774645162715"></a>Image classification inference model.</p>
    <p id="p47741455273"><a name="p47741455273"></a><a name="p47741455273"></a>It is a MobileNet V1 model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.00000000000001%" headers="mcps1.2.4.1.3 "><p id="p5586471511"><a name="p5586471511"></a><a name="p5586471511"></a>Download the source network model file and its weight file by referring to<strong id="b1788218341812"><a name="b1788218341812"></a><a name="b1788218341812"></a> README.md</strong> at <a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/mobilenet_v1" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/mobilenet_v1</a>.</p>
    </td>
    </tr>
    <tr id="row12774164515277"><td class="cellrowborder" valign="top" width="21%" headers="mcps1.2.4.1.1 "><p id="p187741345112718"><a name="p187741345112718"></a><a name="p187741345112718"></a>mobilenet_v2</p>
    </td>
    <td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.4.1.2 "><p id="p277414519274"><a name="p277414519274"></a><a name="p277414519274"></a>Image classification inference model.</p>
    <p id="p8774174502713"><a name="p8774174502713"></a><a name="p8774174502713"></a>It is a MobileNet V2 model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.00000000000001%" headers="mcps1.2.4.1.3 "><p id="p1677414514274"><a name="p1677414514274"></a><a name="p1677414514274"></a>Download the source network model file and its weight file by referring to<strong id="b45351545586"><a name="b45351545586"></a><a name="b45351545586"></a> README.md</strong> at <a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/mobilenet_v2" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/mobilenet_v2</a>.</p>
    </td>
    </tr>
    <tr id="row1577434516271"><td class="cellrowborder" valign="top" width="21%" headers="mcps1.2.4.1.1 "><p id="p3774194512713"><a name="p3774194512713"></a><a name="p3774194512713"></a>resnet18</p>
    </td>
    <td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.4.1.2 "><p id="p7774245122713"><a name="p7774245122713"></a><a name="p7774245122713"></a>Image classification inference model.</p>
    <p id="p577494517271"><a name="p577494517271"></a><a name="p577494517271"></a>It is a ResNet 18 model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.00000000000001%" headers="mcps1.2.4.1.3 "><p id="p16774144510270"><a name="p16774144510270"></a><a name="p16774144510270"></a>Download the source network model file and its weight file by referring to<strong id="b1728815118918"><a name="b1728815118918"></a><a name="b1728815118918"></a> README.md</strong> at <a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/resnet18" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/resnet18</a>.</p>
    </td>
    </tr>
    <tr id="row377414452276"><td class="cellrowborder" valign="top" width="21%" headers="mcps1.2.4.1.1 "><p id="p10774545142714"><a name="p10774545142714"></a><a name="p10774545142714"></a>resnet50</p>
    </td>
    <td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.4.1.2 "><p id="p97741245142712"><a name="p97741245142712"></a><a name="p97741245142712"></a>Image classification inference model.</p>
    <p id="p177412456271"><a name="p177412456271"></a><a name="p177412456271"></a>It is a ResNet 50 model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.00000000000001%" headers="mcps1.2.4.1.3 "><p id="p57747459272"><a name="p57747459272"></a><a name="p57747459272"></a>Download the source network model file and its weight file by referring to<strong id="b135771417991"><a name="b135771417991"></a><a name="b135771417991"></a> README.md</strong> at <a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/resnet50" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/resnet50</a>.</p>
    </td>
    </tr>
    <tr id="row377484514279"><td class="cellrowborder" valign="top" width="21%" headers="mcps1.2.4.1.1 "><p id="p1777454516275"><a name="p1777454516275"></a><a name="p1777454516275"></a>resnet101</p>
    </td>
    <td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.4.1.2 "><p id="p15774124516274"><a name="p15774124516274"></a><a name="p15774124516274"></a>Image classification inference model.</p>
    <p id="p7774134552720"><a name="p7774134552720"></a><a name="p7774134552720"></a>It is a ResNet 101 model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.00000000000001%" headers="mcps1.2.4.1.3 "><p id="p117741545132710"><a name="p117741545132710"></a><a name="p117741545132710"></a>Download the source network model file and its weight file by referring to<strong id="b1586253018915"><a name="b1586253018915"></a><a name="b1586253018915"></a> README.md</strong> at <a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/resnet101" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/resnet101</a>.</p>
    </td>
    </tr>
    <tr id="row14774154513279"><td class="cellrowborder" valign="top" width="21%" headers="mcps1.2.4.1.1 "><p id="p1077413452272"><a name="p1077413452272"></a><a name="p1077413452272"></a>resnet152</p>
    </td>
    <td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.4.1.2 "><p id="p177434517275"><a name="p177434517275"></a><a name="p177434517275"></a>Image classification inference model.</p>
    <p id="p877515459276"><a name="p877515459276"></a><a name="p877515459276"></a>It is a ResNet 152 model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.00000000000001%" headers="mcps1.2.4.1.3 "><p id="p777514582712"><a name="p777514582712"></a><a name="p777514582712"></a>Download the source network model file and its weight file by referring to<strong id="b749519434920"><a name="b749519434920"></a><a name="b749519434920"></a> README.md</strong> at <a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/resnet152" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/resnet152</a>.</p>
    </td>
    </tr>
    <tr id="row37752450270"><td class="cellrowborder" valign="top" width="21%" headers="mcps1.2.4.1.1 "><p id="p977544513278"><a name="p977544513278"></a><a name="p977544513278"></a>vgg16</p>
    </td>
    <td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.4.1.2 "><p id="p1177514522713"><a name="p1177514522713"></a><a name="p1177514522713"></a>Image classification inference model.</p>
    <p id="p10775194582713"><a name="p10775194582713"></a><a name="p10775194582713"></a>It is a VGG16 model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.00000000000001%" headers="mcps1.2.4.1.3 "><p id="p18775124582720"><a name="p18775124582720"></a><a name="p18775124582720"></a>Download the source network model file and its weight file by referring to<strong id="b19172155512916"><a name="b19172155512916"></a><a name="b19172155512916"></a> README.md</strong> at <a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/vgg16" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/vgg16</a>.</p>
    </td>
    </tr>
    <tr id="row2775194518272"><td class="cellrowborder" valign="top" width="21%" headers="mcps1.2.4.1.1 "><p id="p5775154516272"><a name="p5775154516272"></a><a name="p5775154516272"></a>vgg19</p>
    </td>
    <td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.4.1.2 "><p id="p0775204532711"><a name="p0775204532711"></a><a name="p0775204532711"></a>Image classification inference model.</p>
    <p id="p1477554519275"><a name="p1477554519275"></a><a name="p1477554519275"></a>It is a VGG19 model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.00000000000001%" headers="mcps1.2.4.1.3 "><p id="p777554542713"><a name="p777554542713"></a><a name="p777554542713"></a>Download the source network model file and its weight file by referring to<strong id="b1268419531013"><a name="b1268419531013"></a><a name="b1268419531013"></a> README.md</strong> at <a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/vgg19" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/vgg19</a>.</p>
    </td>
    </tr>
    <tr id="row17513194404914"><td class="cellrowborder" valign="top" width="21%" headers="mcps1.2.4.1.1 "><p id="p7513164419495"><a name="p7513164419495"></a><a name="p7513164419495"></a>squeezenet</p>
    </td>
    <td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.4.1.2 "><p id="p1315111145015"><a name="p1315111145015"></a><a name="p1315111145015"></a>Image classification inference model.</p>
    <p id="p1515131114501"><a name="p1515131114501"></a><a name="p1515131114501"></a>It is a SqueezeNet model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.00000000000001%" headers="mcps1.2.4.1.3 "><p id="p16265437125015"><a name="p16265437125015"></a><a name="p16265437125015"></a>Download the source network model file and its weight file by referring to<strong id="b12997191414105"><a name="b12997191414105"></a><a name="b12997191414105"></a> README.md</strong> at <a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/squeezenet" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/squeezenet</a>.</p>
    </td>
    </tr>
    <tr id="row17757454270"><td class="cellrowborder" valign="top" width="21%" headers="mcps1.2.4.1.1 "><p id="p17759452279"><a name="p17759452279"></a><a name="p17759452279"></a>dpn98</p>
    </td>
    <td class="cellrowborder" valign="top" width="23%" headers="mcps1.2.4.1.2 "><p id="p4775545162716"><a name="p4775545162716"></a><a name="p4775545162716"></a>Image classification inference model.</p>
    <p id="p1577504516278"><a name="p1577504516278"></a><a name="p1577504516278"></a>It is a DPN-98 model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.00000000000001%" headers="mcps1.2.4.1.3 "><p id="p19776154592711"><a name="p19776154592711"></a><a name="p19776154592711"></a>Download the source network model file and its weight file by referring to<strong id="b1087911266106"><a name="b1087911266106"></a><a name="b1087911266106"></a> README.md</strong> at <a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/dpn98" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/dpn98</a>.</p>
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
        -   Select the model file downloaded in  [Step 2](#li29641938112018)  for  **Model File**. The weight file is automatically matched and filled in  **Weight File**.
        -   Set  **Model Name**  to the model name in  [Table 1](#table1119094515272).

            ![](figures/en-us_image_0208264607.png)

        -   For the GoogleNet and Inception\_v2 models, a general classification network application processes one image at a time. Therefore, the value of  **N**  in  **Input Node: data**  must be set to  **1**  during conversion, as shown in  [Figure 2](#fig95695336322). In the  **AIPP**  configuration, set  **Input Image Size**  to  **256**  and  **224**, respectively. In this sample, the value must be 128 x 16 aligned. Set  **Model Image Format**  to  **BGR888\_U8**, as shown in  [Figure 3](#fig14632122193310).

            **Figure  2**  Nodes configuration example<a name="fig95695336322"></a>  
            ![](figures/nodes-configuration-example.png "nodes-configuration-example")

            **Figure  3**  AIPP configuration example<a name="fig14632122193310"></a>  
            ![](figures/aipp-configuration-example.png "aipp-configuration-example")

    3.  Click  **OK**  to start model conversion.

        After successful conversion, an .om offline model is generated in the  **$HOME/modelzoo/XXX/device**  directory.

    >![](public_sys-resources/icon-note.gif) **NOTE:**   
    >-   For details about the descriptions of each step and parameters in model conversion on Mind Studio, see "Model Conversion" in the  [Mind Studio User Guide](https://ascend.huawei.com/doc/mindstudio/).  
    >-   **XXX**  indicates the name of the model to be converted. For example,  **googlenet.om**  is stored in  **$HOME/modelzoo/googlenet/device**.  

5.  <a name="li470213205618"></a>Upload the converted .om model file to the  **sample-classification/script**  directory under the source code path in  [Step 1](#li953280133816).

## Build<a name="section18931344873"></a>

1.  Open the project.

    Go to the directory that stores the decompressed installation package as the Mind Studio installation user in CLI mode, for example,  **$HOME/MindStudio-ubuntu/bin**. Run the following command to start Mind Studio:

    **./MindStudio.sh**

    Open the  **sample-classification**  project, as shown in  [Figure 4](#fig11106241192810).

    **Figure  4**  Opening the classification project<a name="fig11106241192810"></a>  
    ![](figures/opening-the-classification-project.png "opening-the-classification-project")

2.  Configure project information in the  **src/param\_configure.conf**  file.

    **Figure  5**  Configuration file path<a name="fig0391184062214"></a>  
    ![](figures/configuration-file-path-13.png "configuration-file-path-13")

    Content of the configuration file:

    ```
    remote_host=
    model_name=
    ```

    Parameter settings to be manually added:

    -   **remote\_host**: IP address of the Atlas 200 DK developer board
    -   **model\_name**: offline model name

    Configuration example:

    ```
    remote_host=192.168.1.2
    model_name=googlenet.om
    ```

    >![](public_sys-resources/icon-note.gif) **NOTE:**   
    >-   All the three parameters must be set. Otherwise, the build fails.  
    >-   Do not use double quotation marks \(""\) during parameter settings.  
    >-   Only one model name can be typed into the configuration file. The typed model must be one of the models stored in  [Step 5](#li470213205618). GoogleNet is used as an example. You can use any of other models listed in this sample and execute it by performing the preceding steps.  

3.  Run the  **deploy.sh**  script to adjust configuration parameters and download and compile the third-party library. Open the  **Terminal**  window of Mind Studio. By default, the home directory of the code is used. Run the  **deploy.sh**  script in the background to deploy the environment, as shown in  [Figure 6](#fig478266192619).

    **Figure  6**  Running the deploy.sh script<a name="fig478266192619"></a>  
    ![](figures/running-the-deploy-sh-script-14.png "running-the-deploy-sh-script-14")

    >![](public_sys-resources/icon-note.gif) **NOTE:**   
    >-   During the first deployment, if no third-party library is used, the system automatically downloads and builds the third-party library, which may take a long time. The third-party library can be directly used for the subsequent build.  
    >-   During deployment, select the IP address of the host that communicates with the developer board. Generally, the IP address is the IP address configured for the virtual NIC. If the IP address is in the same network segment as the IP address of the developer board, it is automatically selected for deployment. If they are not in the same network segment, you need to manually type the IP address of the host that communicates with the Atlas DK to complete the deployment.  

4.  Start building. Open Mind Studio and choose  **Build \> Build \> Build-Configuration**  from the main menu. The  **build**  and  **run**  folders are generated in the directory, as shown in  [Figure 7](#fig1741464713019).

    **Figure  7**  Build and file generating<a name="fig1741464713019"></a>  
    ![](figures/build-and-file-generating-15.png "build-and-file-generating-15")

    >![](public_sys-resources/icon-notice.gif) **NOTICE:**   
    >When you build a project for the first time,  **Build \> Build**  is unavailable. You need to choose  **Build \> Edit Build Configuration**  to set parameters before the build.  

5.  Upload the images to be inferred to any directory of the  **HwHiAiUser**  user on the host side.

    The image requirements are as follows:

    -   Format: jpg, png, and bmp
    -   Width of the input image: an integer ranging from 16px to 4096px
    -   Height of the input image: an integer ranging from 16px to 4096px


## Run<a name="section372782554919"></a>

1.  On the toolbar of Mind Studio, click  **Run**  and choose  **Run \> Run 'sample-classification'**. As shown in  [Figure 8](#fig93931954162719), the executable application is running on the developer board.

    **Figure  8**  Running application<a name="fig93931954162719"></a>  
    ![](figures/running-application.png "running-application")

    You can ignore the error information reported during the execution because Mind Studio cannot transfer parameters for an executable application. In the preceding steps, the executable application and dependent library files are deployed to the developer board. You need to log in to the developer board in SSH mode and manually execute the files in the corresponding directory. For details, see the following steps.

2.  Log in to the host side as the  **HwHiAiUser**  user in SSH mode on Ubuntu Server where  Mind Studio  is located.

    **ssh HwHiAiUser@**_host\_ip_

    For the Atlas 200 DK, the default value of  _**host\_ip**_  is  **192.168.1.2**  \(USB connection mode\) or  **192.168.0.2**  \(NIC connection mode\).

3.  Go to the path of the executable files of the classification network application.

    **cd \~/HIAI\_PROJECTS/ascend\_workspace/classification/out**

4.  Run the application.

    Run the  **run\_classification.py**  script to print the inference result on the execution terminal.

    Command example:

    **python3 run\_classification.py -w  _224_  -h  _224_  -i** **_./example.jpg_  -n  _10_**

    -   **-w/model\_width**: width of the input image of a model. The value is an integer ranging from 16px to 4096px. Obtain the input width and height required by each model by referring to the README file of each model file on Gitee. For details, see  [Table 1](#table1119094515272).
    -   **-h/model\_height**: height of the input image of a model. The value is an integer ranging from 16px to 4096px. Obtain the input width and height required by each model by referring to the README file of each model file on Gitee. For details, see  [Table 1](#table1119094515272).
    -   **-i/input\_path**: path of the input image. It can be a directory, indicating that all images in the current directory are used as input. \(Multiple inputs can be specified\).
    -   **-n/top\_n**: the first  _n_  inference results that are output

    For other parameters, run the  **python3 run\_classification.py --help**  command to check help information.


