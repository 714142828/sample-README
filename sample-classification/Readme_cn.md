中文|[English](Readme.md)

# 分类网络应用（C++）<a name="ZH-CN_TOPIC_0203223265"></a>

本Application支��行在Atlas 200 DK或者AI加速云�务器上，实现了对常�的分类网络的推�功能并输出�n个推�结果。

当�分支中的应用适�**1.32.0.0�以上**版本的[DDK&RunTime](https://ascend.huawei.com/resources)。

## ���件<a name="section137245294533"></a>

部署此Sample�，需�准备好以下环境：

-   已完�Mind Studio的安装。
-   已完�Atlas 200 DK开�者�与Mind Studio的连接，交�编译器的安装，SD�的制作�基本信�的�置等。

## 软件准备<a name="section181111827718"></a>

�行此Sample�，需�按照此章节获���包，并进行相关的环境�置。

1.  <a name="li953280133816"></a>获���包。
    1.  下载压缩包方�获�。

        将[https://github.com/Atlas200dk/sample-classification/tree/1-3x-0-0/](https://github.com/Atlas200dk/sample-classification/tree/1-3x-0-0/)仓中的代�以Mind Studio安装用户下载至Mind Studio所在Ubuntu�务器的任�目录，这两个文件必须存放到�一个目录下。例如代�存放路径为：$HOME/AscendProjects/sample-classification。

    2.  命令行使用git命令方�获�。

        在命令行中：$HOME/AscendProjects目录下执行以下命令下载代�。

        **git clone https://github.com/Atlas200dk/sample-classification.git --branch 1-3x-0-0**

2.  <a name="li29641938112018"></a>获�此应用中所需�的原始网络模型。

    �考[表1](#table1119094515272)获�此应用中所用到的原始网络模型�其对应的��文件，并将其存放到Mind Studio所在Ubuntu�务器的任�目录，这两个文件必须存放到�一个目录下。例如：$HOME/models/classification。

    **表 1**  通用分类网络应用使用模型

    <a name="table1119094515272"></a>
    <table><thead align="left"><tr id="row677354502719"><th class="cellrowborder" valign="top" width="12.85%" id="mcps1.2.4.1.1"><p id="p167731845122717"><a name="p167731845122717"></a><a name="p167731845122717"></a>模型�称</p>
    </th>
    <th class="cellrowborder" valign="top" width="12.57%" id="mcps1.2.4.1.2"><p id="p277317459276"><a name="p277317459276"></a><a name="p277317459276"></a>模型说明</p>
    </th>
    <th class="cellrowborder" valign="top" width="74.58%" id="mcps1.2.4.1.3"><p id="p9773114512270"><a name="p9773114512270"></a><a name="p9773114512270"></a>模型下载路径</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row3122314144215"><td class="cellrowborder" valign="top" width="12.85%" headers="mcps1.2.4.1.1 "><p id="p14407251134314"><a name="p14407251134314"></a><a name="p14407251134314"></a>alexnet</p>
    </td>
    <td class="cellrowborder" valign="top" width="12.57%" headers="mcps1.2.4.1.2 "><p id="p116141194720"><a name="p116141194720"></a><a name="p116141194720"></a>图片分类推�模型。</p>
    <p id="p86191184712"><a name="p86191184712"></a><a name="p86191184712"></a>是基于Caffe的AlexNet模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="74.58%" headers="mcps1.2.4.1.3 "><p id="p67311330479"><a name="p67311330479"></a><a name="p67311330479"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/alexnet" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/alexnet</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    <tr id="row2399521134819"><td class="cellrowborder" valign="top" width="12.85%" headers="mcps1.2.4.1.1 "><p id="p3400192113488"><a name="p3400192113488"></a><a name="p3400192113488"></a>caffenet</p>
    </td>
    <td class="cellrowborder" valign="top" width="12.57%" headers="mcps1.2.4.1.2 "><p id="p5645133234810"><a name="p5645133234810"></a><a name="p5645133234810"></a>图片分类推�模型。</p>
    <p id="p14645153244816"><a name="p14645153244816"></a><a name="p14645153244816"></a>是基于Caffe的CaffeNet模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="74.58%" headers="mcps1.2.4.1.3 "><p id="p1537844912482"><a name="p1537844912482"></a><a name="p1537844912482"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/caffenet" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/caffenet</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    <tr id="row3773114518271"><td class="cellrowborder" valign="top" width="12.85%" headers="mcps1.2.4.1.1 "><p id="p17738455277"><a name="p17738455277"></a><a name="p17738455277"></a>densenet</p>
    </td>
    <td class="cellrowborder" valign="top" width="12.57%" headers="mcps1.2.4.1.2 "><p id="p16773124511270"><a name="p16773124511270"></a><a name="p16773124511270"></a>图片分类推�模型。</p>
    <p id="p2773745162718"><a name="p2773745162718"></a><a name="p2773745162718"></a>是基于Caffe的DenseNet121模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="74.58%" headers="mcps1.2.4.1.3 "><p id="p187731945132715"><a name="p187731945132715"></a><a name="p187731945132715"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/densenet" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/densenet</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    <tr id="row137731845122710"><td class="cellrowborder" valign="top" width="12.85%" headers="mcps1.2.4.1.1 "><p id="p477316457275"><a name="p477316457275"></a><a name="p477316457275"></a>googlenet</p>
    </td>
    <td class="cellrowborder" valign="top" width="12.57%" headers="mcps1.2.4.1.2 "><p id="p197731456270"><a name="p197731456270"></a><a name="p197731456270"></a>图片分类推�模型。</p>
    <p id="p1877394515274"><a name="p1877394515274"></a><a name="p1877394515274"></a>是基于Caffe的GoogLeNet模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="74.58%" headers="mcps1.2.4.1.3 "><p id="p197738453275"><a name="p197738453275"></a><a name="p197738453275"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/googlenet" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/googlenet</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    <tr id="row977374512716"><td class="cellrowborder" valign="top" width="12.85%" headers="mcps1.2.4.1.1 "><p id="p1977324512272"><a name="p1977324512272"></a><a name="p1977324512272"></a><span>inception_v2</span></p>
    </td>
    <td class="cellrowborder" valign="top" width="12.57%" headers="mcps1.2.4.1.2 "><p id="p14773445122712"><a name="p14773445122712"></a><a name="p14773445122712"></a>图片分类推�模型。</p>
    <p id="p877311459270"><a name="p877311459270"></a><a name="p877311459270"></a>是基于Caffe的Inception V2模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="74.58%" headers="mcps1.2.4.1.3 "><p id="p16773145162719"><a name="p16773145162719"></a><a name="p16773145162719"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/inception_v2" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/inception_v2</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    <tr id="row429165985115"><td class="cellrowborder" valign="top" width="12.85%" headers="mcps1.2.4.1.1 "><p id="p1050712711523"><a name="p1050712711523"></a><a name="p1050712711523"></a><span>inception_v3</span></p>
    </td>
    <td class="cellrowborder" valign="top" width="12.57%" headers="mcps1.2.4.1.2 "><p id="p18641141115218"><a name="p18641141115218"></a><a name="p18641141115218"></a>图片分类推�模型。</p>
    <p id="p06411511105213"><a name="p06411511105213"></a><a name="p06411511105213"></a>是基于Caffe的Inception V3模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="74.58%" headers="mcps1.2.4.1.3 "><p id="p1241971612520"><a name="p1241971612520"></a><a name="p1241971612520"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/inception_v3" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/inception_v3</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    <tr id="row6482142185210"><td class="cellrowborder" valign="top" width="12.85%" headers="mcps1.2.4.1.1 "><p id="p12508168115214"><a name="p12508168115214"></a><a name="p12508168115214"></a><span>inception_v4</span></p>
    </td>
    <td class="cellrowborder" valign="top" width="12.57%" headers="mcps1.2.4.1.2 "><p id="p8785612105217"><a name="p8785612105217"></a><a name="p8785612105217"></a>图片分类推�模型。</p>
    <p id="p47851512105212"><a name="p47851512105212"></a><a name="p47851512105212"></a>是基于Caffe的Inception V4模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="74.58%" headers="mcps1.2.4.1.3 "><p id="p1028761705212"><a name="p1028761705212"></a><a name="p1028761705212"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/inception_v4" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/inception_v4</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    <tr id="row77732045152717"><td class="cellrowborder" valign="top" width="12.85%" headers="mcps1.2.4.1.1 "><p id="p0773114572715"><a name="p0773114572715"></a><a name="p0773114572715"></a><span>mobilenet_v1</span></p>
    </td>
    <td class="cellrowborder" valign="top" width="12.57%" headers="mcps1.2.4.1.2 "><p id="p11774645162715"><a name="p11774645162715"></a><a name="p11774645162715"></a>图片分类推�模型。</p>
    <p id="p47741455273"><a name="p47741455273"></a><a name="p47741455273"></a>是基于Caffe的MobileNet V1模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="74.58%" headers="mcps1.2.4.1.3 "><p id="p5586471511"><a name="p5586471511"></a><a name="p5586471511"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/mobilenet_v1" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/mobilenet_v1</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    <tr id="row12774164515277"><td class="cellrowborder" valign="top" width="12.85%" headers="mcps1.2.4.1.1 "><p id="p187741345112718"><a name="p187741345112718"></a><a name="p187741345112718"></a><span>mobilenet_v2</span></p>
    </td>
    <td class="cellrowborder" valign="top" width="12.57%" headers="mcps1.2.4.1.2 "><p id="p277414519274"><a name="p277414519274"></a><a name="p277414519274"></a>图片分类推�模型。</p>
    <p id="p8774174502713"><a name="p8774174502713"></a><a name="p8774174502713"></a>是基于Caffe的MobileNet V2模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="74.58%" headers="mcps1.2.4.1.3 "><p id="p1677414514274"><a name="p1677414514274"></a><a name="p1677414514274"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/mobilenet_v2" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/mobilenet_v2</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    <tr id="row1577434516271"><td class="cellrowborder" valign="top" width="12.85%" headers="mcps1.2.4.1.1 "><p id="p3774194512713"><a name="p3774194512713"></a><a name="p3774194512713"></a><span>resnet18</span></p>
    </td>
    <td class="cellrowborder" valign="top" width="12.57%" headers="mcps1.2.4.1.2 "><p id="p7774245122713"><a name="p7774245122713"></a><a name="p7774245122713"></a>图片分类推�模型。</p>
    <p id="p577494517271"><a name="p577494517271"></a><a name="p577494517271"></a>是基于Caffe的ResNet 18模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="74.58%" headers="mcps1.2.4.1.3 "><p id="p16774144510270"><a name="p16774144510270"></a><a name="p16774144510270"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/resnet18" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/resnet18</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    <tr id="row377414452276"><td class="cellrowborder" valign="top" width="12.85%" headers="mcps1.2.4.1.1 "><p id="p10774545142714"><a name="p10774545142714"></a><a name="p10774545142714"></a><span>resnet50</span></p>
    </td>
    <td class="cellrowborder" valign="top" width="12.57%" headers="mcps1.2.4.1.2 "><p id="p97741245142712"><a name="p97741245142712"></a><a name="p97741245142712"></a>图片分类推�模型。</p>
    <p id="p177412456271"><a name="p177412456271"></a><a name="p177412456271"></a>是基于Caffe的ResNet 50模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="74.58%" headers="mcps1.2.4.1.3 "><p id="p57747459272"><a name="p57747459272"></a><a name="p57747459272"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/resnet50" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/resnet50</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    <tr id="row377484514279"><td class="cellrowborder" valign="top" width="12.85%" headers="mcps1.2.4.1.1 "><p id="p1777454516275"><a name="p1777454516275"></a><a name="p1777454516275"></a><span>resnet101</span></p>
    </td>
    <td class="cellrowborder" valign="top" width="12.57%" headers="mcps1.2.4.1.2 "><p id="p15774124516274"><a name="p15774124516274"></a><a name="p15774124516274"></a>图片分类推�模型。</p>
    <p id="p7774134552720"><a name="p7774134552720"></a><a name="p7774134552720"></a>是基于Caffe的ResNet 101模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="74.58%" headers="mcps1.2.4.1.3 "><p id="p117741545132710"><a name="p117741545132710"></a><a name="p117741545132710"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/resnet101" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/resnet101</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    <tr id="row14774154513279"><td class="cellrowborder" valign="top" width="12.85%" headers="mcps1.2.4.1.1 "><p id="p1077413452272"><a name="p1077413452272"></a><a name="p1077413452272"></a><span>resnet15</span>2</p>
    </td>
    <td class="cellrowborder" valign="top" width="12.57%" headers="mcps1.2.4.1.2 "><p id="p177434517275"><a name="p177434517275"></a><a name="p177434517275"></a>图片分类推�模型。</p>
    <p id="p877515459276"><a name="p877515459276"></a><a name="p877515459276"></a>是基于Caffe的ResNet 152模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="74.58%" headers="mcps1.2.4.1.3 "><p id="p777514582712"><a name="p777514582712"></a><a name="p777514582712"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/resnet152" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/resnet152</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    <tr id="row37752450270"><td class="cellrowborder" valign="top" width="12.85%" headers="mcps1.2.4.1.1 "><p id="p977544513278"><a name="p977544513278"></a><a name="p977544513278"></a><span>vgg16</span></p>
    </td>
    <td class="cellrowborder" valign="top" width="12.57%" headers="mcps1.2.4.1.2 "><p id="p1177514522713"><a name="p1177514522713"></a><a name="p1177514522713"></a>图片分类推�模型。</p>
    <p id="p10775194582713"><a name="p10775194582713"></a><a name="p10775194582713"></a>是基于Caffe的VGG16模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="74.58%" headers="mcps1.2.4.1.3 "><p id="p18775124582720"><a name="p18775124582720"></a><a name="p18775124582720"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/vgg16" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/vgg16</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    <tr id="row2775194518272"><td class="cellrowborder" valign="top" width="12.85%" headers="mcps1.2.4.1.1 "><p id="p5775154516272"><a name="p5775154516272"></a><a name="p5775154516272"></a><span>vgg19</span></p>
    </td>
    <td class="cellrowborder" valign="top" width="12.57%" headers="mcps1.2.4.1.2 "><p id="p0775204532711"><a name="p0775204532711"></a><a name="p0775204532711"></a>图片分类推�模型。</p>
    <p id="p1477554519275"><a name="p1477554519275"></a><a name="p1477554519275"></a>是基于Caffe的VGG19模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="74.58%" headers="mcps1.2.4.1.3 "><p id="p777554542713"><a name="p777554542713"></a><a name="p777554542713"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/vgg19" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/vgg19</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    <tr id="row17513194404914"><td class="cellrowborder" valign="top" width="12.85%" headers="mcps1.2.4.1.1 "><p id="p7513164419495"><a name="p7513164419495"></a><a name="p7513164419495"></a>squeezenet</p>
    </td>
    <td class="cellrowborder" valign="top" width="12.57%" headers="mcps1.2.4.1.2 "><p id="p1315111145015"><a name="p1315111145015"></a><a name="p1315111145015"></a>图片分类推�模型。</p>
    <p id="p1515131114501"><a name="p1515131114501"></a><a name="p1515131114501"></a>是基于Caffe的SqueezeNet模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="74.58%" headers="mcps1.2.4.1.3 "><p id="p16265437125015"><a name="p16265437125015"></a><a name="p16265437125015"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/squeezenet" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/squeezenet</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
    </td>
    </tr>
    <tr id="row17757454270"><td class="cellrowborder" valign="top" width="12.85%" headers="mcps1.2.4.1.1 "><p id="p17759452279"><a name="p17759452279"></a><a name="p17759452279"></a><span>dpn98</span></p>
    </td>
    <td class="cellrowborder" valign="top" width="12.57%" headers="mcps1.2.4.1.2 "><p id="p4775545162716"><a name="p4775545162716"></a><a name="p4775545162716"></a>图片分类推�模型。</p>
    <p id="p1577504516278"><a name="p1577504516278"></a><a name="p1577504516278"></a>是基于Caffe的<span>dpn98</span>模型。</p>
    </td>
    <td class="cellrowborder" valign="top" width="74.58%" headers="mcps1.2.4.1.3 "><p id="p19776154592711"><a name="p19776154592711"></a><a name="p19776154592711"></a>请�考<a href="https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/dpn98" target="_blank" rel="noopener noreferrer">https://github.com/Ascend-Huawei/models/tree/master/computer_vision/classification/dpn98</a>目录中README.md下载原始网络模型文件�其对应的��文件。</p>
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
        -   Model File选择[步骤2](#li29641938112018)中下载的模型文件，此时会自动匹�到��文件并填写在Weight File中。
        -   Model Name填写为[表1](#table1119094515272)中对应的**模型�称**。

            ![](figures/zh-cn_image_0208264607.png)

        -   googlenet�inception\_v2模型转�时中，由于通用分类网络应用一次处�一张图片，所以转�时需�将Input Node�置中的**N**修改为1，如[图2](#fig95695336322)所示。AIPP�置中的  **Input Image Size**  需�分别修改为256�224，此处需�128\*16对�，**Model Image Format**  选择BGR888\_U8，如[图3](#fig14632122193310)所示。

            **图 2**  Nodes�置示例<a name="fig95695336322"></a>  
            ![](figures/Nodes�置示例.png "Nodes�置示例")

            **图 3**  AIPP�置示例<a name="fig14632122193310"></a>  
            ![](figures/AIPP�置示例.png "AIPP�置示例")

    3.  �击OK开始转�模型。

        模型转��功�，�缀为.om的离线模型存放地�为：$HOME/modelzoo/XXX/device。

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   Mind Studio模型转�中�一步的具体�义和�数说明�以�考[Mind Studio用户手册](https://ascend.huawei.com/doc/mindstudio/)中的“模型转�“章节。  
    >-   XXX表示当�转�的模型�称，如googlenet.om存放地�为：$HOME/modelzoo/googlenet/device。  

5.  <a name="li470213205618"></a>将转�好的模型文件（.om文件）上传到[步骤1](#li953280133816)中��所在路径下的“**sample-classification/script**�目录下。

## 编译<a name="section18931344873"></a>

1.  打开对应的工程。

    以Mind Studio安装用户在命令行进入安装包解压�的“MindStudio-ubuntu/bin�目录，如：$HOME/MindStudio-ubuntu/bin。执行如下命令�动Mind Studio。

    **./MindStudio.sh**

    �动�功�，打开**sample-classification**工程，如[图 打开classification工程](#fig11106241192810)所示。

    **图 4**  打开classification工程<a name="fig11106241192810"></a>  
    ![](figures/打开classification工程.png "打开classification工程")

2.  在**src/param\_configure.conf**文件中�置相关工程信�。

    **图 5**  �置文件路径<a name="fig0391184062214"></a>  
    ![](figures/�置文件路径-14.png "�置文件路径-14")

    该�置文件内容如下：

    ```
    remote_host=
    model_name=
    ```

    需�手动添加�数�置：

    -   remote\_host：Atlas 200 DK开�者�的IP地�。
    -   model\_name : 离线模型�称。

    �置示例：

    ```
    remote_host=192.168.1.2
    model_name=googlenet.om
    ```

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   �数必须全部填写，�则无法通过build。  
    >-   注��数填写时�需�使用“�符�。  
    >-   �置文件中�能填入�个模型�称，填入的模型必须为[步骤5](#li470213205618)中存储的模型之一。本示例是以googlenet举例，用户�以使用本样例列举的其它模型按照文档步骤进行替��行。  

3.  执行deploy脚本， 进行�置�数调整�第三方库下载编译 打开Mind Studio工具的Terminal，此时默认在代�主目录下，执行如下命令在��指执行deploy脚本，进行环境部署。如[图 执行deploy脚本](#fig478266192619)所示。

    **图 6**  执行deploy脚本<a name="fig478266192619"></a>  
    ![](figures/执行deploy脚本-15.png "执行deploy脚本-15")

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   首次deploy时，没有部署第三方库时会自动下载并编译，耗时�能比较久，请�心等待。�续��新编译时，�会��下载编译，部署如上图所示。  
    >-   deploy时，需�选择与开��通信的主机侧ip，一般为虚拟网��置的ip。如果此ip和开��ip属于�网段，则会自动选择并部署。如果��网段，则需�手动输入与开��通信的主机侧ip�能完�deploy。  

4.  开始编译，打开Mind Studio工具，在工具�中点击**Build \> Build \> Build-Configuration**。如[图 编译�作�生�文件](#fig1741464713019)所示，会在目录下生�build和run文件夹。

    **图 7**  编译�作�生�文件<a name="fig1741464713019"></a>  
    ![](figures/编译�作�生�文件-16.png "编译�作�生�文件-16")

    >![](public_sys-resources/icon-notice.gif) **须知：**   
    >首次编译工程时，**Build \> Build**为�色��点击状�。需�点击**Build \> Edit Build Configuration**，�置编译�数��进行编译。  

5.  将需�推�的图片上传至Host侧任一属组为HwHiAiUser用户的目录。

    图片�求如下：

    -   格�：jpg�png�bmp。
    -   输入图片宽度：16px\~4096px之间的整数。
    -   输入图片高度：16px\~4096px之间的整数。


## �行<a name="section372782554919"></a>

1.  在Mind Studio工具的工具�中找到Run按钮，�击  **Run \> Run 'sample-classification'**，如[图 程�已执行示�图](#fig93931954162719)所示，�执行程�已�在开�者�执行。

    **图 8**  程�已执行示�图<a name="fig93931954162719"></a>  
    ![](figures/程�已执行示�图.png "程�已执行示�图")

    以上报错信�请忽略，因为Mind Studio无法为�执行程�传�，上述步骤是将�执行程�与�赖的库文件部署到开�者�，此步骤需�ssh登录到开�者�至相应的目录文件下手动执行，具体请�考以下步骤。

2.  在Mind Studio所在Ubuntu�务器中，以HwHiAiUser用户SSH登录到Host侧。

    **ssh HwHiAiUser@**_host\_ip_

    对于Atlas 200 DK，host\_ip默认为192.168.1.2（USB连接）或者192.168.0.2（NIC连接）。

3.  进入通用分类网络应用的�执行文件所在路径。

    **cd \~/HIAI\_PROJECTS/ascend\_workspace/classification/out**

4.  执行应用程�。

    执行**run\_classification.py**脚本会将推�结果在执行终端直接打�显示。

    命令示例如下所示：

    **python3 run\_classification.py -w  _224_  -h  _224_  -i** **_./example.jpg_  -n  _10_**

    -   -w/model\_width：模型的输入图片宽度，为16\~4096之间的整数，请�考[表1](#table1119094515272)在Gitee上查看所使用模型文件的Readme，获�模型�求的输入数�的宽和高。
    -   -h/model\_height：模型的输入图片高度，为16\~4096之间的整数，请�考[表1](#table1119094515272)在Gitee上查看所使用模型文件的Readme，获�模型�求的输入数�的宽和高。
    -   -i/input\_path：输入图片的路径，�以是目录，表示当�目录下的所有图片都作为输入（�以指定多个输入）。
    -   -n/top\_n：输出�n个推�结果。

    其他详细�数请执行**python3 run\_classification.py --help**命令��帮助信�。


