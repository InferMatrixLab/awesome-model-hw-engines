# Awesome Model × Hardware Inference Engines

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

**Languages:** [English](README.en.md) · [中文](README.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Français](README.fr.md) · [Español](README.es.md)

> **模型 × 硬件专用推理引擎精选** · specialized backends · not a general serving yellow pages  
> Curated list of **model/hardware-specialized inference engines** — engines and plugins whose value is tied to a **model family** and/or **accelerator**, not generic LLM serving stacks.

**In scope（收）：** 分层 / 混合 CPU–GPU 专家调度类专用引擎（Strata 方法族）；面向特定芯片 / 运行时的编译型或内核级推理引擎；模型族专用 runtime（如 DeepSeek-class）；厂商 EP / 后端插件（Ascend、Neuron、TPU、Tenstorrent…）；边缘 NPU LLM 栈；MoE / attention 专用内核库（在「引擎层」可独立引用时）。  
**Out of scope（不收）：** vLLM / SGLang / TGI / Ollama 等**通用 serving 全家桶黄页**（仅当条目明确是「某加速器或模型族的专用后端 / 插件」时收录该行）；训练框架；纯基准榜；营销页无开源/无文档实现。

**标记：** ⭐ 成熟 / 广泛采用 · ☄️ 上升中 / 值得盯  
**结构：** Method Family × Hardware Domain  
**语言：** 中文说明为主；另有 [English](README.en.md) / [日本語](README.ja.md) / [한국어](README.ko.md) / [Français](README.fr.md) / [Español](README.es.md)；项目名与链接保留英文。

### 专用引擎 ≠ 通用 Serving（先读）

| 概念 | 是什么 | 本仓？ |
|---|---|---|
| **专用引擎** | 为某芯片 ISA / 厂商 runtime / 模型族编译或深度定制的推理路径 | ✅ 本仓 |
| **通用 Serving** | 多模型多卡统一调度栈（vLLM、SGLang、TGI…） | ❌ 不收黄页；仅收其 **硬件/模型专用插件行** |
| **内核库** | FlashAttention / DeepGEMM 等可被多引擎调用的算子层 | ✅ 可进「Kernels / MoE」区 |
| **格式/转换工具** | 仅导出 ONNX/GGUF、无推理 runtime | ❌ 一般不收（Core ML Tools 等转换+部署链可酌情） |

---

## 贡献 / 收录规则 · Contribution

- **⭐ Established：** 文档完整；有可复现构建/运行路径；公开约 ≥ 6 个月或已成某芯片栈事实标准。
- **☄️ Rising：** 近 12 个月活跃；能说明绑定的模型族或硬件；可核验仓库/文档链接。
- **必备信息：** 针对什么模型/硬件、一句话问题定义、链接、分区、⭐/☄️。
- **拒收：** 通用 serving 整仓广告；无硬件或模型专用性；仅 API 包装层。
- 欢迎 PR；分区不准先开 issue。

---

## 目录 · Table of Contents

