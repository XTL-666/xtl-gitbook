# 第三篇:（A Neural Algorithm of Artistic Style\)

利用神经网络进行提取

（模电考试完，有时间更了）（利用pretrain的Pre-trained VGG network model）来分别做Content、Style的reconstruction，在合成时考虑content loss 与style loss的最小化（其实还包括去噪变化的的loss），这样合成出来的图像会保证在content 和style的重构上更准确。废话不多说看图。

![](https://gblobscdn.gitbook.com/assets%2F-MR3FOdSWIFY1yDqfjZ2%2F-MR9H5fXn5dAu97wvyXB%2F-MR9IivUvvFt-pjHpSjb%2Fv2-b3c1cb0342d7c436df2ef6888b023d9e_r%20%281%29.jpg?alt=media&token=ff8d927e-6ed7-428b-9396-1ba12fcbba99)

* Content Reconstruction: 上图中下面部分是Content Reconstruction对应于CNN中的a，b，c，d，e层，注意最开始标了Content Representations的部分不是原始图片（可以理解是给计算机比如分类器看的图片，因此如果可视化它，可能完全就不知道是什么内容），而是经过了Pre-trained之后的VGG network model的图像数据， 该model主要用来做object recognition， 这里主要用来生成图像的Content Representations。理解了这里，后面就比较容易了，经过五层卷积网络来做Content的重构，文章作者实验发现在前3层的Content Reconstruction效果比较好，d，e两层丢失了部分细节信息，保留了比较high-level的信息。
* Style Reconstruction： Style的重构比较复杂，很难去模型化Style这个东西，Style Represention的生成也是和Content Representation的生成类似，也是由VGG network model去做的，不同点在于a,b,c,d,e的处理方式不同，Style Represention的Reconstruction是在CNN的不同的子集上来计算的，怎么说呢，它会分别构造conv1\_1\(a\),[conv 1\_1, conv2\_1](https://b/),\[conv1\_1, conv2\_1, conv3\_1\],\[conv1\_1, conv2\_1, conv3\_1,conv4\_1\],\[conv1\_1, conv2\_1, conv3\_1, conv4\_1, conv5\_1\]。这样重构的Style 会在各个不同的尺度上更加匹配图像本身的style，忽略场景的全局信息.

