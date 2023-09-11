# SAM.cpp

This repository integrates [sam-cpp](https://github.com/ggerganov/ggml/tree/master/examples/sam) and [ggml](https://github.com/ggerganov/ggml) into Visual Studio. Sam-cpp is a pure C/C++ implementation of Meta's [Segment Anything Model](https://github.com/facebookresearch/segment-anything/). The repo doesn't require any additional library and dependencies.

## Description

The example currently supports only the [ViT-B SAM model checkpoint](https://huggingface.co/facebook/sam-vit-base).

## Quick start
In visual studio, set to build in `Release` mode with the `x64`.
### 1. Download model
```
Download [ggml-model-f16.bin](https://drive.google.com/file/d/1n25nEYFyM3-Wyaliftru3IfIJB9lsJYz/view?usp=drive_link)
```
### 2. Run inference
```
Release/main.exe -t 16 -i img.jpg -m models/ggml-model-f16.bin
```

## Downloading and converting the model checkpoints

You can download a [model checkpoint](https://github.com/facebookresearch/segment-anything/tree/main#model-checkpoints) and convert it to `ggml` format using the script `convert-pth-to-ggml.py`:

```
# Convert PTH model to ggml
python convert-pth-to-ggml.py models/sam_vit_b_01ec64.pth . 1
```

## Example output on M2 Ultra
```
 $ ▶ Release/main.exe -t 16 -i img.jpg -m examples/sam/ggml-model-f16.bin
main: seed = 1694396520
main: loaded image 'img.jpg' (680 x 453)
sam_image_preprocess: scale = 0.664062
main: preprocessed image (1024 x 1024)
sam_model_load: loading model from '\models\ggml-model-f16.bin' - please wait ...
sam_model_load: n_enc_state      = 768
sam_model_load: n_enc_layer      = 12
sam_model_load: n_enc_head       = 12
sam_model_load: n_enc_out_chans  = 256
sam_model_load: n_pt_embd        = 4
sam_model_load: ftype            = 1
sam_model_load: qntvr            = 0
operator (): ggml ctx size = 202.32 MB
sam_model_load: ...................................... done
sam_model_load: model size =   185.05 MB / num tensors = 304
embd_img
dims: 64 64 256 1 f32
First & Last 10 elements:
-0.05101 -0.06350 -0.07115 -0.06838 -0.06825 -0.06971 -0.07147 -0.07088 -0.06774 -0.05427
0.01575 0.01772 0.02244 0.01668 0.01755 0.01668 0.01795 0.02048 0.02101 0.03388
sum:  12757.156252

Skipping mask 0 with iou 0.705756 below threshold 0.880000
Skipping mask 1 with iou 0.762171 below threshold 0.880000
Mask 2: iou = 0.947049, stability_score = 0.956250, bbox (371, 436), (144, 168)
Inference done
```

Input point is (414.375, 162.796875) (currently hardcoded)

Input image:

![llamas](https://user-images.githubusercontent.com/8558655/261301565-37b7bf4b-bf91-40cf-8ec1-1532316e1612.jpg)

Output mask (mask_out_2.png in build folder):

![mask_glasses](https://user-images.githubusercontent.com/8558655/263706800-47eeea30-1457-4c87-938b-8f11536c5aa7.png)

## References

- [ggml](https://github.com/ggerganov/ggml)
- [SAM](https://segment-anything.com/)
- [SAM demo](https://segment-anything.com/demo)
- [sam-cpp](https://github.com/ggerganov/ggml/tree/master/examples/sam)
