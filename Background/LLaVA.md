论文链接：https://llava-vl.github.io/  
知乎：https://zhuanlan.zhihu.com/p/625723805  
论文的贡献是Instruction Tuning  
首先使用图片的caption和bounding box来prompt GPT-4生成三种问题，仅使用了文字，获得了158K大小的数据集。  

模型结构:  

LLM使用的是Vicuna，Vision Encoder使用的是ViT-L/14，Projection用的是简单的线性层。  
Xq的格式如下所示，仅需要让LLM预测绿色部分。  

模型使用了二阶段的训练  
第一阶段使用了image-text pairs，共595K。仅训练了Projection层，使得视觉信息和文本信息对齐。  
第二阶段使用了构造的Instruction Tuning dataset，训练Projection层和LLM。  

LLaVA v1.5做出的改进：
对构造instruction的prompt做出了修改，使模型更容易理解。  
Projection层改成用两层的MLP。  
使用了更多的学术的VQA数据集。  
提升了图片的分辨率，从224提升到336。将LLM的规模从7B增加到13B。  
