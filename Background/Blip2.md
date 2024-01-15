论文链接：https://arxiv.org/pdf/2301.12597.pdf  
知乎链接：https://zhuanlan.zhihu.com/p/653902791

![image](https://github.com/RLSNLP/Image-Generation-Examples/blob/main/Background/images/blip-2-1.png)

BLIP2的Image Encoder和LLM Decoder是Freeze的，训练的是Q-Former。在Q-Former中，文字和图片共享的是Self Attention层，如果输入的是Learned Queries，则需要过Cross Attention和Feed Forward层（Image Transformer）。如果输入的是Text，则需要过单独的Feed Forward层（Text Transformer）。Q-Former用于弥补视觉和语言两种模态的Modality Gap。  

Learned Queries的长度是32*768，因此输出的维度也是32*768，小于Image-Encoder的输出257*1024。  

为了减少计算成本并避免灾难性遗忘，进行了两阶段的预训练。Transformer使用BERT作为初始化。  
第一阶段是表示学习，用ITC+ITM+ITG三个loss联合训练。在实际操作中，将Q和T concat起来输入transformer中，所以用Attention mask，避免它们相互影响。  
其中，ITM将Query之后的输出过一个额外的分类器，判断图和文本是否匹配。构建负样本对的方法参考了ALBEF。  
ITG是以Learned Queries作为Prefix的Language Model Loss  
ITC是将Image Transformer输出的Queries的每一维与Text Transformer输出的文本表示算一个相似度，然后选择最高的作为图文相似度。与0，1算出loss。  

![image](https://github.com/RLSNLP/Image-Generation-Examples/blob/main/Background/images/blip-2-2.png)

第二阶段是生成学习，添加了一个全连接层将Image Transformer的输出映射成LLM的维度。下游任务的大模型是Freeze住的。  

![image](https://github.com/RLSNLP/Image-Generation-Examples/blob/main/Background/images/blip-2-3.png)

只有在VQA finetuning的时候才会用到Text Transformer  
