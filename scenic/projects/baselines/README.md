## Scenic baseline models
This directory contains several baseline vision models implemented in Scenic.
These models span a range of architectures, as well as tasks.

They include:

 * [Vision Transformer](https://arxiv.org/abs/2010.11929) (ViT) for image classification. [[Official Implementation](https://github.com/google-research/vision_transformer#vision-transformer)]
 * [Detection Transformer](https://arxiv.org/abs/2005.12872) (DETR) for object detection. [[Official PyTorch Implementation](https://github.com/facebookresearch/detr)]
 * [MLP-Mixer](https://arxiv.org/abs/2105.01601) an all-MLP model for image classification. [[Official Implementation](https://github.com/google-research/vision_transformer#mlp-mixer)]
 * [CLIP](https://arxiv.org/abs/2103.00020) for learning visual concepts from natural language supervision [[Official Implementation](https://github.com/openai/CLIP/tree/main/clip)]
 * [Residual Networks](https://arxiv.org/abs/1512.03385) (ResNet) for image classification.
 * [Big Transfer ResNet](https://arxiv.org/abs/1912.11370) (BitResNet) for image classification. [[Official Implementation](https://github.com/google-research/big_transfer)]
 * [UNet](http://arxiv.org/abs/1505.04597) for semantic segmentation.
 * [Axial-ResNet](https://arxiv.org/abs/2003.07853) for image classification. [[Official TF Implementation](https://github.com/csrhddlam/axial-deeplab)]


## Model Zoo

### Vision Transformers
We share checkpoints of models from the following papers, trained on various
datasets:

- **ViT**: [An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale](https://arxiv.org/abs/2010.11929)
- **ViT-AugReg:** [How to train your ViT? Data, Augmentation, and Regularization in Vision Transformers](https://arxiv.org/abs/2106.10270)
  For the `ImageNet-21K`-pre-trained checkpoints we are using the "recommended
  checkpoints" (see paper section 4.5). The `ImageNet Accuracy` numbers are
  after fine-tuning (resolution 224px) as described in Appendix B. For more
  information see https://github.com/google-research/vision_transformer/

| Model | Dataset | Pretraining | ImageNet Accuracy | Checkpoint |
|-------|:-:|:-:|:-:|:-:|
| ViT-B/16            | ImageNet |       -        |  74.1 |  [Link](https://storage.googleapis.com/scenic-bucket/baselines/ViT_B_16_ImageNet1k) |
| ViT-AugReg-B/16     | ImageNet |       -        |  79.7 |  [Link](https://storage.googleapis.com/scenic-bucket/baselines/ViT-AugReg_B_16_ImageNet1k) |
| ViT-B/32            |     -    |  ImageNet-21K  |   -   |  [Link](https://storage.googleapis.com/scenic-bucket/baselines/ViT_B_32_ImageNet21k) |
| ViT-B/16            |     -    |  ImageNet-21K  |   -   |  [Link](https://storage.googleapis.com/scenic-bucket/baselines/ViT_B_16_ImageNet21k) |
| ViT-L/32            |     -    |  ImageNet-21K  |   -   |  [Link](https://storage.googleapis.com/scenic-bucket/baselines/ViT_L_32_ImageNet21k) |
| ViT-L/16            |     -    |  ImageNet-21K  |   -   |  [Link](https://storage.googleapis.com/scenic-bucket/baselines/ViT_L_16_ImageNet21k) |
| ViT-AugReg-B/32     |     -    |  ImageNet-21K  |  79.1 |  [Link](https://storage.googleapis.com/vit_models/augreg/B_32-i21k-300ep-lr_0.001-aug_light1-wd_0.1-do_0.0-sd_0.0.npz) |
| ViT-AugReg-B/16     |     -    |  ImageNet-21K  |  84.0 |  [Link](https://storage.googleapis.com/vit_models/augreg/B_16-i21k-300ep-lr_0.001-aug_medium1-wd_0.1-do_0.0-sd_0.0.npz) |

The AugReg params can be directly loaded into a `train_state`:

```python
train_state_with_augreg_params = model.load_augreg_params(
    train_state,
    # Can read directly from storage bucket. Filename must start with model name
    # ("B_32-" in this case).
    'gs://vit_models/augreg/B_32-i21k-300ep-lr_0.001-aug_light1-wd_0.1-do_0.0-sd_0.0.npz',
    # Config is checked against AugReg config.
    config.model)
```


### ResNet
We share checkpoints of models from the following papers, trained on ImageNet:

- **ResNet**: [Deep Residual Learning for Image Recognition](https://arxiv.org/abs/1512.03385)
- **BiTResNet**: [Big Transfer (BiT): General Visual Representation Learning](https://arxiv.org/abs/1912.11370)

| Model | Dataset | Pretraining | ImageNet Accuracy | Checkpoint |
|-------|:-:|:-:|:-:|:-:|
| ResNet50         | ImageNet |       -        |  76.1 |  [Link](https://storage.googleapis.com/scenic-bucket/baselines/ResNet50_ImageNet1k) |
| BiTResNet50      | ImageNet |       -        |  77.0 |  [Link](https://storage.googleapis.com/scenic-bucket/baselines/BiTResNet50_ImageNet1k) |

### DETR
Please check [DETR directory](detr) for more information and link to download
pretrained checkpoints.
