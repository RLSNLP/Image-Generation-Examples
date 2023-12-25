原始论文： 
https://arxiv.org/abs/2005.12872  
DETR详解：  
https://zhuanlan.zhihu.com/p/387102036  
残差网络详解：  
https://zhuanlan.zhihu.com/p/42706477  

将Transformer模型用于目标检测任务，没有使用预训练。  
DETR由四个主要模块组成：backbone，编码器，解码器以及预测头。  
DETR的backbone是经典的卷积网络，在实验中作者使用的是ResNet-50或者ResNet-101作为基础网络。  
DETR的编码器就是Transformer的Encoder，输入是Image feature。  
DETR的解码器与Transformer不一样，一次性得到 N 个结果（非自回归），这点和原始的Transformer的自回归计算是不同的。  
DERT的预测头是一个三层的FFN，每个Object queries通过预测头预测目标的bounding box和类别，其中bounding box有三个值，分别是目标的中心点以及宽和高。  

特别注意DETR的解码器输入，是由Archor Box事先划定好的N个框。N是一个超参数，远大于实际目标数，超过目标个数的ground truth使用背景元素来作为负样本。  
