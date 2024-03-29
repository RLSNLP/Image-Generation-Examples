论文链接：https://arxiv.org/pdf/2107.07651.pdf  
知乎链接：https://zhuanlan.zhihu.com/p/517907790  
更详细且有用的版本：https://zhuanlan.zhihu.com/p/619501914  
ALBEF的主要创新点为：  
通过ITC任务实现了图像向量和文本向量的对齐；  
使用ViT代替了图像检测模块，抽取图像特征，减少了图像的标注成本；  
通过Momentum Distillation的方式，降低了训练数据中噪声的影响。  
三个预训练任务：masked language modeling (MLM)  image-text matching (ITM, 根据<CLS>判断图片和文本输入是否是一对）  image-text contrastive learning （ITC, 将图片的embedding和文本信息的embedding求余弦相似度） 。  
一个好的多模态模型，图像编码器要足够大，同时多模态编码器也要大，文本编码器不需要特别大。  
Image encoder是ViT，Text Encoder是BERT的前六层，Multimodal Encoder是BERT的后六层。  
特别关注动量蒸馏，如果有需要就详细看。  

![image](https://github.com/RLSNLP/Image-Generation-Examples/blob/main/Background/images/albef.png)
