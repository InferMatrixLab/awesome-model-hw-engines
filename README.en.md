# Awesome Model × Hardware Inference Engines

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

**Languages:** [English](README.en.md) · [中文](README.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Français](README.fr.md) · [Español](README.es.md)

> **Curated model × hardware specialized inference engines** · specialized backends · not a general serving yellow pages  
> A curated list of **model/hardware-specialized inference engines** — engines and plugins whose value is tied to a **model family** and/or **accelerator**, not generic LLM serving stacks.

**In scope:** Compile-time or kernel-level inference engines for specific chips / runtimes; model-family-specialized runtimes (e.g. DeepSeek-class); vendor EP / backend plugins (Ascend, Neuron, TPU, Tenstorrent…); edge NPU LLM stacks; MoE / attention specialized kernel libraries (when citable as an “engine layer”).  
**Out of scope:** Generic serving megapack yellow pages such as vLLM / SGLang / TGI / Ollama (include a row only when it is clearly a **hardware- or model-family-specific backend / plugin**); training frameworks; pure benchmark boards; marketing pages with no OSS/docs implementation.

**Markers:** ⭐ Established / widely adopted · ☄️ Rising / watchlist  
**Structure:** Method Family × Hardware Domain  
**Languages:** English edition; Chinese is primary at [README.md](README.md). Project names and links stay in English.

### Specialized engine ≠ generic Serving (read first)

| Concept | What it is | This repo? |
|---|---|---|
| **Specialized engine** | Inference path compiled or deeply customized for a chip ISA / vendor runtime / model family | ✅ Here |
| **Generic Serving** | Multi-model multi-GPU unified scheduling stack (vLLM, SGLang, TGI…) | ❌ No yellow pages; only their **hardware/model-specific plugin rows** |
| **Kernel library** | Operator layer callable by many engines (FlashAttention / DeepGEMM…) | ✅ OK in “Kernels / MoE” |
| **Format / conversion tools** | Export-only ONNX/GGUF with no inference runtime | ❌ Usually reject (Core ML Tools conversion+deploy chain may qualify) |

---

## Contribution rules

- **⭐ Established:** Solid docs; reproducible build/run path; public ~≥ 6 months or de-facto standard for a chip stack.
- **☄️ Rising:** Active in the last 12 months; can name the bound model family or hardware; verifiable repo/docs link.
- **Required:** Which model/hardware, one-line problem definition, link, section, ⭐/☄️.
- **Reject:** Whole-repo ads for generic serving; no hardware or model specialization; API wrappers only.
- PRs welcome; open an issue first if the section is unclear.

---

## Table of Contents

