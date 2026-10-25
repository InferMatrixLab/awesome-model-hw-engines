# Awesome Model × Hardware Inference Engines

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

**Languages:** [English](README.en.md) · [中文](README.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Français](README.fr.md) · [Español](README.es.md)

> **模型 × 硬件专用推理引擎精选** · specialized backends · not a general serving yellow pages  
> Curated list of **model/hardware-specialized inference engines** — engines and plugins whose value is tied to a **model family** and/or **accelerator**, not generic LLM serving stacks.

**In scope（收）：** 按**模型类别**组织、再按**硬件**细分的专用推理引擎与插件；分层 / 混合 CPU–GPU 专家调度（Strata 方法族）；模型族专用 runtime；厂商 EP / 后端插件；边缘 NPU 栈；可独立引用的 MoE / Attention 内核库。  
**Out of scope（不收）：** vLLM / SGLang / TGI / Ollama 等**通用 serving 全家桶黄页**（仅当条目明确是某加速器或模型族的专用后端 / 插件时收录该行）；训练框架；纯基准榜；营销页无开源/无文档实现。

**标记：** ⭐ 成熟 / 广泛采用 · ☄️ 上升中 / 值得盯 · **自有** = InferMatrixLab 维护（非第三方 Spec）  
**结构：** **一级 = 模型类别** → **二级 = 硬件**（NVIDIA / Ascend / Neuron-Trainium / TPU / Apple-Metal / Intel / Edge-NPU / CPU-RAM-SSD tier / CPU-NVMe / Cross-vendor kernels；未列入芯片进 Other accelerators）  
**语言：** 中文说明为主；另有 [English](README.en.md) / [日本語](README.ja.md) / [한국어](README.ko.md) / [Français](README.fr.md) / [Español](README.es.md)；项目名与链接保留英文。

### 专用引擎 ≠ 通用 Serving（先读）

| 概念 | 是什么 | 本仓？ |
|---|---|---|
| **专用引擎** | 为某芯片 ISA / 厂商 runtime / 模型族编译或深度定制的推理路径 | ✅ 本仓 |
| **通用 Serving** | 多模型多卡统一调度栈（vLLM、SGLang、TGI…） | ❌ 不收黄页；仅收其 **硬件/模型专用插件行** |
| **内核库** | FlashAttention / DeepGEMM 等可被多引擎调用的算子层 | ✅ 可进对应模型类下的 Cross-vendor kernels |
| **格式/转换工具** | 仅导出 ONNX/GGUF、无推理 runtime | ❌ 一般不收（Core ML Tools 等转换+部署链可酌情） |

---

## 贡献 / 收录规则 · Contribution

- **⭐ Established：** 文档完整；有可复现构建/运行路径；公开约 ≥ 6 个月或已成某芯片栈事实标准。
- **☄️ Rising：** 近 12 个月活跃；能说明绑定的模型族或硬件；可核验仓库/文档链接。
- **必备信息：** 模型类别、硬件、一句话问题定义、链接、⭐/☄️；自有项目须标明「自有」。
- **拒收：** 通用 serving 整仓广告；无硬件或模型专用性；仅 API 包装层。
- 欢迎 PR；分区不准先开 issue。

---

## 目录 · Table of Contents

