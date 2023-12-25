原始论文：  
https://arxiv.org/pdf/2010.11929.pdf  
Transformer基本结构和原理详解： 
https://zhuanlan.zhihu.com/p/340149804  
从Vision Transformer开始  
https://zhuanlan.zhihu.com/p/445122996  
https://cloud.tencent.com/developer/article/1758068  

ViT只用到了Transformer的Encoder部分。  
在NLP中，模型的输入是一串字符经过Embedding变成的向量。在CV中有所区别。比如有张图片的尺寸是32*32，按照16*16将图片切成4个patch。每个像素点由三个通道值（RGB）组成，所以每个patch可以组成16*16*3=768维度的向量。  
这张图片变成了4*768的矩阵。在实际中，像BERT一样会加入一个cls符号用来做理解，实际长度变为5*768。  
在大训练数据的情况下，ViT的结果好于ResNet。如果没有足够的训练数据，结果较差。  
其他需要注意的知识点：ViT的相对Position Embedding是如何实现的？  
