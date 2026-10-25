# Awesome Model × Hardware Inference Engines

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

**Languages:** [English](README.en.md) · [中文](README.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Français](README.fr.md) · [Español](README.es.md)

> **Curated model × hardware specialized inference engines** · specialized backends · not a general serving yellow pages  
> A curated list of **model/hardware-specialized inference engines** — engines and plugins whose value is tied to a **model family** and/or **accelerator**, not generic LLM serving stacks.

**In scope:** Specialized inference engines and plugins organized by **model category**, then by **hardware**; stratified / hybrid CPU–GPU expert scheduling (Strata method family); model-family runtimes; vendor EP / backend plugins; edge NPU stacks; citable MoE / Attention kernel libraries.  
**Out of scope:** Generic serving megapack yellow pages such as vLLM / SGLang / TGI / Ollama (include a row only when it is clearly a **hardware- or model-family-specific backend / plugin**); training frameworks; pure benchmark boards; marketing pages with no OSS/docs implementation.

**Markers:** ⭐ Established / widely adopted · ☄️ Rising / watchlist · **First-party** = InferMatrixLab-maintained (not third-party Spec)  
**Structure:** **L1 = model category** → **L2 = hardware** (NVIDIA / Ascend / Neuron-Trainium / TPU / Apple-Metal / Intel / Edge-NPU / CPU-RAM-SSD tier / Cross-vendor kernels; unlisted chips under Other accelerators)  
**Languages:** English edition; Chinese is primary at [README.md](README.md). Project names and links stay in English.

### Specialized engine ≠ generic Serving (read first)

| Concept | What it is | This repo? |
|---|---|---|
| **Specialized engine** | Inference path compiled or deeply customized for a chip ISA / vendor runtime / model family | ✅ Here |
| **Generic Serving** | Multi-model multi-GPU unified scheduling stack (vLLM, SGLang, TGI…) | ❌ No yellow pages; only their **hardware/model-specific plugin rows** |
| **Kernel library** | Operator layer callable by many engines (FlashAttention / DeepGEMM…) | ✅ OK under the matching model class → Cross-vendor kernels |
| **Format / conversion tools** | Export-only ONNX/GGUF with no inference runtime | ❌ Usually reject (Core ML Tools conversion+deploy chain may qualify) |

---

## Contribution rules

- **⭐ Established:** Solid docs; reproducible build/run path; public ~≥ 6 months or de-facto standard for a chip stack.
- **☄️ Rising:** Active in the last 12 months; can name the bound model family or hardware; verifiable repo/docs link.
- **Required:** Model category, hardware, one-line problem definition, link, ⭐/☄️; first-party rows must be marked.
- **Reject:** Whole-repo ads for generic serving; no hardware or model specialization; API wrappers only.
- PRs welcome; open an issue first if the section is unclear.

---

## Table of Contents

