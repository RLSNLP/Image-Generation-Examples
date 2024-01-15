论文链接：https://arxiv.org/pdf/2201.12086.pdf  
知乎链接：https://zhuanlan.zhihu.com/p/521260597  

![image](https://github.com/RLSNLP/Image-Generation-Examples/blob/main/Background/images/blip-1.png)

颜色相同的模块是共享参数的。训练时每个图文对只过一次Image Encoder，过三次Text Encoder。  
和ALBEF相比，MLM预训练任务变成了LM任务。  

![image](https://github.com/RLSNLP/Image-Generation-Examples/blob/main/Background/images/blip-1-1.png) 

预训练数据（Web texts）中包含了大量噪声。所以先用高质量数据finetune一下Encoder和Decoder。然后对于图片，生成一个伪标题。判断{Iw, Tw}和{Iw, Ts}是否是符合要求的。如果符合，就用来作为合成的数据去训练BLIP，循环往复进行。本质上是数据增强的方法。
两大优势  
（1）模型既有encoder模块又有decoder模块，在预训练中统一了多模态理解与多模态生成任务；  
（2）利用数据扩充与数据清洗（CapFilt）进一步提升了模型的效果。  