- [Hardware · NVIDIA（TensorRT 系）](#hardware--nvidiatensorrt-系)
- [Hardware · Ascend / 国产 NPU](#hardware--ascend--国产-npu)
- [Hardware · AWS Inferentia / Trainium](#hardware--aws-inferentia--trainium)
- [Hardware · TPU](#hardware--tpu)
- [Hardware · Apple / Metal](#hardware--apple--metal)
- [Hardware · Intel OpenVINO / CPU·iGPU·NPU](#hardware--intel-openvino--cpuiGPUNpu)
- [Hardware · 边缘 NPU / 移动](#hardware--边缘-npu--移动)
- [Hardware · 其他加速器插件](#hardware--其他加速器插件)
- [Model · 模型族专用 Runtime](#model--模型族专用-runtime)
- [Method · 分层 / 专用调度引擎（Strata 类）](#method--分层--专用调度引擎strata-类)
- [自有 · InferMatrixLab（非第三方 Spec）](#自有--infermatrixlab非第三方-spec)
- [Kernels · MoE / Attention 专用算子](#kernels--moe--attention-专用算子)
- [Contrast · 与通用 Serving 的边界](#contrast--与通用-serving-的边界)
- [Related](#related)
- [License](#license)

---

## Hardware · NVIDIA（TensorRT 系）

面向 NVIDIA GPU 的**编译型 / 厂商级** LLM 与图优化引擎（不是「又一个 OpenAI 兼容 server」）。

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ⭐ | **NVIDIA/TensorRT-LLM** | NVIDIA 官方 LLM/VLM 推理引擎：自定义 CUDA 内核、引擎构建、IB 批处理；绑 NVIDIA GPU | https://github.com/NVIDIA/TensorRT-LLM |
| ⭐ | **NVIDIA/TensorRT** | 通用 NVIDIA 推理优化器与 runtime；大量 CV/扩散/自定义网络专用引擎构建入口 | https://github.com/NVIDIA/TensorRT |

---

## Hardware · Ascend / 国产 NPU

昇腾等 NPU 上的专用后端与插件（通用 vLLM 本体不收录，只收 Ascend 路径）。

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ☄️ | **vllm-project/vllm-ascend** | vLLM 的昇腾（Ascend）硬件插件；NPU 专用后端而非通用黄页 | https://github.com/vllm-project/vllm-ascend |

> MindIE / CANN 官方栈以华为文档与固件渠道为主；有稳定公开镜像后再补 ⭐ 行。

---

## Hardware · AWS Inferentia / Trainium

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ☄️ | **aws-neuron/neuronx-distributed-inference** | NeuronX Distributed Inference（NxDI）：Inferentia/Trainium 上的分布式 LLM 推理库 | https://github.com/aws-neuron/neuronx-distributed-inference |
| ☄️ | **vllm-project/vllm-neuron** | vLLM × Neuron 插件路径；Trainium/Inferentia 专用后端 | https://github.com/vllm-project/vllm-neuron |

---

## Hardware · TPU

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ☄️ | **vllm-project/tpu-inference** | vLLM 的 TPU 推理后端（tpu-inference）；绑 Google TPU | https://github.com/vllm-project/tpu-inference |
| ☄️ | **huggingface/optimum-tpu** | Hugging Face Optimum TPU：在 TPU 上部署 Transformer 的专用路径 | https://github.com/huggingface/optimum-tpu |

---

## Hardware · Apple / Metal

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ⭐ | **ml-explore/mlx** | Apple 官方风格的 Apple Silicon 数组框架；Metal 上的模型运行底座 | https://github.com/ml-explore/mlx |
| ⭐ | **ml-explore/mlx-lm** | 基于 MLX 的 LLM 推理与服务工具链；绑 Apple Silicon | https://github.com/ml-explore/mlx-lm |
| ⭐ | **apple/coremltools** | Core ML 转换与部署工具链；iOS/macOS Neural Engine / GPU 路径 | https://github.com/apple/coremltools |

---

## Hardware · Intel OpenVINO / CPU·iGPU·NPU

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ⭐ | **openvinotoolkit/openvino.genai** | OpenVINO GenAI：Intel CPU/GPU/NPU 上的生成式 AI 推理运行时与管线 | https://github.com/openvinotoolkit/openvino.genai |

---

## Hardware · 边缘 NPU / 移动

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ☄️ | **airockchip/rknn-llm** | Rockchip RKNN-LLM：RK3588 等板端 NPU 上的 LLM 推理栈 | https://github.com/airockchip/rknn-llm |
| ☄️ | **hailo-ai/hailort** | HailoRT：Hailo 边缘 AI 加速器上的轻量高性能推理 runtime | https://github.com/hailo-ai/hailort |

---

## Hardware · 其他加速器插件

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ☄️ | **tenstorrent/vllm-tt-plugin** | Tenstorrent 的 vLLM 后端插件；配合 TT-Metalium 算子栈 | https://github.com/tenstorrent/vllm-tt-plugin |
| ☄️ | **tenstorrent/tt-metal** | TT-Metalium / TT-NN：Tenstorrent 芯片上的算子与内核编程模型 | https://github.com/tenstorrent/tt-metal |

---

## Model · 模型族专用 Runtime

为特定模型结构（DeepSeek MoE、高压缩量化布局、混合专家卸载等）深度定制的引擎。

> 另见下方 [Method · 分层 / 专用调度引擎（Strata 类）](#method--分层--专用调度引擎strata-类)。

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepInfer** | DeepSeek 生产级推理框架开源版；绑 DeepSeek-V4.1-Flash，硬件为 NVIDIA SM100 / Ascend 950 | https://github.com/deepseek-ai/DeepInfer |
| ☄️ | **turboderp-org/exllamav3** | 面向现代消费级 NVIDIA GPU 的高速量化 LLM 推理库（ExLlama 系） | https://github.com/turboderp-org/exllamav3 |
| ⭐ | **kvcache-ai/ktransformers** | 混合 CPU/GPU 的 MoE / 大模型推理优化框架；强调专家卸载与内核路径 | https://github.com/kvcache-ai/ktransformers |

---

## Method · 分层 / 专用调度引擎（Strata 类）

> **命名说明：** 「Strata」在本仓主要指 [Niko1221/Strata](https://github.com/Niko1221/Strata)——为特定大 MoE（如 Qwen3.8-Flash-Next）在消费级 PC 上做的 **VRAM / 系统 RAM / SSD 分层 + CPU 并行计算未缓存专家** 的专用引擎。同方法族还包括将该思路泛化到更多 MoE、或做专家主机/SSD 卸载与 CPU–GPU 协同的实现。若 GitHub 上存在同名歧义项目，**以本表链接与一句话为准**。

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ⭐ | **Niko1221/Strata** | 面向 Qwen3.8-Flash-Next 等的消费级专用引擎：GPU 常驻稠密/热专家，RAM 钉住全专家并由 CPU 并行算未缓存专家，SSD 供 n-gram；CUDA/HIP 等 | https://github.com/Niko1221/Strata |
| ☄️ | **voidstackloop/extended-strata-moe** | 将 Strata 式异步 GPU/CPU 专家分层泛化到 llama.cpp 支持的多架构 MoE（方法对齐；仓库仍早期） | https://github.com/voidstackloop/extended-strata-moe |
| ☄️ | **EfficientMoE/MoE-Infinity** | MoE 专家卸载到主机内存/SSD + 激活感知缓存与预取的推理库与服务路径 | https://github.com/EfficientMoE/MoE-Infinity |
| ☄️ | **efeslab/fiddler** | ICLR'25：本地设备上 MoE 的 CPU–GPU 协同编排（缺专家时在 CPU 算激活，而非搬权重） | https://github.com/efeslab/fiddler |

---

## 自有 · InferMatrixLab（非第三方 Spec）

> **边界（必读）：** 以下为本组织 **InferMatrixLab** 维护的模型/硬件**专用**推理引擎与配方入口，仅供组织内互链与对外透明列出。**不是**第三方行业 Spec，也不得当作「官方标准」或 Hardware/Model 区的厂商权威条目引用。与上方第三方精选**分列**。

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ☄️ | **InferMatrixLab/system1-omni** | System1 模型族的社区维护式高性能推理引擎（Rust；vLLM / vLLM-Omni 风格） | https://github.com/InferMatrixLab/system1-omni |
| ☄️ | **InferMatrixLab/vllm-rlt** | 面向 looped transformer 的推理引擎：loop 级调度与可组合阶段执行 | https://github.com/InferMatrixLab/vllm-rlt |
| ☄️ | **InferMatrixLab/minicpm-o-4.5-single-gpu-engine** | MiniCPM-o 4.5 单卡流式语音专用引擎（可对照 vLLM-Omni / SGLang-Omni） | https://github.com/InferMatrixLab/minicpm-o-4.5-single-gpu-engine |
| ☄️ | **InferMatrixLab/vllm-omni-mlx** | Apple Silicon 上的全模态推理服务（OpenAI / Anthropic 兼容 API） | https://github.com/InferMatrixLab/vllm-omni-mlx |
| ☄️ | **InferMatrixLab/qwen3-tts-rsi-npu-engine** | Qwen3-TTS 在昇腾 NPU（如 910B）上的独立快速推理引擎（RSI 路径） | https://github.com/InferMatrixLab/qwen3-tts-rsi-npu-engine |
| ☄️ | **InferMatrixLab/drama-3-single-b300-engine** | Fish Audio Drama 3 在单卡 NVIDIA B300 上的流式 TTS 专用引擎 | https://github.com/InferMatrixLab/drama-3-single-b300-engine |
| ☄️ | **InferMatrixLab/recipe** | 按「模型 × 引擎 × 硬件」整理的社区推理配方目录（非通用 serving 黄页） | https://github.com/InferMatrixLab/recipe |

---

## Kernels · MoE / Attention 专用算子

可被上层引擎组合的**专用内核库**（本身不是完整 serving 产品，但是「模型×硬件」性能的核心层）。

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ⭐ | **flashinfer-ai/flashinfer** | LLM Serving 向的 Attention / 采样等内核库；多引擎可嵌入 | https://github.com/flashinfer-ai/flashinfer |
| ⭐ | **deepseek-ai/DeepGEMM** | DeepSeek 开源的高效 GPU BLAS/GEMM 内核库 | https://github.com/deepseek-ai/DeepGEMM |
| ⭐ | **deepseek-ai/DeepEP** | DeepSeek 开源的 Expert Parallel 通信库；MoE 专用 | https://github.com/deepseek-ai/DeepEP |

---

## Contrast · 与通用 Serving 的边界

| 常见项目 | 本仓态度 | 说明 |
|---|---|---|
| vLLM / SGLang / TGI | 不收黄页 | 只收其 **Ascend / Neuron / TPU / TT** 等专用插件行 |
| Ollama / llama.cpp | 默认不收 | 跨硬件便携 runtime；若某后端成为「芯片官方路径」可另开行讨论 |
| Triton Inference Server | 不收产品黄页 | 属编排/serving 外壳；后端引擎（TRT-LLM 等）已在上表 |

---

## Related

- **自有引擎：** 见上方 [自有 · InferMatrixLab](#自有--infermatrixlab非第三方-spec)（组织项目，非 Spec）
- InferMatrixLab 其它推理工程文档与对比（本组织内后续互链）
- 通用 serving 选型请另寻 inference serving awesome / 工程手册，避免与本仓混表

---

## License

本列表内容以 **CC0 1.0** 精神贡献（允许自由复用条目表）。被链接项目保留各自许可证。
