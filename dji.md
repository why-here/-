## Dji--视觉算法优化工程师

### 算法定点化

- [定点数编程](fixedvalue.md)

### FPGA 设计

### Caffe TensorFlow 平台

##### Caffe

##### TensorFlow

- [tf](tf.md)

### 计算机视觉算法

##### 分类 

- [分类卷积网](class_cnn.md) [Link](http://www.infoq.com/cn/articles/cnn-and-imagenet-champion-model-analysis)

##### 目标检测

- [目标检测](object_dection.md)

##### 语义分割

- [语义分割](semantic_segmentation.md)

##### 细粒度图像分类

- [Link](https://zhuanlan.zhihu.com/p/24738319)

##### GAN

- [Link](https://blog.csdn.net/on2way/article/details/72773771)

##### 基础

###### 边缘检测算子

> 不同图像灰度不同，边界处一般会有明显的边缘，利用此特征可以分割图像。需要说明的是：边缘和物体间的边界并不等同，边缘指的是图像中像素的值有突变的地方，而物体间的边界指的是现实场景中的存在于物体之间的边界。 

- [Link](https://blog.csdn.net/icamera0/article/details/50521442)
- [Link](https://blog.csdn.net/gdut2015go/article/details/46779251)

###### OTSU（大津法）阈值分割

> OTSU是一种对图像进行全局自适应阈值来进行二值化的方法。它按图像的灰度特性，将图像分为前景和背景两个部分。因为方差是会度分布均匀性的一种度量，前景（目标）和背景的类间方差越大，说明构成图像两部分的差别越大，即说明当前前景与背景的分割越好，因此我们可以认为当所取阈值使得类间方差最大时，分割结果最好，此时的阈值就是OTSU的结果。 

- [Link](https://blog.csdn.net/donghai_yu/article/details/79545508)

###### smooth l1 loss

- [Link](https://www.zhihu.com/question/58200555)
- [Link](https://blog.csdn.net/weixin_35653315/article/details/54571681)

###### 如何用计算机求解，如有推导过程请写下推导过程 

- $min\{x^4-4x^3+x^2+10\}$

###### 矩阵的广义逆

> 任意的矩阵都存在广义逆阵，若一矩阵存在逆矩阵，逆矩阵即为其唯一的广义逆阵。 

###### 矩阵链乘法

> 对于一般的矩阵乘法来说，如矩阵A(m,n)与矩阵B(n,p)相乘需要进行的加法次数为`m*n*p`次乘法。 

- [Link](https://blog.csdn.net/luoshixian099/article/details/46344175)

###### 电影票问题

> 模拟所有人买票过程，递归求解；拿50块钱的都能立即买票，拿100块钱的只有前面拿50块钱的多余100块钱的才能买票。

- [Link](http://samuschen.iteye.com/blog/1158748)

### 深度学习

#### 神经网络

##### 神经元

- 权重，输入，bias，激活函数

##### 训练

- 前向传播，后向传播，损失函数，正则化，
- chain rule 链式法则

##### 卷积网络

- 卷积核，参数，池化，

### 嵌入式系统

