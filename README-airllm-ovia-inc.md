# Ovia Inc — AirLLM (fork of lyogavin/airllm)

![Ovia Inc — AirLLM logo from the upstream project assets](assets/airllm_logo.png)

We maintain this fork of [lyogavin/airllm](https://github.com/lyogavin/airllm), AirLLM: inference that dramatically reduces memory use, letting large language models run on a single small GPU — 70B models on a single 4GB GPU card without quantization, distillation, or pruning, with larger results recorded upstream for 405B, DeepSeek-V3, and sparse mixture-of-experts models. Upstream credit: lyogavin and the AirLLM contributors. Licence: Apache-2.0 (see LICENSE).

**Our main site:** https://oviainc.github.io/ai-services/

**Upstream repository:** https://github.com/lyogavin/airllm

## What this is

The infrastructure shelf of our collection, held for local large-model inference on limited hardware:

- The complete upstream project at the fork point (Python, the `air_llm` package, `examples/`, `eval/`, `training/`, `rlhf/`, `scripts/`, and `requirements.txt`): layer-by-layer and, for sparse models, expert-by-expert streaming that keeps only the part of a model needed for the current step in GPU memory.
- The model results recorded in the upstream README preserved below: 70B on 4GB, Llama 3.1 405B on 8GB, DeepSeek-V3 (671B) on about 12GB, and Kimi K3 (2.8T) on under 4GB, plus Qwen3.8-27B support added in the August 2026 updates at the fork point.
- A single `AutoModel` entry point across model families, with configurations for compression (recorded upstream as a 3x inference speed-up), 8-bit and 4-bit quantization options, CPU inference, and macOS support.
- Example notebooks and supporting material for the supported-model list preserved below, covering Llama, Qwen, DeepSeek, Mistral, ChatGLM, Baichuan, InternLM, Phi, Gemma, and further families named upstream.

No project homepage is recorded on the fork or upstream at this pass, so no homepage is proposed. Upstream carries about 43,399 stars and a large fork network at the time of this pass.

## Story

AirLLM opened as a public project on June 12, 2023, under lyogavin, with an initial version recorded in the upstream updates on November 20, 2023. The upstream record preserved below shows the shape of the work from the start: safetensors support and the top open models in December 2023, compression for a 3x speed-up, prefetching to overlap loading and compute, an `AutoModel` that detects model type without a model class argument, macOS support for 70B models, and then steady expansion — Llama 3, Llama 3.1 405B, quantization options, CPU inference, Qwen2.5, and the 2026 generation of very large and sparse models through one entry point. The companion Anima work in this repository (`anima_100k`, `anima_logo.png`) sits beside the inference core as part of the upstream project as received.

We forked the project on August 21, 2026, at the August 20, 2026 snapshot (tip commit 8e45623, a star-history refresh over the Qwen3.8-27B support release), into the infrastructure and other group of the Oviainc collection. In role, this fork is the local-inference seat of that group: where the cloud shelves hold emulators and access layers, this fork holds a way to run very large open models on a single small GPU on own hardware, at no cloud cost. That shape matches the standing preference for local, low-cost operation wherever the work allows, and gives evaluation a path that does not wait on rented accelerators.

What we evaluate here is the inference trade in practice, with its limits kept visible:

- **Memory against speed** — streaming layers and experts from disk cuts memory dramatically; the cost is throughput. Prefetching and compression numbers recorded upstream are the claims to test on own hardware and own models, not to repeat as results.
- **Model coverage in practice** — the supported list is broad and still growing upstream; which families load cleanly through `AutoModel`, and which need version-pinned dependencies (the upstream Kimi K3 notes name exact transformer and attention requirements), decides real usability.
- **Local fit** — a 4GB GPU path, CPU inference, and macOS support decide whether large-model checks can run beside agent and data work on machines already on hand, or still need a dedicated box.
- **Dependency and maintenance shape** — a fast upstream cadence, model-specific requirements, and gated-model handling in the FAQ preserved below decide the upkeep cost of staying current.

Where the project fits our work:

- **AI agents** — agent systems need a model behind the harness; a local path to large open models allows harness, tool, and prompt behaviour to be checked without a hosted API in the loop and without per-call spend.
- **Context engineering** — larger local models change what fits in a working evaluation: long-context behaviour, compression trade-offs, and model choice for a given context budget can be tested directly rather than inferred from a hosted tier.
- **Business intelligence and data** — a lighter fit: local inference keeps document and data work on own hardware during evaluation, which matters when the material should not leave the building before a deployment shape is chosen.
- **Virtual production** — a lighter fit again: on-set and in-studio tools benefit from models that run on a single workstation GPU, with no cloud round trip, for drafting, tagging, and assistive steps in a media pipeline.

## Modifications by Ovia Inc

Documentation only. Upstream code and content are unchanged from the fork point, except for documentation notes added in November 2026: a modification reference on November 4, 2026, replaced by this expanded treatment (Ovia section, story, picture, and repository details) on November 25, 2026. Where a later commit in this repository says otherwise, that commit governs.

## Sync status

Behind upstream, by design of this pass. This fork carries the August 20, 2026 snapshot (tip commit 8e45623) plus documentation commits of our own (November 4, 2026, replaced and expanded November 25, 2026). A cross-repository compare at this pass records the fork as diverged, ahead by 1 documentation commit and behind by 144 commits, at merge base 8e45623, with upstream HEAD e8a270d pushed November 25, 2026, including the 4.0.1 release of November 23, 2026. No sync was applied in this pass, and a reviewed sync is recommended for Ja when the infrastructure shelf needs a current upstream base.

## Related repositories

- [ai-services](https://github.com/Oviainc/ai-services) — our flagship site: AI agents, machine learning in production, and AI products for business
- [ovia-inc-floci](https://github.com/Oviainc/ovia-inc-floci) — the local-cloud seat of the infrastructure shelf: a free local AWS emulator for development and testing on own hardware
- [ollama-ovia-inc](https://github.com/Oviainc/ollama-ovia-inc) — local model serving in the collection, held beside this fork for the local-inference comparison
- [OVIA-INC-MiniCPM-V](https://github.com/Oviainc/OVIA-INC-MiniCPM-V) — the perception layer of the video and multimodal shelf: small multimodal models for on-device work
- [token_reducer](https://github.com/Oviainc/token_reducer) — our own small context-engineering utility for reducing large text files, part of the same local, low-cost tooling preference

## Working with us

Start from our site: https://oviainc.github.io/ai-services/ — the contact form there is the fastest way to reach us.

## Licence

Apache-2.0, as recorded in the LICENSE file in this fork and upstream. Upstream credit remains with lyogavin and the AirLLM contributors.

---

Ovia Inc — Artificial Intelligence & Context Engineering. Based in Canada, working wherever the work is.

---

![airllm_logo](https://github.com/lyogavin/airllm/blob/main/assets/airllm_logo_sm.png?v=3&raw=true)

[**Quickstart**](#quickstart) | 
[**Configurations**](#configurations) | 
[**MacOS**](#macos) | 
[**Example notebooks**](#example-python-notebook) | 
[**FAQ**](#faq)

**AirLLM** dramatically reduces inference memory usage, letting 70B large language models run on a single 4GB GPU card — without quantization, distillation, or pruning. You can even run **405B Llama 3.1** on **8GB**, **DeepSeek-V3 (671B)** on **~12GB**, and **Kimi K3 (2.8T)** — the largest open-source model released to date — on **under 4GB**, because sparse MoE models stream one expert at a time rather than a whole layer.

<a href="https://github.com/lyogavin/airllm/stargazers">![GitHub Repo stars](https://img.shields.io/github/stars/lyogavin/airllm?style=social)</a>
[![Downloads](https://static.pepy.tech/personalized-badge/airllm?period=total&units=international_system&left_color=grey&right_color=blue&left_text=downloads)](https://pepy.tech/project/airllm)

[![Code License](https://img.shields.io/badge/Code%20License-Apache_2.0-green.svg)](https://github.com/LianjiaTech/BELLE/blob/main/LICENSE)
[![Generic badge](https://img.shields.io/badge/wechat-Anima-brightgreen?logo=wechat)](https://static.aicompose.cn/static/wecom_barcode.png?t=1671918938)
[![Discord](https://img.shields.io/discord/1175437549783760896?logo=discord&color=7289da
)](https://discord.gg/2xffU5sn)
[![PyPI - AirLLM](https://img.shields.io/pypi/format/airllm?logo=pypi&color=3571a3)
](https://pypi.org/project/airllm/)
[![Website](https://img.shields.io/website?up_message=blog&url=https%3A%2F%2Fmedium.com%2F%40lyo.gavin&logo=medium&color=black)](https://medium.com/@lyo.gavin)
[![Website](https://img.shields.io/badge/Gavin_Li-Blog-blue)](https://gavinliblog.com)
[![Support me on Patreon](https://img.shields.io/endpoint.svg?url=https%3A%2F%2Fshieldsio-patreon.vercel.app%2Fapi%3Fusername%3Dgavinli%26type%3Dpatrons&style=flat)](https://patreon.com/gavinli)
[![GitHub Sponsors](https://img.shields.io/github/sponsors/lyogavin?logo=GitHub&color=lightgray)](https://github.com/sponsors/lyogavin)

## AI Agents Recommendation:

* [Best AI Game Sprite Generator](https://godmodeai.co)

* [Best AI Facial Expression Editor](https://crazyfaceai.com)

* [Bloome — build & run AI agent teams in the cloud, zero setup](https://bloome.im/app?ref=G6BYnov0&utm_medium=github&utm_source=lyogavin-airllm-ivor-202606)

## Updates
[2026/08] **Qwen3.8-27B** support: Qwen's new dense VL (Gated DeltaNet + Gated Attention, native vision) runs in **3.33GB** of VRAM, measured end to end on one RTX 3090. Needs `transformers` 5.8+.

[2026/07] **Kimi K3 (2.8T)** support: the largest open-source model runs on a single card in **3.72GB** of VRAM, measured end to end on one RTX 6000 Ada. Per-expert streaming loads only the experts a token actually routes to. K3 brings three requirements of its own: `pip install compressed-tensors flash-attn` (its model code mandates flash attention regardless of what you request), a CUDA 12 build of torch, since no prebuilt flash-attn wheel exists for CUDA 13 yet, and `transformers` 4.56.x, as its remote code does not load on 5.x.

[2026/06] **v3.0**: FP8 model support + the latest models. Run **DeepSeek-V3 (671B) on ~12GB** and **Qwen3-235B on ~3GB**, plus Qwen3, Llama 3.x/4, DeepSeek V2/V3, Phi-4, Gemma and more — all through a single `AutoModel`.

[2024/08/20] v2.11.0: Support Qwen2.5

[2024/08/18] v2.10.1 Support CPU inference. Support non sharded models. Thanks @NavodPeiris for the great work! 

[2024/07/30] Support Llama3.1 **405B** ([example notebook](https://colab.research.google.com/github/lyogavin/airllm/blob/main/air_llm/examples/run_llama3.1_405B.ipynb)). Support **8bit/4bit quantization**.

[2024/04/20] AirLLM supports Llama3 natively already. Run Llama3 70B on 4GB single GPU.

[2023/12/25] v2.8.2: Support MacOS running 70B large language models.

[2023/12/20] v2.7: Support AirLLMMixtral. 

[2023/12/20] v2.6: Added AutoModel, automatically detect model type, no need to provide model class to initialize model.

[2023/12/18] v2.5: added prefetching to overlap the model loading and compute. 10% speed improvement.

[2023/12/03] added support of **ChatGLM**, **QWen**, **Baichuan**, **Mistral**, **InternLM**!

[2023/12/02] added support for safetensors. Now support all top 10 models in open llm leaderboard.

[2023/12/01] airllm 2.0. Support compressions: **3x run time speed up!**

[2023/11/20] airllm Initial version!

## Star History

<a href="https://star-history.com/#lyogavin/airllm&Timeline">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/star-history-dark.png">
    <img alt="Star History Chart" src="assets/star-history.png">
  </picture>
</a>

## Table of Contents

* [Quick start](#quickstart)
* [Model Compression](#model-compression---3x-inference-speed-up)
* [Configurations](#configurations)
* [Run on MacOS](#macos)
* [Example notebooks](#example-python-notebook)
* [Supported Models](#supported-models)
* [Acknowledgement](#acknowledgement)
* [FAQ](#faq)

## Quickstart

### 1. Install package

First, install the airllm pip package.

```bash
pip install airllm
```

### 2. Inference

Then, initialize AirLLMLlama2, pass in the huggingface repo ID of the model being used, or the local path, and inference can be performed similar to a regular transformer model.

(*You can also specify the path to save the splitted layered model through **layer_shards_saving_path** when init AirLLMLlama2.*

```python
from airllm import AutoModel

MAX_LENGTH = 128
# just pass a hugging face repo id — works with almost any popular model:
model = AutoModel.from_pretrained("Qwen/Qwen3-32B")

# go bigger with the exact same one line:
#model = AutoModel.from_pretrained("Qwen/Qwen3.8-27B")          # 27B dense VL, 3.33GB
#model = AutoModel.from_pretrained("Qwen/Qwen3-235B-A22B")     # 235B, runs in ~3GB
#model = AutoModel.from_pretrained("deepseek-ai/DeepSeek-V3")  # 671B, runs in ~12GB

# or use a model's local path...
#model = AutoModel.from_pretrained("/home/ubuntu/.cache/huggingface/hub/models--Qwen--Qwen3-32B/snapshots/...")

input_text = [
        'What is the capital of United States?',
        #'I like',
    ]

input_tokens = model.tokenizer(input_text,
    return_tensors="pt", 
    return_attention_mask=False, 
    truncation=True, 
    max_length=MAX_LENGTH, 
    padding=False)
           
generation_output = model.generate(
    input_tokens['input_ids'].cuda(), 
    max_new_tokens=20,
    use_cache=True,
    return_dict_in_generate=True)

output = model.tokenizer.decode(generation_output.sequences[0])

print(output)

```
 
 
Note: During inference, the original model will first be decomposed and saved layer-wise. Please ensure there is sufficient disk space in the huggingface cache directory.
 

## Model Compression - 3x Inference Speed Up!

We just added model compression based on block-wise quantization-based model compression. Which can further **speed up the inference speed** for up to **3x** , with **almost ignorable accuracy loss!** (see more performance evaluation and why we use block-wise quantization in [this paper](https://arxiv.org/abs/2212.09720))

![speed_improvement](https://github.com/lyogavin/airllm/blob/main/assets/airllm2_time_improvement.png?v=2&raw=true)

#### How to enable model compression speed up:

* Step 1. make sure you have [bitsandbytes](https://github.com/TimDettmers/bitsandbytes) installed by `pip install -U bitsandbytes `
* Step 2. make sure airllm verion later than 2.0.0: `pip install -U airllm` 
* Step 3. when initialize the model, passing the argument compression ('4bit' or '8bit'):

```python
model = AutoModel.from_pretrained("garage-bAInd/Platypus2-70B-instruct",
                     compression='4bit' # specify '8bit' for 8-bit block-wise quantization 
                    )
```

#### What are the differences between model compression and quantization?

Quantization normally needs to quantize both weights and activations to really speed things up. Which makes it harder to maintain accuracy and avoid the impact of outliers in all kinds of inputs.

While in our case the bottleneck is mainly at the disk loading, we only need to make the model loading size smaller. So, we get to only quantize the weights' part, which is easier to ensure the accuracy.

## Configurations
 
When initialize the model, we support the following configurations:

* **compression**: supported options: 4bit, 8bit for 4-bit or 8-bit block-wise quantization, or by default None for no compression
* **profiling_mode**: supported options: True to output time consumptions or by default False
* **layer_shards_saving_path**: optionally another path to save the splitted model
* **hf_token**: huggingface token can be provided here if downloading gated models like: *meta-llama/Llama-2-7b-hf*
* **prefetching**: prefetching to overlap the model loading and compute. By default, turned on. For now, only AirLLMLlama2 supports this.
* **delete_original**: if you don't have too much disk space, you can set delete_original to true to delete the original downloaded hugging face model, only keep the transformed one to save half of the disk space. 

## MacOS

Just install airllm and run the code the same as on linux. See more in [Quick Start](#quickstart).

* make sure you installed [mlx](https://github.com/ml-explore/mlx?tab=readme-ov-file#installation) and torch
* you probably need to install python native see more [here](https://stackoverflow.com/a/65432861/21230266)
* only [Apple silicon](https://support.apple.com/en-us/HT211814) is supported

Example [python notebook] (https://github.com/lyogavin/airllm/blob/main/air_llm/examples/run_on_macos.ipynb)


## Example Python Notebook

Example colabs here:

<a target="_blank" href="https://colab.research.google.com/github/lyogavin/airllm/blob/main/air_llm/examples/run_all_types_of_models.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>

#### example of other models (ChatGLM, QWen, Baichuan, Mistral, etc):

<details>


* ChatGLM:

```python
from airllm import AutoModel
MAX_LENGTH = 128
model = AutoModel.from_pretrained("THUDM/chatglm3-6b-base")
input_text = ['What is the capital of China?',]
input_tokens = model.tokenizer(input_text,
    return_tensors="pt", 
    return_attention_mask=False, 
    truncation=True, 
    max_length=MAX_LENGTH, 
    padding=True)
generation_output = model.generate(
    input_tokens['input_ids'].cuda(), 
    max_new_tokens=5,
    use_cache= True,
    return_dict_in_generate=True)
model.tokenizer.decode(generation_output.sequences[0])
```

* QWen:

```python
from airllm import AutoModel
MAX_LENGTH = 128
model = AutoModel.from_pretrained("Qwen/Qwen-7B")
input_text = ['What is the capital of China?',]
input_tokens = model.tokenizer(input_text,
    return_tensors="pt", 
    return_attention_mask=False, 
    truncation=True, 
    max_length=MAX_LENGTH)
generation_output = model.generate(
    input_tokens['input_ids'].cuda(), 
    max_new_tokens=5,
    use_cache=True,
    return_dict_in_generate=True)
model.tokenizer.decode(generation_output.sequences[0])
```


* Baichuan, InternLM, Mistral, etc:

```python
from airllm import AutoModel
MAX_LENGTH = 128
model = AutoModel.from_pretrained("baichuan-inc/Baichuan2-7B-Base")
#model = AutoModel.from_pretrained("internlm/internlm-20b")
#model = AutoModel.from_pretrained("mistralai/Mistral-7B-Instruct-v0.1")
input_text = ['What is the capital of China?',]
input_tokens = model.tokenizer(input_text,
    return_tensors="pt", 
    return_attention_mask=False, 
    truncation=True, 
    max_length=MAX_LENGTH)
generation_output = model.generate(
    input_tokens['input_ids'].cuda(), 
    max_new_tokens=5,
    use_cache=True,
    return_dict_in_generate=True)
model.tokenizer.decode(generation_output.sequences[0])
```


</details>


#### To request other model support: [here](https://docs.google.com/forms/d/e/1FAIpQLSe0Io9ANMT964Zi-OQOq1TJmnvP-G3_ZgQDhP7SatN0IEdbOg/viewform?usp=sf_link)



## Supported Models

AirLLM works out of the box with **virtually every popular open LLM** — just pass its Hugging Face ID to `AutoModel.from_pretrained(...)`. That covers all the major families:

**Llama** (2 / 3 / 3.1 / 3.3 / 4) · **Qwen** (1 / 2 / 2.5 / 3 / 3.5 / 3.8, including MoE, FP8, and native VL) · **DeepSeek** (V2 / V3 / R1) · **Mistral & Mixtral** · **Phi** · **Gemma** · **ChatGLM** · **Baichuan** · **InternLM** · **Yi** · **Kimi K3** — and most new models the day they're released.

### Tiny GPU, huge models

The trick: AirLLM only ever keeps **one layer on the GPU at a time**, so the VRAM you need depends on the model's layer size — not its total size. That's how a 671B model fits on a hobbyist card:

| Model | Size | GPU VRAM |
|---|---|---|
| Qwen3 / Mistral / Phi (≈8B) | 8B | **~1–2 GB** |
| Qwen3-30B / Mixtral (MoE) | 30–47B | **~1–3 GB** |
| Qwen3.8-27B (dense VL) | 27B | **3.33 GB** |
| Qwen3-235B (MoE) | 235B | **~3 GB** |
| Llama 3.x 70B (full precision) | 70B | **~4 GB** |
| Llama 3.1 405B | 405B | **~8 GB** |
| DeepSeek-V3 | **671B** | **~12 GB** |

Same one line of code for all of them — no special setup.

## Acknowledgement

A lot of the code are based on SimJeg's great work in the Kaggle exam competition. Big shoutout to SimJeg:

[GitHub account @SimJeg](https://github.com/SimJeg), 
[the code on Kaggle](https://www.kaggle.com/code/simjeg/platypus2-70b-with-wikipedia-rag), 
[the associated discussion](https://www.kaggle.com/competitions/kaggle-llm-science-exam/discussion/446414).


## FAQ

### 1. MetadataIncompleteBuffer

safetensors_rust.SafetensorError: Error while deserializing header: MetadataIncompleteBuffer

If you run into this error, most possible cause is you run out of disk space. The process of splitting model is very disk-consuming. See [this](https://huggingface.co/TheBloke/guanaco-65B-GPTQ/discussions/12). You may need to extend your disk space, clear huggingface [.cache](https://huggingface.co/docs/datasets/cache) and rerun. 

### 2. ValueError: max() arg is an empty sequence

Most likely you are loading QWen or ChatGLM model with Llama2 class. Try the following:

For QWen model: 

```python
from airllm import AutoModel #<----- instead of AirLLMLlama2
AutoModel.from_pretrained(...)
```

For ChatGLM model: 

```python
from airllm import AutoModel #<----- instead of AirLLMLlama2
AutoModel.from_pretrained(...)
```

### 3. 401 Client Error....Repo model ... is gated.

Some models are gated models, needs huggingface api token. You can provide hf_token:

```python
model = AutoModel.from_pretrained("meta-llama/Llama-2-7b-hf", #hf_token='HF_API_TOKEN')
```

### 4. ValueError: Asking to pad but the tokenizer does not have a padding token.

Some model's tokenizer doesn't have padding token, so you can set a padding token or simply turn the padding config off:

 ```python
input_tokens = model.tokenizer(input_text,
    return_tensors="pt", 
    return_attention_mask=False, 
    truncation=True, 
    max_length=MAX_LENGTH, 
    padding=False  #<-----------   turn off padding 
)
```

## Citing AirLLM

If you find
AirLLM useful in your research and wish to cite it, please use the following
BibTex entry:

```
@software{airllm2023,
  author = {Gavin Li},
  title = {AirLLM: scaling large language models on low-end commodity computers},
  url = {https://github.com/lyogavin/airllm/},
  version = {0.0},
  year = {2023},
}
```


## Sponsors

<a href="https://bloome.im/app?ref=G6BYnov0&utm_medium=github&utm_source=lyogavin-airllm-ivor-202606">
  <img src="https://github.com/lyogavin/airllm/blob/main/assets/bloome.png?raw=true" alt="Bloome — Run AI Agent Teams in the Cloud" width="50%" />
</a>

### Run AI Agent Teams in the Cloud — Bloome

Bloome is an AI-agent IM platform: build and run AI agent teams in the cloud with zero setup. Add a skill as an agent in a group chat, run it in one click from web or mobile, and share it with your team — think of it as a group chat where your AI assistants are teammates you can @mention and assign tasks to.

👉 Try [Bloome](https://bloome.im/app?ref=G6BYnov0&utm_medium=github&utm_source=lyogavin-airllm-ivor-202606)


## Contribution 

Welcomed contributions, ideas and discussions!

If you find it useful, please ⭐ or buy me a coffee! 🙏

[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://bmc.link/lyogavinQ)
