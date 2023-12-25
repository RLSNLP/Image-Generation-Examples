使用Huggingface官方的代码进行训练，用的是stable-diffusion-xl。  
代码：  
https://github.com/huggingface/diffusers/tree/main/examples/controlnet  
但是这个页面提供的inference代码有问题，需要用：  
https://huggingface.co/docs/diffusers/api/pipelines/controlnet_sdxl  

```python
# !pip install opencv-python transformers accelerate
from diffusers import StableDiffusionXLControlNetPipeline, ControlNetModel, AutoencoderKL
from diffusers.utils import load_image
import numpy as np
import torch
import cv2
from PIL import Image
prompt = "aerial view, a futuristic research complex in a bright foggy jungle, hard lighting"
negative_prompt = "low quality, bad quality, sketches"
# download an image
image = load_image(
"https://hf.co/datasets/hf-internal-testing/diffusers-images/resolve/main/sd_controlnet/hf-logo.png"
)
# initialize the models and pipeline
controlnet_conditioning_scale = 0.5 # recommended for good generalization
controlnet = ControlNetModel.from_pretrained(
"diffusers/controlnet-canny-sdxl-1.0", torch_dtype=torch.float16
)
vae = AutoencoderKL.from_pretrained("madebyollin/sdxl-vae-fp16-fix", torch_dtype=torch.float16)
pipe = StableDiffusionXLControlNetPipeline.from_pretrained(
"stabilityai/stable-diffusion-xl-base-1.0", controlnet=controlnet, vae=vae, torch_dtype=torch.float16
)
pipe.enable_model_cpu_offload()
# get canny image
image = np.array(image)
image = cv2.Canny(image, 100, 200)
image = image[:, :, None]
image = np.concatenate([image, image, image], axis=2)
canny_image = Image.fromarray(image)
# generate image
image = pipe(
prompt, controlnet_conditioning_scale=controlnet_conditioning_scale, image=canny_image
).images[0]
```

cv2.Canny的作用是把原始图片变成线性图。其中VAE不需要添加，保持pipe的默认就好。如果遇到精度问题，把type改成float32。

自定义数据集  
仿照fill50k数据集建立自己的数据集。  
在.sh文件里面去掉--dataset_name这项参数，改为使用–train_data_dir。  
在这个文件夹里，建立两个文件夹，分别存放原始图片和conditioning图片。还需要建立一个与文件夹同名的.py文件。  
最后建立一个名为metadata的jsonl文件，具体格式如下所示。  
