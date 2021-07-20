传统CNN输入图片是固定大小的原因
===
对于CNN，一幅输入图片在经过卷积和pooling层时，这些层是不关心图片大小的。<br>
比如对于一个卷积层，outputsize = (inputsize - kernelsize) / stride + 1，它并不关心inputsize多大，对于一个inputsize大小的输入feature map，滑窗卷积，输出outputsize大小的feature map即可(主要是这里的卷积核个数K可以自己指定)。pooling层同理。<br>
但是在进入全连接层时，feature map（假设大小为n×n）要拉成一条向量，而向量中每个元素（共n×n个）作为一个结点都要与下一个层的所有结点（假设4096个）全连接，这里的权值个数是4096×n×n，而我们知道神经网络结构一旦确定，它的权值个数都是固定的，所以这个n不能变化。<br>
n是conv5的outputsize，所以层层向回看，每个outputsize都要固定，那每个inputsize都要固定，因此输入图片大小要固定。<br>
