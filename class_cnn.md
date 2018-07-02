分类卷积网 

来自 [cs231n](http://cs231n.github.io/convolutional-networks/#case)

**LeNet** 1990‘s 

第一次成功应用卷积网络。[LeNet](http://yann.lecun.com/exdb/publis/pdf/lecun-98.pdf) 被用来识别手写数字。

卷积核 5x5 stride 1，池化 2x2 stride 2
结构 CONV-POOL-CONV-POOL-FC-FC

![LeNet](http://img.blog.csdn.net/20171112223922233?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMzU4MDM5Nw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

**AlexNet** 2012

第一个被广泛关注的卷积网络。结构和 LeNet 基本一致，但是变得更深，更大，使用多卷积层+池化层的堆叠结构。[AlexNet ](http://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks)

输入 227x227x3
结构 CONV1-POOL1-NORM1-CONV2-POOL2-NORM2-CONV3-CONV4-CONV5-POOL-FC6-FC7-FC8
CONV1 : 96 11x11 stride 4 ；输出 [55x55x96]  参数：`(11*11*3)*96=35K`
输出维度 = (输入维度 - 核大小）/ stride + 1 (卷积和池化一样)
POOL1：3x3 stride 2 ；输出 [27x27x96]

```
Full (simplified) AlexNet architecture:
[227x227x3] INPUT
[55x55x96] CONV1: 96 11x11 filters at stride 4, pad 0
[27x27x96] MAX POOL1: 3x3 filters at stride 2
[27x27x96] NORM1: Normalization layer
[27x27x256] CONV2: 256 5x5 filters at stride 1, pad 2
[13x13x256] MAX POOL2: 3x3 filters at stride 2
[13x13x256] NORM2: Normalization layer
[13x13x384] CONV3: 384 3x3 filters at stride 1, pad 1
[13x13x384] CONV4: 384 3x3 filters at stride 1, pad 1
[13x13x256] CONV5: 256 3x3 filters at stride 1, pad 1
[6x6x256] MAX POOL3: 3x3 filters at stride 2
[4096] FC6: 4096 neurons
[4096] FC7: 4096 neurons
[1000] FC8: 1000 neurons (class scores)
```

第一次使用 ReLU; droupout 0.5


![AlexNet](http://img.blog.csdn.net/20171112224006395?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMzU4MDM5Nw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

**ZFNet** 2013

重新调整了 AlexNet 的超参数，如：增大了中间卷积层的大小，减小第一层的卷积核数和步伐 (stride) 。[ZENet](http://arxiv.org/abs/1311.2901)

```
AlexNet but:
CONV1: change from (11x11 stride 4) to (7x7 stride 2)
CONV3,4,5: instead of 384, 384, 256 filters use 512, 1024, 512
```

![ZFNet](http://img.blog.csdn.net/20171112224122083?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMzU4MDM5Nw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

**VGGNet** 2014

最大的贡献是网络的深度对性能有很大的影响。并且整个网络只使用 3 x 3 的卷积核以及 2 x 2 的池化。但是网络的参数量很大。[VGGNet](http://www.robots.ox.ac.uk/~vgg/research/very_deep/) 。

特点：使用更小的卷积核 3x3 stride 1,堆叠 3 层 3x3 的卷积核能达到与 7x7 卷积核一样大的感受域，堆叠 3 层更深，达到更好的非线性特性。参数更少 $3*(3^2*C^2) vs 7^2C^2$ C 为每层的通道数

```
memory: 224*224*3=150K params: 0
CONV3-64: [224x224x64] memory: 224*224*64=3.2M params: (3*3*3)*64 = 1,728
CONV3-64: [224x224x64] memory: 224*224*64=3.2M params: (3*3*64)*64 = 36,864
POOL2: [112x112x64] memory: 112*112*64=800K params: 0
CONV3-128: [112x112x128] memory: 112*112*128=1.6M params: (3*3*64)*128 = 73,728
CONV3-128: [112x112x128] memory: 112*112*128=1.6M params: (3*3*128)*128 = 147,456
POOL2: [56x56x128] memory: 56*56*128=400K params: 0
CONV3-256: [56x56x256] memory: 56*56*256=800K params: (3*3*128)*256 = 294,912
CONV3-256: [56x56x256] memory: 56*56*256=800K params: (3*3*256)*256 = 589,824
CONV3-256: [56x56x256] memory: 56*56*256=800K params: (3*3*256)*256 = 589,824
POOL2: [28x28x256] memory: 28*28*256=200K params: 0
CONV3-512: [28x28x512] memory: 28*28*512=400K params: (3*3*256)*512 = 1,179,648
CONV3-512: [28x28x512] memory: 28*28*512=400K params: (3*3*512)*512 = 2,359,296
CONV3-512: [28x28x512] memory: 28*28*512=400K params: (3*3*512)*512 = 2,359,296
POOL2: [14x14x512] memory: 14*14*512=100K params: 0
CONV3-512: [14x14x512] memory: 14*14*512=100K params: (3*3*512)*512 = 2,359,296
CONV3-512: [14x14x512] memory: 14*14*512=100K params: (3*3*512)*512 = 2,359,296
CONV3-512: [14x14x512] memory: 14*14*512=100K params: (3*3*512)*512 = 2,359,296
POOL2: [7x7x512] memory: 7*7*512=25K params: 0
FC: [1x1x4096] memory: 4096 params: 7*7*512*4096 = 102,760,448
FC: [1x1x4096] memory: 4096 params: 4096*4096 = 16,777,216
FC: [1x1x1000] memory: 1000 params: 4096*1000 = 4,096,000
```
> TOTAL memory: 24M * 4 bytes ~= 96MB / image (only forward! ~*2 for bwd)
> TOTAL params: 138M parameters

FC7 的输出能很好地应用于其他任务。

<center>
![VGGNet](http://img.blog.csdn.net/20171112224305458?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMzU4MDM5Nw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
</center>

**GoogLeNet** 2014

设计了一个称为 *Inception Module* 的模块，大幅度降低网络的参数数目。此外使用平均池化代替卷积网末端的全连接层。后续也有几个不同版本的 GoogLeNet，最新的是 [Inception-v4](http://arxiv.org/abs/1602.07261) 。
没有 FC 层，参数少
Inception module 设计了网络中的网络，然后堆叠这些模块。
使用并行的卷积核作用于上层的输入，分别为 1x1x 3x3 5x5 的 conv 和 3x3 的 pool (stride1,padding?)，然后将输出拼接。输出通道数分别为 128 192 96 256。图 (a)
缺点：会加大计算量，同时通道数不断增加。使用 1x1 的卷积来减少通道数。图(b)

通过 pool 降低空间维度，1x1 conv 降低特征维度，从而避免 FC 的大量参数。将中间某一层的输出用作分类，并按一个较小的权重（0.3）加到最终分类结果中。这样相当于做了模型融合

![Inception](http://img.blog.csdn.net/20171112224205966?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMzU4MDM5Nw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

**Inception V2** 

Inception V2学习了VGGNet，用两个3*3的卷积代替5*5的大卷积（用以降低参数量并减轻过拟合），还提出了著名的BatchNormalization（以下简称BN）方法。BN某种意义上还起到了正则化的作用，所以可以减少或者取消Dropout，简化网络结构。

**Inception V3**

Inception V3网络则主要有两方面的改造：将一个较大的二维卷积拆成两个较小的一维卷积，比如将`7*7`卷积拆成`1*7`卷积和`7*1`卷积，或者将`3*3`卷积拆成`1*3`卷积和`3*1`卷积，
<center>
![i3](https://img-blog.csdn.net/2018062922215071?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTM1ODAzOTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
![i3all](https://img-blog.csdn.net/20180629222203128?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTM1ODAzOTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
</center>
**Inception V4**

融合了 ResNet

![googelnet](https://img-blog.csdn.net/2018062921384419?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTM1ODAzOTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**ResNet** 2015

[ResNet](http://arxiv.org/abs/1512.03385) 的特点是引入了跳跃连接以及大量使用 [batch normalization](http://arxiv.org/abs/1502.03167) ，并且去掉了网络末端的全连接层。ResNet 是目前表现最好的卷积网，并且被大量使用（ 2016 年 5 月 10 号）。ResNet 还有其他改进的版本。

越深的网络按道理应该表现得别浅的网络好，但由于优化问题，反而表现得差。

输出为 H(x) = F(x) + x => F(x) = H(x) - x ,使用网络来拟合 F(x) 残差。

每个残差块包含两个 3x3 的卷积，周期性地翻倍卷积核个数并通过stride2来降低空间维度。最后通过Pool来降低 FC 的参数。

深度可以为 34 50 101 152 ，在深度大于50 时可以采用 GoogLeNet 的 1x1 降低空间维度的方法来提高效率

<center>
![Res_block](http://img.blog.csdn.net/20171112224350433?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMzU4MDM5Nw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
![deeperresnet](https://img-blog.csdn.net/20180629223245947?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTM1ODAzOTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
![resnet](https://img-blog.csdn.net/20180629222228622?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTM1ODAzOTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
</center>

**研究方向**
1. 围绕卷积层的设计以及跳跃网络的设计，提高梯度更新效率
2. 深度和广度的重要性，

<center>
|         Model         | Score (top5 err) |
| :-------------------: | :--------------: |
|  AlexNet (8 layers)   |       16.4       |
|   ZFNet (8 layers )   |       11.7       |
|  VGGNet (19 layers)   |       7.3        |
| GoogLeNet (22 layers) |       6.7        |
|  ResNet (152 layers)  |       3.57       |
</center>

Top-5错误率：即对一个图片，如果概率前五中包含正确答案，即认为正确。
Top-1错误率：即对一个图片，如果概率最大的是正确答案，才认为正确。