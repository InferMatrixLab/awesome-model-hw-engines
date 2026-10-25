# Awesome Model × Hardware Inference Engines

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

**Languages:** [English](README.en.md) · [中文](README.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Français](README.fr.md) · [Español](README.es.md)

> **Motores de inferencia especializados modelo × hardware** · specialized backends · no un directorio de serving genérico  
> Lista curada de **engines y plugins** cuyo valor está ligado a una **familia de modelos** y/o un **acelerador**.

**En alcance:** engines/plugins organizados por **categoría de modelo** y luego por **hardware**; planificación de expertos estratificada / híbrida CPU–GPU (familia Strata); runtimes de familia de modelos; plugins EP / backends de fabricante; stacks NPU edge; bibliotecas de kernels MoE / Attention citables.  
**Fuera de alcance:** directorios serving genéricos vLLM / SGLang / TGI / Ollama (incluir una fila solo si es claramente un **backend / plugin** de acelerador o familia de modelos); frameworks de entrenamiento; puros benchmarks; páginas de marketing sin OSS/docs.

**Marcadores:** ⭐ Establecido / ampliamente adoptado · ☄️ En auge / a vigilar · **First-party** = mantenido por InferMatrixLab (no Spec de terceros)  
**Estructura:** **L1 = categoría de modelo** → **L2 = hardware** (NVIDIA / Ascend / Neuron-Trainium / TPU / Apple-Metal / Intel / Edge-NPU / CPU-RAM-SSD tier / Cross-vendor kernels; chips no listados bajo Other accelerators)  
**Idiomas:** edición en español; primaria en chino [README.md](README.md). Nombres de proyectos y enlaces en inglés.

### Engine especializado ≠ Serving genérico (leer primero)

| Concepto | Qué es | ¿Este repo? |
|---|---|---|
| **Engine especializado** | Ruta de inferencia compilada o profundamente customizada para ISA / runtime de fabricante / familia de modelos | ✅ Aquí |
| **Serving genérico** | Stack multi-modelo multi-GPU (vLLM, SGLang, TGI…) | ❌ Sin directorio; solo **filas de plugin hard/modelo** |
| **Biblioteca de kernels** | Capa de operadores usable por varios engines | ✅ OK bajo la clase de modelo → Cross-vendor kernels |
| **Herramientas de formato / conversión** | Solo export ONNX/GGUF sin runtime de inferencia | ❌ Suele rechazarse (Core ML Tools conversión+despliegue puede calificar) |

---

## Reglas de contribución