- [Dense LLM](#dense-llm)
- [MoE](#moe)
- [Multimodal / Omni](#multimodal--omni)
- [Diffusion · Image](#diffusion--image)
- [Diffusion · Video](#diffusion--video)
- [Speech · TTS / ASR](#speech--tts--asr)
- [Embedding / Rerank](#embedding--rerank)
- [Other](#other)
- [First-party index · InferMatrixLab (not third-party Spec)](#first-party-index--infermatrixlab-not-third-party-spec)
- [Contrast · Boundary vs generic Serving](#contrast--boundary-vs-generic-serving)
- [Related](#related)
- [License](#license)

---

## Dense LLM

Specialized engines and hardware backends for dense Transformer / decoder LLMs (non-MoE primary).

### NVIDIA

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ⭐ | **NVIDIA/TensorRT-LLM** | NVIDIA's official LLM/VLM inference engine: custom CUDA kernels, engine build, in-flight batching; tied to NVIDIA GPUs | https://github.com/NVIDIA/TensorRT-LLM |
| ☄️ | **turboderp-org/exllamav3** | High-speed quantized LLM inference for modern consumer NVIDIA GPUs (ExLlama line) | https://github.com/turboderp-org/exllamav3 |

### NVIDIA · RTX / Blackwell (SM120)

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ☄️ | **NVIDIA/flare-local-inference** | Local Agent inference: PyTorch build + Rust serve; full dialogue state (KV + recurrent); NVIDIA SM120/SM121; research prototype, not a vLLM replacement | https://github.com/NVIDIA/flare-local-inference |

### Ascend

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ☄️ | **vllm-project/vllm-ascend** | vLLM Ascend (昇腾) hardware plugin; NPU-specific backend, not a generic yellow-pages listing | https://github.com/vllm-project/vllm-ascend |

> MindIE / CANN official stacks mainly ship via Huawei docs and firmware channels; add a ⭐ row once a stable public mirror exists.

### Neuron-Trainium

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ☄️ | **aws-neuron/neuronx-distributed-inference** | NeuronX Distributed Inference (NxDI): distributed LLM inference on Inferentia/Trainium | https://github.com/aws-neuron/neuronx-distributed-inference |
| ☄️ | **vllm-project/vllm-neuron** | vLLM × Neuron plugin path; Trainium/Inferentia-specific backend | https://github.com/vllm-project/vllm-neuron |

### TPU

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ☄️ | **vllm-project/tpu-inference** | vLLM TPU inference backend (tpu-inference); tied to Google TPU | https://github.com/vllm-project/tpu-inference |
| ☄️ | **huggingface/optimum-tpu** | Hugging Face Optimum TPU: specialized path to deploy Transformers on TPU | https://github.com/huggingface/optimum-tpu |

### Apple-Metal

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ⭐ | **ml-explore/mlx** | Apple Silicon array framework in the official style; model-running substrate on Metal | https://github.com/ml-explore/mlx |
| ⭐ | **ml-explore/mlx-lm** | LLM inference & serving toolchain on MLX; tied to Apple Silicon | https://github.com/ml-explore/mlx-lm |
| ⭐ | **apple/coremltools** | Core ML conversion & deployment toolchain; iOS/macOS Neural Engine / GPU path | https://github.com/apple/coremltools |

### Intel

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ⭐ | **openvinotoolkit/openvino.genai** | OpenVINO GenAI: generative AI inference runtime & pipelines on Intel CPU/GPU/NPU | https://github.com/openvinotoolkit/openvino.genai |

### Edge-NPU

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ☄️ | **airockchip/rknn-llm** | Rockchip RKNN-LLM: LLM inference stack on board-level NPUs (e.g. RK3588) | https://github.com/airockchip/rknn-llm |
| ☄️ | **hailo-ai/hailort** | HailoRT: lightweight high-performance inference runtime on Hailo edge AI accelerators | https://github.com/hailo-ai/hailort |

### Other accelerators

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ☄️ | **tenstorrent/vllm-tt-plugin** | Tenstorrent's vLLM backend plugin; pairs with the TT-Metalium operator stack | https://github.com/tenstorrent/vllm-tt-plugin |
| ☄️ | **tenstorrent/tt-metal** | TT-Metalium / TT-NN: operator & kernel programming model on Tenstorrent chips | https://github.com/tenstorrent/tt-metal |

### Cross-vendor kernels

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ⭐ | **flashinfer-ai/flashinfer** | Attention / sampling kernel library for LLM serving; embeddable by multiple engines | https://github.com/flashinfer-ai/flashinfer |

---

## MoE

Engines specialized for Mixture-of-Experts: expert parallelism, offload, stratified scheduling, and MoE kernels.

### NVIDIA

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepInfer** | DeepSeek production inference framework (OSS); tied to DeepSeek-V4.1-Flash on NVIDIA SM100 / Ascend 950 | https://github.com/deepseek-ai/DeepInfer |

### Ascend

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepInfer** | Same as above; Ascend 950 path (dual-hardware with NVIDIA SM100) | https://github.com/deepseek-ai/DeepInfer |

### Apple-Metal

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ☄️ | **incoai/splash** | Local Apple Silicon engine (extreme vs mlx-serve): DFlash speculative decoding + SSD expert offload + prefix cache; Qwen Flash-Next-class MoEs | https://github.com/incoai/splash |

### CPU-RAM-SSD tier

> **Strata-class:** In this list, “Strata” primarily means [Niko1221/Strata](https://github.com/Niko1221/Strata) — a **model-specialized** consumer-PC engine for large MoEs (e.g. Qwen3.8-Flash-Next) with **VRAM / system RAM / SSD tiers** and **CPU computing uncached experts in parallel**. The same method family includes generalizations to more MoEs and expert host/SSD offload or CPU–GPU orchestration. If other same-named repos appear, **trust the links and one-liners below**.

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ⭐ | **Niko1221/Strata** | Consumer specialized engine for Qwen3.8-Flash-Next-class MoEs: dense/hot experts on GPU, all experts pinned in RAM with CPU parallel compute for misses, SSD n-gram; CUDA/HIP | https://github.com/Niko1221/Strata |
| ☄️ | **voidstackloop/extended-strata-moe** | Generalizes Strata-style async GPU/CPU expert tiering across many llama.cpp MoE architectures (method-aligned; early repo) | https://github.com/voidstackloop/extended-strata-moe |
| ☄️ | **EfficientMoE/MoE-Infinity** | MoE expert offload to host memory/SSD with activation-aware cache and prefetch; library + serving path | https://github.com/EfficientMoE/MoE-Infinity |
| ☄️ | **efeslab/fiddler** | ICLR'25: CPU–GPU orchestration for local MoE (compute missing experts on CPU instead of shipping weights) | https://github.com/efeslab/fiddler |
| ⭐ | **kvcache-ai/ktransformers** | Hybrid CPU/GPU MoE / large-model inference framework; expert offload & kernel paths | https://github.com/kvcache-ai/ktransformers |
| ⭐ | **Tiiny-AI/PowerInfer** | Consumer GPU+CPU hybrid LLM engine via activation locality (hot/cold neurons); PowerInfer-2 for on-device Mixtral; formerly SJTU-IPADS | https://github.com/Tiiny-AI/PowerInfer |

### Cross-vendor kernels

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepGEMM** | DeepSeek OSS high-efficiency GPU BLAS/GEMM kernel library | https://github.com/deepseek-ai/DeepGEMM |
| ⭐ | **deepseek-ai/DeepEP** | DeepSeek OSS Expert Parallel communication library; MoE-specific | https://github.com/deepseek-ai/DeepEP |

---

## Multimodal / Omni

Engines specialized for multimodal / Omni (speech · vision · text) model families.

### NVIDIA

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ☄️ · First-party | **InferMatrixLab/system1-omni** | Community-maintained high-performance inference engine for System1 model family (Rust; vLLM / vLLM-Omni style) | https://github.com/InferMatrixLab/system1-omni |
| ☄️ · First-party | **InferMatrixLab/minicpm-o-4.5-single-gpu-engine** | Single-GPU streaming speech engine specialized for MiniCPM-o 4.5 (comparable to vLLM-Omni / SGLang-Omni) | https://github.com/InferMatrixLab/minicpm-o-4.5-single-gpu-engine |

### Apple-Metal

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ☄️ · First-party | **InferMatrixLab/vllm-omni-mlx** | Omni-modality inference server on Apple Silicon (OpenAI / Anthropic-compatible API) | https://github.com/InferMatrixLab/vllm-omni-mlx |

---

## Diffusion · Image

Image diffusion / image-generation specialized or compile-heavy engine paths.

### NVIDIA

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ⭐ | **NVIDIA/TensorRT** | General NVIDIA inference optimizer & runtime; entry point for many CV/diffusion/custom-network specialized engines | https://github.com/NVIDIA/TensorRT |

---

## Diffusion · Video

Video diffusion / video-generation specialized engines.

> No verified rows yet; PRs welcome under model category → hardware.

---

## Speech · TTS / ASR

Speech synthesis / recognition model-family specialized engines.

### NVIDIA

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ☄️ · First-party | **InferMatrixLab/drama-3-single-b300-engine** | Streaming TTS engine specialized for Fish Audio Drama 3 on a single NVIDIA B300 | https://github.com/InferMatrixLab/drama-3-single-b300-engine |

### Ascend

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ☄️ · First-party | **InferMatrixLab/qwen3-tts-rsi-npu-engine** | Standalone fast Qwen3-TTS inference on Ascend NPU (e.g. 910B) via RSI path | https://github.com/InferMatrixLab/qwen3-tts-rsi-npu-engine |

---

## Embedding / Rerank

Embedding / rerank model specialized inference paths.

> No verified rows yet; PRs welcome under model category → hardware.

---

## Other

Engines and recipe catalogs that are still model×hardware specialized but do not fit the classes above.

### NVIDIA

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ☄️ · First-party | **InferMatrixLab/vllm-rlt** | Inference engine for looped transformers: loop-level scheduling across composable stages | https://github.com/InferMatrixLab/vllm-rlt |

### Catalogs

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ☄️ · First-party | **InferMatrixLab/recipe** | Community catalog of “model × engine × hardware” inference recipes (not a generic serving yellow pages) | https://github.com/InferMatrixLab/recipe |

---

## First-party index · InferMatrixLab (not third-party Spec)

> **Boundary (required):** Rows below are **InferMatrixLab**-maintained specialized engines and recipes, already placed in the tables above (marked First-party). They are **not** third-party industry Spec and must **not** be cited as vendor-authority rows. This section is a transparency index only.

| Project | Lands in | Link |
|---|---|---|
| system1-omni | Multimodal / Omni → NVIDIA | https://github.com/InferMatrixLab/system1-omni |
| minicpm-o-4.5-single-gpu-engine | Multimodal / Omni → NVIDIA | https://github.com/InferMatrixLab/minicpm-o-4.5-single-gpu-engine |
| vllm-omni-mlx | Multimodal / Omni → Apple-Metal | https://github.com/InferMatrixLab/vllm-omni-mlx |
| drama-3-single-b300-engine | Speech · TTS / ASR → NVIDIA | https://github.com/InferMatrixLab/drama-3-single-b300-engine |
| qwen3-tts-rsi-npu-engine | Speech · TTS / ASR → Ascend | https://github.com/InferMatrixLab/qwen3-tts-rsi-npu-engine |
| vllm-rlt | Other → NVIDIA | https://github.com/InferMatrixLab/vllm-rlt |
| recipe | Other → Catalogs | https://github.com/InferMatrixLab/recipe |

---

## Contrast · Boundary vs generic Serving

| Common project | Stance here | Note |
|---|---|---|
| vLLM / SGLang / TGI | No yellow pages | Only their **Ascend / Neuron / TPU / TT** specialized plugin rows (under matching model class × hardware) |
| Ollama / llama.cpp | Default reject | Cross-hardware portable runtime; discuss a separate row if a backend becomes a “chip-official path” |
| Triton Inference Server | No product yellow pages | Orchestration/serving shell; backend engines (TRT-LLM etc.) already listed by model × hardware |

---

## Related

- **First-party index:** see [First-party index · InferMatrixLab](#first-party-index--infermatrixlab-not-third-party-spec)
- Other InferMatrixLab inference engineering docs and comparisons (cross-links within the org later)
- For generic serving selection, use a separate inference-serving awesome / engineering handbook—do not mix tables with this repo

---

## License

List content is contributed in the spirit of **CC0 1.0** (free reuse of the entry tables). Linked projects keep their own licenses.