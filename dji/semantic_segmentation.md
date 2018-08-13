翻译自[qure.ai](http://blog.qure.ai/notes/semantic-segmentation-deep-learning-review)

1. 什么是语义分割

   对图片的每个像素都做分类。

   较为重要的语义分割数据集有：[VOC2012](http://host.robots.ox.ac.uk/pascal/VOC/voc2012/) 以及 [MSCOCO](http://mscoco.org/explore/) 。

2. 有哪几种方法

   传统机器学习方法：如像素级的决策树分类，参考[TextonForest](http://mi.eng.cam.ac.uk/~cipolla/publications/inproceedings/2008-CVPR-semantic-texton-forests.pdf) 以及 [Random Forest based classifiers](http://www.cse.chalmers.se/edu/year/2011/course/TDA361/Advanced%20Computer%20Graphics/BodyPartRecognition.pdf) 。再有就是深度学习方法。更确切地说，是卷积神经网络。

   深度学习最初流行的分割方法是，打补丁式的分类方法 ( patch classification ) 。逐像素地抽取周围像素对中心像素进行分类。由于当时的卷积网络末端都使用全连接层 ( full connected layers ) ，所以只能使用这种逐像素的分割方法。

   2014年，来自伯克利的 [Fully Convolutional Networks(FCN)](http://blog.qure.ai/notes/semantic-segmentation-deep-learning-review#fcn) 卷积网络，去掉了末端的全连接层。随后的语义分割模型基本上都采用了这种结构。除了全连接层，语义分割另一个重要的问题是池化层。池化层能进一步提取抽象特征增加感受域，但是丢弃了像素的位置信息。但是语义分割需要类别标签和原图像对齐，因此需要从新引入像素的位置信息。有两种不同的架构可以解决此像素定位问题。

   第一种是编码-译码架构。编码过程通过池化层逐渐减少位置信息、抽取抽象特征；译码过程逐渐恢复位置信息。一般译码与编码间有直接的连接。该类架构中[U-net](https://arxiv.org/abs/1505.04597) 是最流行的。

   第二种架构是膨胀卷积 ( dilated convolutions ) ，抛弃了池化层。使用的卷积核如下图。

   ![dilated](http://blog.qure.ai/assets/images/segmentation-review/dilated_conv.png)

   [条件随机场的后处理](https://arxiv.org/abs/1210.5644) 经常用来提高分割的精确度。后处理利用图像的光感强度（可理解为亮度），将周围强度相近的像素分为同一类。能提高 1-2 个百分点。

3. 文章汇总

   按时间顺序总结八篇paper，看语义分割的结构是如何演变的。分别有[FCN](http://blog.qure.ai/notes/semantic-segmentation-deep-learning-review#fcn) 、[SegNet](http://blog.qure.ai/notes/semantic-segmentation-deep-learning-review#segnet) 、[Dilated Convolutions](http://blog.qure.ai/notes/semantic-segmentation-deep-learning-review#dilation) 、[DeepLab (v1 & v2)](http://blog.qure.ai/notes/semantic-segmentation-deep-learning-review#deeplab) 、[RefineNet](http://blog.qure.ai/notes/semantic-segmentation-deep-learning-review#refinenet) 、[PSPNet](http://blog.qure.ai/notes/semantic-segmentation-deep-learning-review#pspnet) 、[Large Kernel Matters](http://blog.qure.ai/notes/semantic-segmentation-deep-learning-review#large-kernel) 、[DeepLab v3](http://blog.qure.ai/notes/semantic-segmentation-deep-learning-review#deeplabv3) 。

   **FCN** 2014年

   主要的贡献：

   - 为语义分割引入了 [端到端](https://www.zhihu.com/question/51435499/answer/129379006) 的**全**卷积网络，并流行开来
   - 重新利用 ImageNet 的预训练网络用于语义分割
   - 使用 [反卷积层](http://blog.csdn.net/u014722627/article/details/60574260?readlog) 进行上采样
   - 引入跳跃连接来改善上采样粗糙的像素定位

   说明：

   比较重要的发现是，分类网络中的全连接层可以看作对输入的[全域卷积操作](http://blog.csdn.net/taigw/article/details/51401448)，这种转换能使计算更为高效，并且能重新利用 ImageNet 的预训练网络。经过多层卷积及池化操作后，需要进行上采样，FCN 使用反卷积（可学习）取代简单的线性插值算法进行上采样。

![fcn](https://img-blog.csdn.net/20180630173434451?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTM1ODAzOTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

   **SegNet** 2015年

   编码-译码架构

   主要贡献：

   - 将池化层结果应用到译码过程。引入了更多的编码信息。使用的是pooling indices而不是直接复制特征，只是将编码过程中 pool 的位置记下来，在 uppooling 是使用该信息进行 pooling 。

<center>
![poolindex](https://img-blog.csdn.net/20180630181129947?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTM1ODAzOTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
</center>

![segnet](https://img-blog.csdn.net/20180630175123566?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTM1ODAzOTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**U-Net** 2015
U-Net 有更规整的网络结构，通过将编码器的每层结果拼接到译码器中得到更好的结果。

![unet](https://img-blog.csdn.net/20180630180700949?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTM1ODAzOTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

   **Dilated Convolutions** 2015年

   通过膨胀卷积操作聚合多尺度的信息

   主要贡献：

   - 使用膨胀卷积
   - 提出 ’context module‘ ，用来聚合多尺度的信息

   说明：

   池化在分类网络中能够扩大感知域，同样降低了分辨率。所以作者提出了膨胀卷积层。

   ![dilated conv](https://raw.githubusercontent.com/vdumoulin/conv_arithmetic/master/gif/dilation.gif)

![dilated](https://img-blog.csdn.net/20180630173509966?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTM1ODAzOTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
   **(a)** 原始的 3×33×3卷积，1-dilated，感受野为 3×33×3；

   **(b)** 在(a)的基础上进行 3×33×3卷积，2-dilated，感受野为 7×77×7；

   **(c)** 在(b)的基础上进行 3×33×3卷积，4-dilated，感受野为 15×1515×15；

   由于padding和卷积的stride=1，卷积前后feature map大小可以保持不变，但每个元素的感受野指数增大。[Link](https://blog.csdn.net/shuzfan/article/details/69948944)

   膨胀卷积在 DeepLab 中也被称为暗黑卷积 (atrous convolution) 。此卷积能够极大的扩大感知域同时不减小空间维度。本模型移去了VGG网的最后两层池化层，并且其后续的卷积层都采用膨胀卷积。

   作者还训练了一个模块，输入卷积结果，级联了不同膨胀系数的膨胀卷积层的，输出和输入有一样的尺寸，因此此模块能够提取不同规模特征中的信息，得到更精确的分割结果。

   最后预测结果图是原图的八分之一大小，文章使用插值得到最后的分割结果。

   **DeepLab (v1 & v2)** 2014 & 2016

   主要贡献：

   - 使用膨胀卷积
   - 提出了暗黑空间金字塔池化 (ASPP)，融合了不同尺度的信息。
   - 使用全连接的条件随机场

   说明：

   基本网络和 dilated convolutions 一致。最后的结构化预测 (精细分割) 采用全连接的 CDF。提出了ASPP，但结果不如 FC-CDF 。

![Pipline](http://blog.qure.ai/assets/images/segmentation-review/deeplabv2.png)

![ASPP](https://img-blog.csdn.net/20180630173540919?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTM1ODAzOTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

   **RefineNet** 2016年

   主要贡献：

   - 精心设计的译码模块
   - 所有模块遵循残余连接设计

   说明：

   膨胀卷积有几个缺点，如计算量大、需要大量内存。这篇文章采用编码-译码架构。编码部分是 [ResNet-101](https://arxiv.org/abs/1512.03385) 模块。译码采用 RefineNet 模块，该模块融合了编码模块的高分辨率特征和前一个 RefineNet 模块的抽象特征。

   每个 RefineNet 模块接收多个不同分辨率特征，并融合。看图。

   ![Architecture](http://blog.qure.ai/assets/images/segmentation-review/refinenet%20-%20architecture.png)

   ![RefineNet Block](http://blog.qure.ai/assets/images/segmentation-review/refinenet%20-%20block.png)

   **PSPNet** 2016年

   Pyramid Scene Parsing Network 金字塔场景解析网络

   主要贡献：

   - 提出了金字塔池化模块来聚合图片信息
   - 使用附加的损失函数

   说明：

   金字塔池化模块通过应用大核心池化层来提高感知域。使用膨胀卷积来修改 ResNet 网，并增加了金字塔池化模块。金字塔池化模块对 ResNet 输出的特征进行不同规模的池化操作，并作上采样后，拼接起来，最后得到结果。

   本文提出的网络结构简单来说就是将DeepLab（不完全一样）aspp之前的feature map pooling了四种尺度之后 将5种feature map concat到一起经过卷积最后进行prediction的过程。 

   附加的损失函数：看不懂

   ![Architecture](http://blog.qure.ai/assets/images/segmentation-review/pspnet.png)

   **Large Kernel Matters** 2017

   主要贡献：

   - 提出了使用大卷积核的编码-译码架构

   说明：

   理论上更深的 ResNet 能有很大的感知域，但研究表明实际上提取的信息来自很小的范围，因此使用大核来扩大感知域。但是核越大，计算量越大，因此将 k x k 的卷积近似转换为 1 x k + k x 1 和 k x 1 + 1 x k 卷积的和。本文称为 GCN。

   本文的架构是：使用 ResNet 作为编译器，而 GCN 和反卷积作为译码器。还使用了名为 Boundary Refinement 的残余模块。

   ![Architecture](http://blog.qure.ai/assets/images/segmentation-review/large_kernel_matter.png)

   **DeepLab v3** 2017

   主要贡献：

   - 改进 ASPP
   - 串行部署 ASPP 的模块

   说明：

   和 DeepLab v2 一样，将膨胀卷积应用于 ResNet 中。改进的 ASPP 指的是将不同膨胀率的膨胀卷积结果拼接起来。并使用了 BN 。

   于 Dilated convolutions (2015) 不一样的是，v3 直接对中间的特征图进行膨胀卷积，而不是在最后做。

   ![Improved ASPP](http://blog.qure.ai/assets/images/segmentation-review/deeplabv3.png)

**采集多尺度信息的方法**
![multi-scale](https://img-blog.csdn.net/201806301741285?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTM1ODAzOTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**对比**

|          模型          | 分数 (VOC2012) |
| :------------------: | :----------: |
|         FCN          |     67.2     |
|        SegNet        |     59.9     |
| Dilated Convolutions |     75.3     |
|  DeepLab (v1 & v2)   |     79.7     |
|      RefineNet       |     84.2     |
|        PSPNet        |     85.4     |
| Large Kernel Matters |     83.6     |
|      DeepLab v3      |     85.7     |