- [Dense LLM](#dense-llm)
- [MoE](#moe)
- [Multimodal / Omni](#multimodal--omni)
- [Diffusion · Image](#diffusion--image)
- [Diffusion · Video](#diffusion--video)
- [Speech · TTS / ASR](#speech--tts--asr)
- [Embedding / Rerank](#embedding--rerank)
- [Other](#other)
- [自有索引 · InferMatrixLab（非第三方 Spec）](#自有索引--infermatrixlab非第三方-spec)
- [Contrast · 与通用 Serving 的边界](#contrast--与通用-serving-的边界)
- [Related](#related)
- [License](#license)

---

## Dense LLM

稠密 Transformer / 通用解码器 LLM（非 MoE 主体）的专用引擎与硬件后端。

### NVIDIA

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ⭐ | **NVIDIA/TensorRT-LLM** | NVIDIA 官方 LLM/VLM 推理引擎：自定义 CUDA 内核、引擎构建、IB 批处理；绑 NVIDIA GPU | https://github.com/NVIDIA/TensorRT-LLM |
| ☄️ | **turboderp-org/exllamav3** | 面向现代消费级 NVIDIA GPU 的高速量化 LLM 推理库（ExLlama 系） | https://github.com/turboderp-org/exllamav3 |
| ⭐ | **antirez/ds4** | DeepSeek-4 Flash/PRO 模型族本地推理引擎；CUDA 路径；另支持 Metal / ROCm | https://github.com/antirez/ds4 |

### NVIDIA · RTX / Blackwell (SM120)

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ☄️ | **NVIDIA/flare-local-inference** | 本地 Agent 推理：PyTorch 构建 + Rust 服务；完整对话状态（KV + 循环）；绑 NVIDIA SM120/SM121；研究原型，不替代 vLLM | https://github.com/NVIDIA/flare-local-inference |

### Ascend

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ☄️ | **vllm-project/vllm-ascend** | vLLM 的昇腾（Ascend）硬件插件；NPU 专用后端而非通用黄页 | https://github.com/vllm-project/vllm-ascend |

> MindIE / CANN 官方栈以华为文档与固件渠道为主；有稳定公开镜像后再补 ⭐ 行。

### Neuron-Trainium

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ☄️ | **aws-neuron/neuronx-distributed-inference** | NeuronX Distributed Inference（NxDI）：Inferentia/Trainium 上的分布式 LLM 推理库 | https://github.com/aws-neuron/neuronx-distributed-inference |
| ☄️ | **vllm-project/vllm-neuron** | vLLM × Neuron 插件路径；Trainium/Inferentia 专用后端 | https://github.com/vllm-project/vllm-neuron |

### TPU

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ☄️ | **vllm-project/tpu-inference** | vLLM 的 TPU 推理后端（tpu-inference）；绑 Google TPU | https://github.com/vllm-project/tpu-inference |
| ☄️ | **huggingface/optimum-tpu** | Hugging Face Optimum TPU：在 TPU 上部署 Transformer 的专用路径 | https://github.com/huggingface/optimum-tpu |

### Apple-Metal

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ⭐ | **ml-explore/mlx** | Apple 官方风格的 Apple Silicon 数组框架；Metal 上的模型运行底座 | https://github.com/ml-explore/mlx |
| ⭐ | **ml-explore/mlx-lm** | 基于 MLX 的 LLM 推理与服务工具链；绑 Apple Silicon | https://github.com/ml-explore/mlx-lm |
| ⭐ | **apple/coremltools** | Core ML 转换与部署工具链；iOS/macOS Neural Engine / GPU 路径 | https://github.com/apple/coremltools |
| ⭐ | **antirez/ds4** | 同上；Apple Silicon Metal 路径（DeepSeek-4 Flash/PRO） | https://github.com/antirez/ds4 |

### Intel

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ⭐ | **openvinotoolkit/openvino.genai** | OpenVINO GenAI：Intel CPU/GPU/NPU 上的生成式 AI 推理运行时与管线 | https://github.com/openvinotoolkit/openvino.genai |

### Edge-NPU

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ☄️ | **airockchip/rknn-llm** | Rockchip RKNN-LLM：RK3588 等板端 NPU 上的 LLM 推理栈 | https://github.com/airockchip/rknn-llm |
| ☄️ | **hailo-ai/hailort** | HailoRT：Hailo 边缘 AI 加速器上的轻量高性能推理 runtime | https://github.com/hailo-ai/hailort |

### Other accelerators

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ☄️ | **tenstorrent/vllm-tt-plugin** | Tenstorrent 的 vLLM 后端插件；配合 TT-Metalium 算子栈 | https://github.com/tenstorrent/vllm-tt-plugin |
| ☄️ | **tenstorrent/tt-metal** | TT-Metalium / TT-NN：Tenstorrent 芯片上的算子与内核编程模型 | https://github.com/tenstorrent/tt-metal |

### Cross-vendor kernels

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ⭐ | **flashinfer-ai/flashinfer** | LLM Serving 向的 Attention / 采样等内核库；多引擎可嵌入 | https://github.com/flashinfer-ai/flashinfer |

---

## MoE

混合专家模型专用引擎：专家并行、卸载、分层调度与 MoE 内核。

### NVIDIA

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepInfer** | DeepSeek 生产级推理框架开源版；绑 DeepSeek-V4.1-Flash，硬件为 NVIDIA SM100 / Ascend 950 | https://github.com/deepseek-ai/DeepInfer |


### NVIDIA · RTX

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ⭐ | **FlashML-org/FreeToken** | 桌面级超大规模 MoE 本地服务：专家卸载与快速路径；面向消费级 NVIDIA（RTX 类） | https://github.com/FlashML-org/FreeToken |

### Ascend

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepInfer** | 同上；Ascend 950 路径（与 NVIDIA SM100 双硬件） | https://github.com/deepseek-ai/DeepInfer |

### Apple-Metal

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ☄️ | **incoai/splash** | Mac Apple Silicon 本地专用推理引擎（相对 mlx-serve 的极致优化）：DFlash 投机解码 + SSD Expert Offload + Prefix Cache；面向 Qwen Flash-Next 等 | https://github.com/incoai/splash |

### CPU-RAM-SSD tier

> **Strata 类：** 「Strata」在本仓主要指 [Niko1221/Strata](https://github.com/Niko1221/Strata)——为特定大 MoE（如 Qwen3.8-Flash-Next）在消费级 PC 上做的 **VRAM / 系统 RAM / SSD 分层 + CPU 并行计算未缓存专家** 的专用引擎。同方法族还包括将该思路泛化到更多 MoE、或做专家主机/SSD 卸载与 CPU–GPU 协同的实现。若存在同名歧义项目，**以本表链接与一句话为准**。

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ⭐ | **Niko1221/Strata** | 面向 Qwen3.8-Flash-Next 等的消费级专用引擎：GPU 常驻稠密/热专家，RAM 钉住全专家并由 CPU 并行算未缓存专家，SSD 供 n-gram；CUDA/HIP 等 | https://github.com/Niko1221/Strata |
| ☄️ | **voidstackloop/extended-strata-moe** | 将 Strata 式异步 GPU/CPU 专家分层泛化到 llama.cpp 支持的多架构 MoE（方法对齐；仓库仍早期） | https://github.com/voidstackloop/extended-strata-moe |
| ☄️ | **EfficientMoE/MoE-Infinity** | MoE 专家卸载到主机内存/SSD + 激活感知缓存与预取的推理库与服务路径 | https://github.com/EfficientMoE/MoE-Infinity |
| ☄️ | **efeslab/fiddler** | ICLR'25：本地设备上 MoE 的 CPU–GPU 协同编排（缺专家时在 CPU 算激活，而非搬权重） | https://github.com/efeslab/fiddler |
| ⭐ | **kvcache-ai/ktransformers** | 混合 CPU/GPU 的 MoE / 大模型推理优化框架；强调专家卸载与内核路径 | https://github.com/kvcache-ai/ktransformers |
| ⭐ | **Tiiny-AI/PowerInfer** | 消费级 GPU+CPU 混合推理：激活 locality（热/冷神经元）拆分；含 PowerInfer-2 端侧 Mixtral；原 SJTU-IPADS | https://github.com/Tiiny-AI/PowerInfer |
| ⭐ | **JustVugg/colibri** | 纯 C、零依赖 MoE 引擎：专家从磁盘流式加载；在现有消费级硬件上跑前沿 MoE | https://github.com/JustVugg/colibri |


### CPU-NVMe

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ⭐ | **sqliteai/warp** | 可嵌入、零依赖纯 C 引擎：从 NVMe 流式加载激活权重，超内存跑 Kimi K3 / DeepSeek-V4.1-Flash / GLM-5.3-Flash 等大 MoE | https://github.com/sqliteai/warp |

### Cross-vendor kernels

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepGEMM** | DeepSeek 开源的高效 GPU BLAS/GEMM 内核库 | https://github.com/deepseek-ai/DeepGEMM |
| ⭐ | **deepseek-ai/DeepEP** | DeepSeek 开源的 Expert Parallel 通信库；MoE 专用 | https://github.com/deepseek-ai/DeepEP |

---

## Multimodal / Omni

多模态 / Omni（语音·视觉·文本一体）模型族专用引擎。

### NVIDIA

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ☄️ · 自有 | **InferMatrixLab/system1-omni** | System1 模型族的社区维护式高性能推理引擎（Rust；vLLM / vLLM-Omni 风格） | https://github.com/InferMatrixLab/system1-omni |
| ☄️ · 自有 | **InferMatrixLab/minicpm-o-4.5-single-gpu-engine** | MiniCPM-o 4.5 单卡流式语音专用引擎（可对照 vLLM-Omni / SGLang-Omni） | https://github.com/InferMatrixLab/minicpm-o-4.5-single-gpu-engine |

### Apple-Metal

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ☄️ · 自有 | **InferMatrixLab/vllm-omni-mlx** | Apple Silicon 上的全模态推理服务（OpenAI / Anthropic 兼容 API） | https://github.com/InferMatrixLab/vllm-omni-mlx |

---

## Diffusion · Image

图像扩散 / 图生成专用或强依赖编译型引擎路径。

### NVIDIA

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ⭐ | **NVIDIA/TensorRT** | 通用 NVIDIA 推理优化器与 runtime；大量 CV/扩散/自定义网络专用引擎构建入口 | https://github.com/NVIDIA/TensorRT |

---

## Diffusion · Video

视频扩散 / 视频生成专用引擎。

> 暂无核实条目；欢迎按「模型类别 → 硬件」PR。

---

## Speech · TTS / ASR

语音合成 / 识别模型族专用引擎。

### NVIDIA

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ☄️ · 自有 | **InferMatrixLab/drama-3-single-b300-engine** | Fish Audio Drama 3 在单卡 NVIDIA B300 上的流式 TTS 专用引擎 | https://github.com/InferMatrixLab/drama-3-single-b300-engine |

### Ascend

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ☄️ · 自有 | **InferMatrixLab/qwen3-tts-rsi-npu-engine** | Qwen3-TTS 在昇腾 NPU（如 910B）上的独立快速推理引擎（RSI 路径） | https://github.com/InferMatrixLab/qwen3-tts-rsi-npu-engine |

---

## Embedding / Rerank

向量 / 重排模型专用推理路径。

> 暂无核实条目；欢迎按「模型类别 → 硬件」PR。

---

## Other

尚未归入上列模型大类、但仍属模型×硬件专用的引擎与配方入口。

### NVIDIA

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ☄️ · 自有 | **InferMatrixLab/vllm-rlt** | 面向 looped transformer 的推理引擎：loop 级调度与可组合阶段执行 | https://github.com/InferMatrixLab/vllm-rlt |

### Catalogs

| 标记 | 项目 | 一句话 | 链接 |
|---|---|---|---|
| ☄️ · 自有 | **InferMatrixLab/recipe** | 按「模型 × 引擎 × 硬件」整理的社区推理配方目录（非通用 serving 黄页） | https://github.com/InferMatrixLab/recipe |

---

## 自有索引 · InferMatrixLab（非第三方 Spec）

> **边界（必读）：** 下列为本组织 **InferMatrixLab** 维护的专用引擎与配方，已按模型类别×硬件落入上表（标记「自有」）。**不是**第三方行业 Spec，也不得当作 Hardware/Model 区的厂商权威条目引用。此处仅作透明索引。

| 项目 | 落入分区 | 链接 |
|---|---|---|
| system1-omni | Multimodal / Omni → NVIDIA | https://github.com/InferMatrixLab/system1-omni |
| minicpm-o-4.5-single-gpu-engine | Multimodal / Omni → NVIDIA | https://github.com/InferMatrixLab/minicpm-o-4.5-single-gpu-engine |
| vllm-omni-mlx | Multimodal / Omni → Apple-Metal | https://github.com/InferMatrixLab/vllm-omni-mlx |
| drama-3-single-b300-engine | Speech · TTS / ASR → NVIDIA | https://github.com/InferMatrixLab/drama-3-single-b300-engine |
| qwen3-tts-rsi-npu-engine | Speech · TTS / ASR → Ascend | https://github.com/InferMatrixLab/qwen3-tts-rsi-npu-engine |
| vllm-rlt | Other → NVIDIA | https://github.com/InferMatrixLab/vllm-rlt |
| recipe | Other → Catalogs | https://github.com/InferMatrixLab/recipe |

---

## Contrast · 与通用 Serving 的边界

| 常见项目 | 本仓态度 | 说明 |
|---|---|---|
| vLLM / SGLang / TGI | 不收黄页 | 只收其 **Ascend / Neuron / TPU / TT** 等专用插件行（落在对应模型类 × 硬件下） |
| Ollama / llama.cpp | 默认不收 | 跨硬件便携 runtime；若某后端成为「芯片官方路径」可另开行讨论 |
| Triton Inference Server | 不收产品黄页 | 属编排/serving 外壳；后端引擎（TRT-LLM 等）已按模型×硬件上表 |

---

## Related

- **自有引擎索引：** 见上方 [自有索引 · InferMatrixLab](#自有索引--infermatrixlab非第三方-spec)
- InferMatrixLab 其它推理工程文档与对比（本组织内后续互链）
- 通用 serving 选型请另寻 inference serving awesome / 工程手册，避免与本仓混表

---

## License

本列表内容以 **CC0 1.0** 精神贡献（允许自由复用条目表）。被链接项目保留各自许可证。