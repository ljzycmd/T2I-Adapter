## MasaCtrl with T2I-Adapter

This repo contains the implementation of [MasaCtrl](https://github.com/TencentARC/MasaCtrl) integrated to controllable diffusion model [T2I-Adapter](https://github.com/TencentARC/T2I-Adapter).

---

<!-- <div align="center">
<img src="https://huggingface.co/TencentARC/MasaCtrl/resolve/main/assets/overview.gif">
<i> MasaCtrl enables performing various consistent non-rigid image synthesis and editing without fine-tuning and optimization. </i>
</div> -->


## Introduction

We propose MasaCtrl, a tuning-free method for non-rigid consistent image synthesis and editing. The key idea is to combine the `contents` from the *source image* and the `layout` synthesized from *text prompt and additional controls* into the desired synthesized or edited image, with **Mutual Self-Attention Control**.


## Main Features

### 1 Controllable Consistent Image Synthesis and Editing

Directly modifying the text prompts often cannot generate target layout of desired image, thus we further integrate our method into existing proposed controllable diffusion pipelines (like T2I-Adapter and ControlNet) to obtain stable synthesis and editing results.

>*The target layout controlled by additional guidance.*

<div align="center">
<img src="https://huggingface.co/TencentARC/MasaCtrl/resolve/main/assets/results_w_adapter.png">
<i>Synthesis (left part) and editing (right part) results with T2I-Adapter</i>
</div>

### 2 Consistent Video Synthesis

With dense consistent guidance, MasaCtrl enables video synthesis

<div align="center">
<img src="https://huggingface.co/TencentARC/MasaCtrl/resolve/main/assets/results_w_adapter_consistent.png">
<i>Video Synthesis Results (with keypose and canny guidance)</i>
</div>


## Usage
### Install

Please refer to usage guide of T2I-Adapter [here](README_adapter.md) (or from official [repo](https://github.com/TencentARC/T2I-Adapter)) and download pretrained guidance models.

### Checkpoints

**Stable Diffusion:**

You can download these checkpoints on their official repository and [Hugging Face](https://huggingface.co/).

**Personalized Models:**
You can download personlized models from [CIVITAI](https://civitai.com/) or train your own customized models.

### Start

For controllable synthesis:

```bash
python masactrl_w_adapter.py \
--which_cond sketch \
--cond_path_src SOURCE_CONDITION_PATH \
--cond_path CONDITION_PATH \
--cond_inp_type sketch \
--prompt_src "A bear walking in the forest" \
--prompt "A bear standing in the forest" \
--sd_ckpt models/sd-v1-4.ckpt \
--resize_short_edge 512 \
--cond_tau 1.0 \
--cond_weight 1.0 \
--n_samples 1 \
--adapter_ckpt models/t2iadapter_sketch_sd14v1.pth
```

NOTE: You can download the sketch examples [here](https://huggingface.co/TencentARC/MasaCtrl/tree/main/sketch_example).

For real image editing:

```bash
python masactrl_w_adapter.py \
--src_img_path SOURCE_IMAGE_PATH \
--cond_path CONDITION_PATH \
--cond_inp_type image \
--prompt_src "" \
--prompt "a photo of a man wearing black t-shirt, giving a thumbs up" \
--sd_ckpt models/sd-v1-4.ckpt \
--resize_short_edge 512 \
--cond_tau 1.0 \
--cond_weight 1.0 \
--n_samples 1 \
--which_cond sketch \
--adapter_ckpt models/t2iadapter_sketch_sd14v1.pth \
--outdir ./workdir/masactrl_w_adapter_inversion/black-shirt
```

NOTE: You can download the real image editing example [here](https://huggingface.co/TencentARC/MasaCtrl/tree/main/black_shirt_example).

## Acknowledgements

We thank the awesome research works [Prompt-to-Prompt](https://github.com/google/prompt-to-prompt), [T2I-Adapter](https://github.com/TencentARC/T2I-Adapter).


## Contact

If your have any comments or questions, please [open a new issue](https://github.com/TencentARC/MasaCtrl/issues/new/choose) or feel free to contact [Mingdeng Cao](https://github.com/ljzycmd) and [Xintao Wang](https://xinntao.github.io/).