- [Hardware · NVIDIA (TensorRT family)](#hardware--nvidia-tensorrt-family)
- [Hardware · Ascend / domestic NPU](#hardware--ascend--domestic-npu)
- [Hardware · AWS Inferentia / Trainium](#hardware--aws-inferentia--trainium)
- [Hardware · TPU](#hardware--tpu)
- [Hardware · Apple / Metal](#hardware--apple--metal)
- [Hardware · Intel OpenVINO / CPU·iGPU·NPU](#hardware--intel-openvino--cpuiGPUnpu)
- [Hardware · Edge NPU / mobile](#hardware--edge-npu--mobile)
- [Hardware · Other accelerator plugins](#hardware--other-accelerator-plugins)
- [Model · Model-family specialized Runtime](#model--model-family-specialized-runtime)
- [Kernels · MoE / Attention specialized ops](#kernels--moe--attention-specialized-ops)
- [Contrast · Boundary vs generic Serving](#contrast--boundary-vs-generic-serving)
- [Related](#related)
- [License](#license)

---

## Hardware · NVIDIA (TensorRT family)

**Compile-time / vendor-grade** LLM and graph-optimization engines for NVIDIA GPUs (not “yet another OpenAI-compatible server”).

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ⭐ | **NVIDIA/TensorRT-LLM** | NVIDIA's official LLM/VLM inference engine: custom CUDA kernels, engine build, in-flight batching; tied to NVIDIA GPUs | https://github.com/NVIDIA/TensorRT-LLM |
| ⭐ | **NVIDIA/TensorRT** | General NVIDIA inference optimizer & runtime; entry point for many CV/diffusion/custom-network specialized engines | https://github.com/NVIDIA/TensorRT |

---

## Hardware · Ascend / domestic NPU

Specialized backends and plugins on Ascend and similar NPUs (generic vLLM core is not listed—only Ascend paths).

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ☄️ | **vllm-project/vllm-ascend** | vLLM Ascend (昇腾) hardware plugin; NPU-specific backend, not a generic yellow-pages listing | https://github.com/vllm-project/vllm-ascend |

> MindIE / CANN official stacks mainly ship via Huawei docs and firmware channels; add a ⭐ row once a stable public mirror exists.

---

## Hardware · AWS Inferentia / Trainium

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ☄️ | **aws-neuron/neuronx-distributed-inference** | NeuronX Distributed Inference (NxDI): distributed LLM inference on Inferentia/Trainium | https://github.com/aws-neuron/neuronx-distributed-inference |
| ☄️ | **vllm-project/vllm-neuron** | vLLM × Neuron plugin path; Trainium/Inferentia-specific backend | https://github.com/vllm-project/vllm-neuron |

---

## Hardware · TPU

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ☄️ | **vllm-project/tpu-inference** | vLLM TPU inference backend (tpu-inference); tied to Google TPU | https://github.com/vllm-project/tpu-inference |
| ☄️ | **huggingface/optimum-tpu** | Hugging Face Optimum TPU: specialized path to deploy Transformers on TPU | https://github.com/huggingface/optimum-tpu |

---

## Hardware · Apple / Metal

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ⭐ | **ml-explore/mlx** | Apple Silicon array framework in the official style; model-running substrate on Metal | https://github.com/ml-explore/mlx |
| ⭐ | **ml-explore/mlx-lm** | LLM inference & serving toolchain on MLX; tied to Apple Silicon | https://github.com/ml-explore/mlx-lm |
| ⭐ | **apple/coremltools** | Core ML conversion & deployment toolchain; iOS/macOS Neural Engine / GPU path | https://github.com/apple/coremltools |

---

## Hardware · Intel OpenVINO / CPU·iGPU·NPU

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ⭐ | **openvinotoolkit/openvino.genai** | OpenVINO GenAI: generative AI inference runtime & pipelines on Intel CPU/GPU/NPU | https://github.com/openvinotoolkit/openvino.genai |

---

## Hardware · Edge NPU / mobile

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ☄️ | **airockchip/rknn-llm** | Rockchip RKNN-LLM: LLM inference stack on board-level NPUs (e.g. RK3588) | https://github.com/airockchip/rknn-llm |
| ☄️ | **hailo-ai/hailort** | HailoRT: lightweight high-performance inference runtime on Hailo edge AI accelerators | https://github.com/hailo-ai/hailort |

---

## Hardware · Other accelerator plugins

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ☄️ | **tenstorrent/vllm-tt-plugin** | Tenstorrent's vLLM backend plugin; pairs with the TT-Metalium operator stack | https://github.com/tenstorrent/vllm-tt-plugin |
| ☄️ | **tenstorrent/tt-metal** | TT-Metalium / TT-NN: operator & kernel programming model on Tenstorrent chips | https://github.com/tenstorrent/tt-metal |

---

## Model · Model-family specialized Runtime

Engines deeply customized for specific model structures (DeepSeek MoE, high-compression quantized layouts, hybrid expert offload, etc.).

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepInfer** | DeepSeek production inference framework (OSS); tied to DeepSeek-V4.1-Flash on NVIDIA SM100 / Ascend 950 | https://github.com/deepseek-ai/DeepInfer |
| ☄️ | **turboderp-org/exllamav3** | High-speed quantized LLM inference for modern consumer NVIDIA GPUs (ExLlama line) | https://github.com/turboderp-org/exllamav3 |
| ⭐ | **kvcache-ai/ktransformers** | Hybrid CPU/GPU MoE / large-model inference framework; expert offload & kernel paths | https://github.com/kvcache-ai/ktransformers |

---

## Kernels · MoE / Attention specialized ops

**Specialized kernel libraries** composable by upper engines (not full serving products, but the core “model×hardware” performance layer).

| Mark | Project | One-liner | Link |
|---|---|---|---|
| ⭐ | **flashinfer-ai/flashinfer** | Attention / sampling kernel library for LLM serving; embeddable by multiple engines | https://github.com/flashinfer-ai/flashinfer |
| ⭐ | **deepseek-ai/DeepGEMM** | DeepSeek OSS high-efficiency GPU BLAS/GEMM kernel library | https://github.com/deepseek-ai/DeepGEMM |
| ⭐ | **deepseek-ai/DeepEP** | DeepSeek OSS Expert Parallel communication library; MoE-specific | https://github.com/deepseek-ai/DeepEP |

---

## Contrast · Boundary vs generic Serving

| Common project | Stance here | Note |
|---|---|---|
| vLLM / SGLang / TGI | No yellow pages | Only their **Ascend / Neuron / TPU / TT** specialized plugin rows |
| Ollama / llama.cpp | Default reject | Cross-hardware portable runtime; discuss a separate row if a backend becomes a “chip-official path” |
| Triton Inference Server | No product yellow pages | Orchestration/serving shell; backend engines (TRT-LLM etc.) already listed above |

---

## Related

- Other InferMatrixLab inference engineering docs and comparisons (cross-links within the org later)
- For generic serving selection, use a separate inference-serving awesome / engineering handbook—do not mix tables with this repo

---

## License

List content is contributed in the spirit of **CC0 1.0** (free reuse of the entry tables). Linked projects keep their own licenses.
