## 登顶Github趋势榜，非监督GAN算法U-GAT-IT大幅改进图像转换效果

原创： CV君 [我爱计算机视觉](javascript:void(0);) *昨天*



点击我爱计算机视觉标星，更快获取CVML新技术

------



近日，GAN的大家族又出一位重量级新成员U-GAT-IT，图像转换效果提升明显，原作者开源代码这两天登顶Github趋势榜，引起极大关注。



U-GAT-IT算法源自论文U-GAT-IT: Unsupervised Generative Attentional Networks with Adaptive Layer-Instance Normalization for Image-to-Image Translation：



![img](https://mmbiz.qpic.cn/mmbiz_png/BJbRvwibeSTuPeJib491yia3s9bbfCctCbDEvIN3APXCvPUpBf6sUOYq6ic02A4Qoor4n0j4CTka8A3XPeUA9CAmng/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

作者来自韩国NCSOFT公司与波音韩国工程技术中心。



论文主要贡献：



\1. 提出了一种新的无监督图像到图像转换方法，它具有新的注意力模块和新的归一化函数AdaLIN。



\2. 提出的注意力模块通过基于辅助分类器获得的注意力图，区分源域和目标域，帮助模型知道在何处进行密集转换。



\3. AdaLIN函数帮助我们的注意力引导模型灵活地控制形状和纹理的变化量，而无需修改模型架构或超参数。



U-GAT-IT，是无监督的GAN，训练时不需要成对图像，由两套GAN系统循环图像转换组成。

一套GAN系统，将图像从源域到目标域转换。

另一套GAN系统，将图像从目标域向源域转换。

故其有两套生成器和判别器。

为了让系统在生成和判别时更具针对性对特定区域进行转换和鉴别，作者加入**CAM（**意即类激活图模块）。它能找出对于判断一张图的真假最重要的区域，这样生成器和判别器就可对此区域更具针对性生成和判别。

作者使用的生成器：

![img](https://mmbiz.qpic.cn/mmbiz_png/BJbRvwibeSTuPeJib491yia3s9bbfCctCbDXicCibsK1n8VicZqWOS04uUynMiaUyMtrm7Rlc37WsFeEeKDXIQeo9iaPyw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



作者使用的判别器：

![img](https://mmbiz.qpic.cn/mmbiz_png/BJbRvwibeSTuPeJib491yia3s9bbfCctCbDAhkxF9TNBjOvjWZmpNAAPMrFoWfuQeibhOyMnlFrRZcaKVORugRHHBA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



另外作者发明了AdaLIN归一化方法，其作用为在归一化时，在Instance Normalization (IN)和Layer Normalization（LN）两种归一化方法之间动态自适应选择，不局限于常用的IN。



作者称，AdaLIN可以使得系统灵活控制形状与质地的变化。

**实验结果**

作者首先研究了添加注意力模块CAM给系统带来的影响，下图为几幅图像转换的视觉效果比较：

![img](https://mmbiz.qpic.cn/mmbiz_png/BJbRvwibeSTuPeJib491yia3s9bbfCctCbDibFCsFNzvUzSksTe3ibLUKH7L0wD3HCPnygiapZWeZ8DUYn0vSGBZfQ3A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

（a）为原图像，（b）为生成器的注意力图，（c）（d）为鉴别器的局部和全局注意力图，（e）为使用CAM后的图像转换结果，（f）为不实用CAM的结果。



可见，该文提出的CAM模块极大提升了转换图像的视觉效果。



数值量化比较结果如下：



![img](https://mmbiz.qpic.cn/mmbiz_png/BJbRvwibeSTuPeJib491yia3s9bbfCctCbDdNa4T4CXcL9aP0TZ4olnT6pmUpVEicFeDSh3HEAx8cYYzOuVY5Vcmmg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



可见使用CAM与AdaIN，均使得算法效果提升。



作者在多个数据集上进行转换，并进行了用户主观感受的调查研究：



![img](https://mmbiz.qpic.cn/mmbiz_png/BJbRvwibeSTuPeJib491yia3s9bbfCctCbDK8sfEtCibjrUXIJWviazAKlAeKgmOoLv46bMMkZBibrSLhRJmpKV0N6Aw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

共有135位参与者对使用图中 5 种算法转换的结果进行了打分，U-GAT-IT可谓是取得了压倒性的优势！



作者在几大数据集上对正向和逆向图像转换都进行了比较，数值结果如下：



![img](https://mmbiz.qpic.cn/mmbiz_png/BJbRvwibeSTuPeJib491yia3s9bbfCctCbDyOshCzGBzn6LicIFg4FyTJbkVxmmRFtQ6jKUoXFosvuTPV5FN6enm2g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



U-GAT-IT在大多数情况下都是最好的！



总之，U-GAT-IT是目前无监督图像转换的新标杆！



**多说一句，**

**图像转换有什么用？**



除了“自拍变漫画”、“猫变狗”、“狗变猫”、“实景变素描”这些偏娱乐性的应用，图像转换也可以用来做“正经事”。



CV君曾经跟大家分享了一篇无监督GAN用于医学图像数据增广的文章：

[数据不够，用GAN来凑！](http://mp.weixin.qq.com/s?__biz=MzIwMTE1NjQxMQ==&mid=2247487613&idx=1&sn=8b1ae56d22f3fd697dd7bb191ee98ddc&chksm=96f36229a184eb3febbd02e192fe45e89dd1424e120a20e81dfd04fd57592637ab18ea64e388&scene=21#wechat_redirect)

大大丰富了医学影像分割的数据，有效提升了分割质量。



现在可以使用U-GAT-IT来一波神笔马良的操作了～



论文地址：

https://arxiv.org/pdf/1907.10830.pdf



TensorFlow版代码：

https://github.com/taki0112/UGATIT



PyTorch版代码：

https://github.com/znxlwm/UGATIT-pytorch