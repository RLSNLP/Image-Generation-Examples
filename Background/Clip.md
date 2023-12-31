原始论文： 
https://arxiv.org/pdf/2103.00020.pdf  
详解：  
https://zhuanlan.zhihu.com/p/486857682  

OpenAI收集了大量的文本-图片对，无监督地联合训练了一个Text Encoder with Image Encoder。  
特别关注其训练任务。文本的表征和图片的表征相乘之后，分别与文本表征和图片表征的cross entropy loss都是最小。  
下游任务是zero-shot的。给Text Encoder设计一个Prompt，生成一个向量。再把Image Encoder得到的向量与该向量进行匹配，选取cosine similarity最大的作为结果。  
看一下CLIP的缺点，比如zero-shot设置下某些任务表现不佳，out-of-distribution的任务无法解决。  
模型足够优秀，还是要多关注预训练用的data。  
