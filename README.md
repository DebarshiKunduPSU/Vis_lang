## BLIP: Bootstrapping Language-Image Pre-training for Unified Vision-Language Understanding and Generation



<img src="BLIP.gif" width="700">

This is the PyTorch code of the <a href="https://arxiv.org/abs/2201.12086">BLIP paper</a> [[blog](https://blog.salesforceairesearch.com/blip-bootstrapping-language-image-pretraining/)]. The code has been tested on PyTorch 1.10.
To install the dependencies, run <pre/>pip install -r requirements.txt</pre> 

Catalog:
- [x] Inference demo
- [x] Pre-trained and finetuned checkpoints
- [x] Finetuning code for Image-Text Retrieval, Image Captioning, VQA, and NLVR2
- [x] Pre-training code
- [x] Zero-shot video-text retrieval
- [x] Download of bootstrapped pre-training datasets 



### Pre-trained checkpoints:
Num. pre-train images | BLIP w/ ViT-B | BLIP w/ ViT-B and CapFilt-L | BLIP w/ ViT-L 
--- | :---: | :---: | :---: 
14M | <a href="https://storage.googleapis.com/sfr-vision-language-research/BLIP/models/model_base_14M.pth">Download</a>| - | -
129M | <a href="https://storage.googleapis.com/sfr-vision-language-research/BLIP/models/model_base.pth">Download</a>| <a href="https://storage.googleapis.com/sfr-vision-language-research/BLIP/models/model_base_capfilt_large.pth">Download</a> | <a href="https://storage.googleapis.com/sfr-vision-language-research/BLIP/models/model_large.pth">Download</a>



### Image-Text Retrieval:
1. Download COCO and Flickr30k datasets from the original websites, and set 'image_root' in configs/retrieval_{dataset}.yaml accordingly.
2. To evaluate the finetuned BLIP model on COCO, run:
<pre>python -m torch.distributed.run --nproc_per_node=8 train_retrieval.py \
--config ./configs/retrieval_coco.yaml \
--output_dir output/retrieval_coco \
--evaluate</pre> 
3. To finetune the pre-trained checkpoint using 8 A100 GPUs, first set 'pretrained' in configs/retrieval_coco.yaml as "https://storage.googleapis.com/sfr-vision-language-research/BLIP/models/model_base.pth". Then run:
<pre>python -m torch.distributed.run --nproc_per_node=8 train_retrieval.py \
--config ./configs/retrieval_coco.yaml \
--output_dir output/retrieval_coco </pre> 


### Acknowledgement
The implementation of BLIP relies on resources from <a href="https://github.com/salesforce/ALBEF">ALBEF</a>, <a href="https://github.com/huggingface/transformers">Huggingface Transformers</a>, and <a href="https://github.com/rwightman/pytorch-image-models/tree/master/timm">timm</a>. We thank the original authors for their open-sourcing.