- **⭐ Established:** docs sólidos; build/run reproducible; público ~≥ 6 meses o estándar de facto de un stack de chip.
- **☄️ Rising:** activo en 12 meses; puede nombrar familia de modelos o hardware; enlace verificable.
- **Requerido:** categoría de modelo, hardware, definición en una línea, enlace, ⭐/☄️; marcar filas first-party.
- **Rechazar:** anuncios de serving genérico; sin especialización; solo wrappers API.
- PRs bienvenidos; abrir issue si la sección no está clara.

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
- [Índice first-party · InferMatrixLab (no Spec de terceros)](#índice-first-party--infermatrixlab-no-spec-de-terceros)
- [Contrast · Límite vs Serving genérico](#contrast--límite-vs-serving-genérico)
- [Related](#related)
- [License](#license)

---

## Dense LLM

Engines y backends de hardware para LLM Transformer / decodificador densos (no MoE principal).

### NVIDIA

| Marca | Proyecto | En una línea | Enlace |
|---|---|---|---|
| ⭐ | **NVIDIA/TensorRT-LLM** | Engine LLM/VLM oficial de NVIDIA: kernels CUDA custom, build de engine, batching in-flight; GPU NVIDIA | https://github.com/NVIDIA/TensorRT-LLM |
| ☄️ | **turboderp-org/exllamav3** | Inferencia LLM cuantizada de alta velocidad para GPU NVIDIA de consumo (línea ExLlama) | https://github.com/turboderp-org/exllamav3 |

### NVIDIA · RTX / Blackwell (SM120)

| Marca | Proyecto | En una línea | Enlace |
|---|---|---|---|
| ☄️ | **NVIDIA/flare-local-inference** | Inferencia Agent local: build PyTorch + serve Rust; estado de diálogo completo (KV + recurrente); NVIDIA SM120/SM121; prototipo de investigación, no reemplaza vLLM | https://github.com/NVIDIA/flare-local-inference |

### Ascend

| Marca | Proyecto | En una línea | Enlace |
|---|---|---|---|
| ☄️ | **vllm-project/vllm-ascend** | Plugin de hardware Ascend para vLLM; backend NPU dedicado | https://github.com/vllm-project/vllm-ascend |

> Stacks MindIE / CANN sobre todo vía docs/firmware de Huawei; añadir fila ⭐ cuando exista espejo público estable.

### Neuron-Trainium

| Marca | Proyecto | En una línea | Enlace |
|---|---|---|---|
| ☄️ | **aws-neuron/neuronx-distributed-inference** | NeuronX Distributed Inference (NxDI): inferencia LLM distribuida en Inferentia/Trainium | https://github.com/aws-neuron/neuronx-distributed-inference |
| ☄️ | **vllm-project/vllm-neuron** | Ruta plugin vLLM × Neuron; backend Trainium/Inferentia | https://github.com/vllm-project/vllm-neuron |

### TPU

| Marca | Proyecto | En una línea | Enlace |
|---|---|---|---|
| ☄️ | **vllm-project/tpu-inference** | Backend de inferencia TPU para vLLM; ligado a Google TPU | https://github.com/vllm-project/tpu-inference |
| ☄️ | **huggingface/optimum-tpu** | Hugging Face Optimum TPU: ruta dedicada para desplegar Transformers en TPU | https://github.com/huggingface/optimum-tpu |

### Apple-Metal

| Marca | Proyecto | En una línea | Enlace |
|---|---|---|---|
| ⭐ | **ml-explore/mlx** | Framework de arrays Apple Silicon; sustrato de ejecución de modelos en Metal | https://github.com/ml-explore/mlx |
| ⭐ | **ml-explore/mlx-lm** | Cadena de inferencia y serving LLM sobre MLX; Apple Silicon | https://github.com/ml-explore/mlx-lm |
| ⭐ | **apple/coremltools** | Conversión y despliegue Core ML; Neural Engine / GPU iOS/macOS | https://github.com/apple/coremltools |

### Intel

| Marca | Proyecto | En una línea | Enlace |
|---|---|---|---|
| ⭐ | **openvinotoolkit/openvino.genai** | OpenVINO GenAI: runtime y pipelines de IA generativa en CPU/GPU/NPU Intel | https://github.com/openvinotoolkit/openvino.genai |

### Edge-NPU

| Marca | Proyecto | En una línea | Enlace |
|---|---|---|---|
| ☄️ | **airockchip/rknn-llm** | Rockchip RKNN-LLM: stack LLM en NPU de placa (p. ej. RK3588) | https://github.com/airockchip/rknn-llm |
| ☄️ | **hailo-ai/hailort** | HailoRT: runtime de inferencia ligero de alto rendimiento en aceleradores Hailo | https://github.com/hailo-ai/hailort |

### Other accelerators

| Marca | Proyecto | En una línea | Enlace |
|---|---|---|---|
| ☄️ | **tenstorrent/vllm-tt-plugin** | Plugin backend vLLM de Tenstorrent; con la stack de operadores TT-Metalium | https://github.com/tenstorrent/vllm-tt-plugin |
| ☄️ | **tenstorrent/tt-metal** | TT-Metalium / TT-NN: modelo de programación de operadores/kernels en chips Tenstorrent | https://github.com/tenstorrent/tt-metal |

### Cross-vendor kernels

| Marca | Proyecto | En una línea | Enlace |
|---|---|---|---|
| ⭐ | **flashinfer-ai/flashinfer** | Biblioteca de kernels Attention / sampling para LLM serving; integrable | https://github.com/flashinfer-ai/flashinfer |

---

## MoE

Engines especializados Mixture-of-Experts: paralelismo de expertos, offload, planificación estratificada, kernels MoE.

### NVIDIA

| Marca | Proyecto | En una línea | Enlace |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepInfer** | Framework de inferencia de producción DeepSeek (OSS); DeepSeek-V4.1-Flash en NVIDIA SM100 / Ascend 950 | https://github.com/deepseek-ai/DeepInfer |

### Ascend

| Marca | Proyecto | En una línea | Enlace |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepInfer** | Igual; ruta Ascend 950 (doble hardware con NVIDIA SM100) | https://github.com/deepseek-ai/DeepInfer |

### CPU-RAM-SSD tier

> **Clase Strata:** aquí, «Strata» significa sobre todo [Niko1221/Strata](https://github.com/Niko1221/Strata) — engine de PC de consumo para MoE grandes (p. ej. Qwen3.8-Flash-Next) con **niveles VRAM / RAM de sistema / SSD** y **CPU calculando en paralelo expertos no cacheados**. Misma familia: generalizaciones MoE, offload host/SSD, orquestación CPU–GPU. Si hay homónimos, **confiar en los enlaces y one-liners de abajo**.

| Marca | Proyecto | En una línea | Enlace |
|---|---|---|---|
| ⭐ | **Niko1221/Strata** | Engine MoE tipo Qwen3.8-Flash-Next: expertos densos/calientes en GPU, todos en RAM + CPU paralelo, SSD n-gram; CUDA/HIP | https://github.com/Niko1221/Strata |
| ☄️ | **voidstackloop/extended-strata-moe** | Generaliza el tiering async GPU/CPU Strata a muchos MoE de llama.cpp (alineado en método; repo temprano) | https://github.com/voidstackloop/extended-strata-moe |
| ☄️ | **EfficientMoE/MoE-Infinity** | Offload de expertos MoE a memoria host/SSD + caché/prefetch consciente de activación | https://github.com/EfficientMoE/MoE-Infinity |
| ☄️ | **efeslab/fiddler** | ICLR'25: orquestación CPU–GPU MoE local (calcular expertos faltantes en CPU) | https://github.com/efeslab/fiddler |
| ⭐ | **kvcache-ai/ktransformers** | Inferencia MoE / modelos grandes híbrida CPU/GPU; offload de expertos y rutas de kernels | https://github.com/kvcache-ai/ktransformers |
| ⭐ | **Tiiny-AI/PowerInfer** | Engine híbrido GPU+CPU de consumo vía localidad de activación (neuronas calientes/frías); PowerInfer-2 Mixtral en dispositivo; ex-SJTU-IPADS | https://github.com/Tiiny-AI/PowerInfer |

### Cross-vendor kernels

| Marca | Proyecto | En una línea | Enlace |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepGEMM** | Biblioteca de kernels GPU BLAS/GEMM de alta eficiencia DeepSeek OSS | https://github.com/deepseek-ai/DeepGEMM |
| ⭐ | **deepseek-ai/DeepEP** | Biblioteca de comunicación Expert Parallel DeepSeek OSS; específica MoE | https://github.com/deepseek-ai/DeepEP |

---

## Multimodal / Omni

Engines para familias multimodal / Omni (voz · visión · texto).

### NVIDIA

| Marca | Proyecto | En una línea | Enlace |
|---|---|---|---|
| ☄️ · First-party | **InferMatrixLab/system1-omni** | Engine de alto rendimiento mantenido por la comunidad para System1 (Rust; estilo vLLM / vLLM-Omni) | https://github.com/InferMatrixLab/system1-omni |
| ☄️ · First-party | **InferMatrixLab/minicpm-o-4.5-single-gpu-engine** | Engine de voz streaming mono-GPU especializado en MiniCPM-o 4.5 | https://github.com/InferMatrixLab/minicpm-o-4.5-single-gpu-engine |

### Apple-Metal

| Marca | Proyecto | En una línea | Enlace |
|---|---|---|---|
| ☄️ · First-party | **InferMatrixLab/vllm-omni-mlx** | Servidor de inferencia omni-modalidad en Apple Silicon (API OpenAI / Anthropic) | https://github.com/InferMatrixLab/vllm-omni-mlx |

---

## Diffusion · Image

Rutas de engine especializadas o compile-heavy para difusión de imagen / generación de imágenes.

### NVIDIA

| Marca | Proyecto | En una línea | Enlace |
|---|---|---|---|
| ⭐ | **NVIDIA/TensorRT** | Optimizador y runtime de inferencia NVIDIA general; entrada a muchos engines CV/difusión/custom | https://github.com/NVIDIA/TensorRT |

---

## Diffusion · Video

Engines especializados en difusión / generación de vídeo.

> Sin filas verificadas aún; PRs bienvenidos bajo categoría de modelo → hardware.

---

## Speech · TTS / ASR

Engines especializados en síntesis / reconocimiento de voz.

### NVIDIA

| Marca | Proyecto | En una línea | Enlace |
|---|---|---|---|
| ☄️ · First-party | **InferMatrixLab/drama-3-single-b300-engine** | Engine TTS streaming para Fish Audio Drama 3 en un solo NVIDIA B300 | https://github.com/InferMatrixLab/drama-3-single-b300-engine |

### Ascend

| Marca | Proyecto | En una línea | Enlace |
|---|---|---|---|
| ☄️ · First-party | **InferMatrixLab/qwen3-tts-rsi-npu-engine** | Inferencia rápida autónoma de Qwen3-TTS en Ascend NPU (p. ej. 910B) vía ruta RSI | https://github.com/InferMatrixLab/qwen3-tts-rsi-npu-engine |

---

## Embedding / Rerank

Rutas de inferencia especializadas embedding / rerank.

> Sin filas verificadas aún; PRs bienvenidos bajo categoría de modelo → hardware.

---

## Other

Engines y catálogos de recetas aún modelo×hardware pero fuera de las clases anteriores.

### NVIDIA

| Marca | Proyecto | En una línea | Enlace |
|---|---|---|---|
| ☄️ · First-party | **InferMatrixLab/vllm-rlt** | Engine para transformers con bucles: planificación a nivel loop y stages componibles | https://github.com/InferMatrixLab/vllm-rlt |

### Catalogs

| Marca | Proyecto | En una línea | Enlace |
|---|---|---|---|
| ☄️ · First-party | **InferMatrixLab/recipe** | Catálogo comunitario de recetas «modelo × engine × hardware» | https://github.com/InferMatrixLab/recipe |

---

## Índice first-party · InferMatrixLab (no Spec de terceros)

> **Límite (obligatorio):** filas **InferMatrixLab** ya colocadas en las tablas (marcadas First-party). **No son** Spec industriales de terceros. Solo índice de transparencia.

| Proyecto | Ubicación | Enlace |
|---|---|---|
| system1-omni | Multimodal / Omni → NVIDIA | https://github.com/InferMatrixLab/system1-omni |
| minicpm-o-4.5-single-gpu-engine | Multimodal / Omni → NVIDIA | https://github.com/InferMatrixLab/minicpm-o-4.5-single-gpu-engine |
| vllm-omni-mlx | Multimodal / Omni → Apple-Metal | https://github.com/InferMatrixLab/vllm-omni-mlx |
| drama-3-single-b300-engine | Speech · TTS / ASR → NVIDIA | https://github.com/InferMatrixLab/drama-3-single-b300-engine |
| qwen3-tts-rsi-npu-engine | Speech · TTS / ASR → Ascend | https://github.com/InferMatrixLab/qwen3-tts-rsi-npu-engine |
| vllm-rlt | Other → NVIDIA | https://github.com/InferMatrixLab/vllm-rlt |
| recipe | Other → Catalogs | https://github.com/InferMatrixLab/recipe |

---

## Contrast · Límite vs Serving genérico

| Proyecto habitual | Postura | Nota |
|---|---|---|
| vLLM / SGLang / TGI | Sin directorio | Solo plugins **Ascend / Neuron / TPU / TT** (bajo clase × hardware) |
| Ollama / llama.cpp | Rechazo por defecto | Runtime portable cross-hardware; discutir fila si un backend se vuelve «ruta oficial de chip» |
| Triton Inference Server | Sin directorio de producto | Cáscara de orquestación; backends (TRT-LLM etc.) ya listados por modelo × hardware |

---

## Related

- **Índice first-party:** [Índice first-party · InferMatrixLab](#índice-first-party--infermatrixlab-no-spec-de-terceros)
- Otros docs de inferencia InferMatrixLab (enlaces cruzados en la org más adelante)
- Para serving genérico, usar otro awesome / manual — no mezclar tablas con este repo

---

## License

Contenido de la lista contribuido en espíritu **CC0 1.0** (reutilización libre de las tablas). Los proyectos enlazados conservan sus licencias.