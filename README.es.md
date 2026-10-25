# Awesome Model × Hardware Inference Engines

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

**Languages:** [English](README.en.md) · [中文](README.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Français](README.fr.md) · [Español](README.es.md)

> **Motores de inferencia especializados modelo × hardware** · specialized backends · not a general serving yellow pages  
> Lista curada de **motores de inferencia especializados por modelo/hardware** — motores y plugins cuyo valor está ligado a una **familia de modelos** y/o un **acelerador**, no stacks genéricos de serving LLM.

**En alcance:** motores especializados de planificación de expertos estratificada / híbrida CPU–GPU（familia de métodos Strata）；motores de inferencia compile-time o a nivel kernel para chips / runtimes específicos; runtimes especializados por familia de modelos (p. ej. clase DeepSeek); plugins EP / backend de vendor (Ascend, Neuron, TPU, Tenstorrent…); stacks LLM NPU edge; bibliotecas de kernels MoE / attention (citables como «capa de motor»).  
**Fuera de alcance:** directorios amarillos de megapacks de serving genérico (vLLM / SGLang / TGI / Ollama) — incluir una fila solo si es claramente un **backend / plugin específico de acelerador o familia de modelos**; frameworks de entrenamiento; tablas de benchmarks puras; páginas de marketing sin implementación OSS/docs.

**Marcas:** ⭐ Establecido / ampliamente adoptado · ☄️ En ascenso / a vigilar  
**Estructura:** Method Family × Hardware Domain  
**Idiomas:** edición en español; el chino es la versión principal en [README.md](README.md). Nombres de proyectos y enlaces se mantienen en inglés.

### Motor especializado ≠ Serving genérico (leer primero)

| Concepto | Qué es | ¿Este repo? |
|---|---|---|
| **Motor especializado** | Ruta de inferencia compilada o profundamente custom para ISA de chip / runtime de vendor / familia de modelos | ✅ Aquí |
| **Serving genérico** | Stack de scheduling multi-modelo multi-GPU (vLLM, SGLang, TGI…) | ❌ Sin directorio; solo sus **filas de plugins hard/modelo** |
| **Biblioteca de kernels** | Capa de operadores invocable por varios motores (FlashAttention / DeepGEMM…) | ✅ OK en «Kernels / MoE» |
| **Herramientas de formato / conversión** | Solo export ONNX/GGUF, sin runtime de inferencia | ❌ En general no (cadena Core ML Tools conversión+despliegue puede calificar) |

---

## Reglas de contribución

- **⭐ Established:** docs sólidos; ruta build/run reproducible; público ~≥ 6 meses o estándar de facto de un stack de chip.
- **☄️ Rising:** activo en los últimos 12 meses; puede nombrar la familia de modelos o el hardware ligado; enlace repo/docs verificable.
- **Requerido:** qué modelo/hardware, definición del problema en una frase, enlace, sección, ⭐/☄️.
- **Rechazo:** anuncios de repos de serving genérico enteros; sin especialización hard/modelo; solo wrappers API.
- PRs bienvenidos; abrir un issue primero si la sección no está clara.

---

## Tabla de contenidos

- [Hardware · NVIDIA (familia TensorRT)](#hardware--nvidia-familia-tensorrt)
- [Hardware · Ascend / NPU doméstico](#hardware--ascend--npu-doméstico)
- [Hardware · AWS Inferentia / Trainium](#hardware--aws-inferentia--trainium)
- [Hardware · TPU](#hardware--tpu)
- [Hardware · Apple / Metal](#hardware--apple--metal)
- [Hardware · Intel OpenVINO / CPU·iGPU·NPU](#hardware--intel-openvino--cpuiGPUnpu)
- [Hardware · NPU edge / móvil](#hardware--npu-edge--móvil)
- [Hardware · Otros plugins de acelerador](#hardware--otros-plugins-de-acelerador)
- [Model · Runtime especializado por familia de modelos](#model--runtime-especializado-por-familia-de-modelos)
- [Method · Planificación estratificada / especializada（clase Strata）](#method--planificación-estratificada--especializadaclase-strata)
- [Propio · InferMatrixLab（no es Spec de terceros）](#propio--infermatrixlabno-es-spec-de-terceros)
- [Kernels · Ops especializadas MoE / Attention](#kernels--ops-especializadas-moe--attention)
- [Contrast · Frontera vs Serving genérico](#contrast--frontera-vs-serving-genérico)
- [Related](#related)
- [License](#license)

---

## Hardware · NVIDIA (familia TensorRT)

Motores LLM y de optimización de grafos **compile-time / grado vendor** para GPU NVIDIA (no «otro servidor compatible con OpenAI»).

| Marca | Proyecto | En una frase | Enlace |
|---|---|---|---|
| ⭐ | **NVIDIA/TensorRT-LLM** | Motor de inferencia LLM/VLM oficial de NVIDIA: kernels CUDA custom, build de engine, batching in-flight; ligado a GPU NVIDIA | https://github.com/NVIDIA/TensorRT-LLM |
| ⭐ | **NVIDIA/TensorRT** | Optimizador y runtime de inferencia NVIDIA general; entrada a muchos motores CV/difusión/redes custom | https://github.com/NVIDIA/TensorRT |

---

## Hardware · Ascend / NPU doméstico

Backends y plugins especializados en Ascend y NPU similares (el núcleo vLLM genérico no se lista — solo rutas Ascend).

| Marca | Proyecto | En una frase | Enlace |
|---|---|---|---|
| ☄️ | **vllm-project/vllm-ascend** | Plugin de hardware Ascend (昇腾) para vLLM; backend NPU dedicado, no un directorio genérico | https://github.com/vllm-project/vllm-ascend |

> Las stacks oficiales MindIE / CANN van sobre todo por docs y firmware de Huawei; añadir una fila ⭐ cuando exista un espejo público estable.

---

## Hardware · AWS Inferentia / Trainium

| Marca | Proyecto | En una frase | Enlace |
|---|---|---|---|
| ☄️ | **aws-neuron/neuronx-distributed-inference** | NeuronX Distributed Inference (NxDI): inferencia LLM distribuida en Inferentia/Trainium | https://github.com/aws-neuron/neuronx-distributed-inference |
| ☄️ | **vllm-project/vllm-neuron** | Ruta de plugin vLLM × Neuron; backend dedicado Trainium/Inferentia | https://github.com/vllm-project/vllm-neuron |

---

## Hardware · TPU

| Marca | Proyecto | En una frase | Enlace |
|---|---|---|---|
| ☄️ | **vllm-project/tpu-inference** | Backend de inferencia TPU de vLLM (tpu-inference); ligado a TPU de Google | https://github.com/vllm-project/tpu-inference |
| ☄️ | **huggingface/optimum-tpu** | Hugging Face Optimum TPU: ruta dedicada para desplegar Transformers en TPU | https://github.com/huggingface/optimum-tpu |

---

## Hardware · Apple / Metal

| Marca | Proyecto | En una frase | Enlace |
|---|---|---|---|
| ⭐ | **ml-explore/mlx** | Framework de arrays estilo oficial para Apple Silicon; base de ejecución de modelos en Metal | https://github.com/ml-explore/mlx |
| ⭐ | **ml-explore/mlx-lm** | Cadena de herramientas de inferencia y serving LLM sobre MLX; ligada a Apple Silicon | https://github.com/ml-explore/mlx-lm |
| ⭐ | **apple/coremltools** | Cadena de conversión y despliegue Core ML; ruta Neural Engine / GPU iOS/macOS | https://github.com/apple/coremltools |

---

## Hardware · Intel OpenVINO / CPU·iGPU·NPU

| Marca | Proyecto | En una frase | Enlace |
|---|---|---|---|
| ⭐ | **openvinotoolkit/openvino.genai** | OpenVINO GenAI: runtime y pipelines de IA generativa en CPU/GPU/NPU Intel | https://github.com/openvinotoolkit/openvino.genai |

---

## Hardware · NPU edge / móvil

| Marca | Proyecto | En una frase | Enlace |
|---|---|---|---|
| ☄️ | **airockchip/rknn-llm** | Rockchip RKNN-LLM: stack de inferencia LLM en NPU de placa (p. ej. RK3588) | https://github.com/airockchip/rknn-llm |
| ☄️ | **hailo-ai/hailort** | HailoRT: runtime de inferencia ligero de alto rendimiento en aceleradores edge Hailo | https://github.com/hailo-ai/hailort |

---

## Hardware · Otros plugins de acelerador

| Marca | Proyecto | En una frase | Enlace |
|---|---|---|---|
| ☄️ | **tenstorrent/vllm-tt-plugin** | Plugin backend vLLM de Tenstorrent; junto con la pila de operadores TT-Metalium | https://github.com/tenstorrent/vllm-tt-plugin |
| ☄️ | **tenstorrent/tt-metal** | TT-Metalium / TT-NN: modelo de programación de operadores y kernels en chips Tenstorrent | https://github.com/tenstorrent/tt-metal |

---

## Model · Runtime especializado por familia de modelos

Motores profundamente custom para estructuras de modelo concretas (DeepSeek MoE, layouts cuantizados de alta compresión, offload híbrido de expertos, etc.).

> Ver también [Method · Planificación estratificada / especializada（clase Strata）](#method--planificación-estratificada--especializadaclase-strata) más abajo.

| Marca | Proyecto | En una frase | Enlace |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepInfer** | Framework de inferencia de producción DeepSeek (OSS); ligado a DeepSeek-V4.1-Flash en NVIDIA SM100 / Ascend 950 | https://github.com/deepseek-ai/DeepInfer |
| ☄️ | **turboderp-org/exllamav3** | Inferencia LLM cuantizada de alta velocidad para GPU NVIDIA de consumo modernas (línea ExLlama) | https://github.com/turboderp-org/exllamav3 |
| ⭐ | **kvcache-ai/ktransformers** | Framework de inferencia MoE / grandes modelos híbrido CPU/GPU; offload de expertos y rutas de kernels | https://github.com/kvcache-ai/ktransformers |

---

## Method · Planificación estratificada / especializada（clase Strata）

> **Nota de nombre:** Aquí «Strata» significa sobre todo [Niko1221/Strata](https://github.com/Niko1221/Strata) — un motor **especializado por modelo** para MoE grandes（p. ej. Qwen3.8-Flash-Next）en PC de consumo, con **capas VRAM / RAM de sistema / SSD** y **CPU calculando en paralelo expertos no cacheados**. La misma familia de métodos incluye generalizaciones a más MoE, offload a host/SSD y orquestación CPU–GPU. Si hay homónimos, **valen los enlaces y las frases de abajo**.

| Marca | Proyecto | Una línea | Enlace |
|---|---|---|---|
| ⭐ | **Niko1221/Strata** | Motor de consumo para MoE tipo Qwen3.8-Flash-Next: expertos densos/calientes en GPU, todos los expertos fijados en RAM con cómputo CPU paralelo de fallos, n-gram en SSD; CUDA/HIP | https://github.com/Niko1221/Strata |
| ☄️ | **voidstackloop/extended-strata-moe** | Generaliza el tiering asíncrono GPU/CPU estilo Strata a muchas arquitecturas MoE de llama.cpp (alineado en método; repo temprano) | https://github.com/voidstackloop/extended-strata-moe |
| ☄️ | **EfficientMoE/MoE-Infinity** | Offload de expertos MoE a memoria host/SSD + caché y prefetch conscientes de activación; biblioteca + ruta de servicio | https://github.com/EfficientMoE/MoE-Infinity |
| ☄️ | **efeslab/fiddler** | ICLR'25: orquestación CPU–GPU para MoE local (expertos faltantes se calculan en CPU en vez de mover pesos) | https://github.com/efeslab/fiddler |

---

## Propio · InferMatrixLab（no es Spec de terceros）

> **Límite（obligatorio）:** Filas siguientes = motores y recetas **especializados** modelo/hardware mantenidos por **InferMatrixLab**, para enlaces internos y transparencia. **No** son Spec industrial de terceros y **no** deben citarse como «norma oficial» ni filas de autoridad Hardware/Model. **Separadas** de las filas de terceros de arriba.

| Marca | Proyecto | Una línea | Enlace |
|---|---|---|---|
| ☄️ | **InferMatrixLab/system1-omni** | Motor de inferencia de alto rendimiento mantenido por la comunidad para la familia System1 (Rust; estilo vLLM / vLLM-Omni) | https://github.com/InferMatrixLab/system1-omni |
| ☄️ | **InferMatrixLab/vllm-rlt** | Motor para transformers en bucle: planificación a nivel loop y etapas componibles | https://github.com/InferMatrixLab/vllm-rlt |
| ☄️ | **InferMatrixLab/minicpm-o-4.5-single-gpu-engine** | Motor de voz streaming mono-GPU especializado en MiniCPM-o 4.5 (comparable a vLLM-Omni / SGLang-Omni) | https://github.com/InferMatrixLab/minicpm-o-4.5-single-gpu-engine |
| ☄️ | **InferMatrixLab/vllm-omni-mlx** | Servidor de inferencia omni-modalidad en Apple Silicon (API compatible OpenAI / Anthropic) | https://github.com/InferMatrixLab/vllm-omni-mlx |
| ☄️ | **InferMatrixLab/qwen3-tts-rsi-npu-engine** | Inferencia rápida independiente de Qwen3-TTS en NPU Ascend (p. ej. 910B) vía ruta RSI | https://github.com/InferMatrixLab/qwen3-tts-rsi-npu-engine |
| ☄️ | **InferMatrixLab/drama-3-single-b300-engine** | Motor TTS streaming especializado en Fish Audio Drama 3 en un solo NVIDIA B300 | https://github.com/InferMatrixLab/drama-3-single-b300-engine |
| ☄️ | **InferMatrixLab/recipe** | Catálogo comunitario de recetas «modelo × motor × hardware» (no un listín serving genérico) | https://github.com/InferMatrixLab/recipe |

---

## Kernels · Ops especializadas MoE / Attention

**Bibliotecas de kernels especializadas** componibles por motores superiores (no productos de serving completos, pero la capa de rendimiento «modelo×hardware»).

| Marca | Proyecto | En una frase | Enlace |
|---|---|---|---|
| ⭐ | **flashinfer-ai/flashinfer** | Biblioteca de kernels Attention / sampling para LLM serving; integrable por varios motores | https://github.com/flashinfer-ai/flashinfer |
| ⭐ | **deepseek-ai/DeepGEMM** | Biblioteca de kernels GPU BLAS/GEMM de alta eficiencia (OSS DeepSeek) | https://github.com/deepseek-ai/DeepGEMM |
| ⭐ | **deepseek-ai/DeepEP** | Biblioteca de comunicación Expert Parallel (OSS DeepSeek); específica MoE | https://github.com/deepseek-ai/DeepEP |

---

## Contrast · Frontera vs Serving genérico

| Proyecto habitual | Postura aquí | Nota |
|---|---|---|
| vLLM / SGLang / TGI | Sin directorio | Solo sus filas de plugins **Ascend / Neuron / TPU / TT** |
| Ollama / llama.cpp | Rechazo por defecto | Runtime portable cross-hardware; discutir una fila aparte si un backend se vuelve «ruta oficial de chip» |
| Triton Inference Server | Sin directorio de producto | Cáscara de orquestación/serving; motores backend (TRT-LLM etc.) ya listados arriba |

---

## Related

- **Motores propios:** ver [Propio · InferMatrixLab](#propio--infermatrixlabno-es-spec-de-terceros)（proyectos de la org, no Spec）
- Otros docs y comparaciones de ingeniería de inferencia de InferMatrixLab (enlaces cruzados en la org más adelante)
- Para elegir serving genérico, use un awesome / manual aparte — no mezcle tablas con este repo

---

## License

El contenido de la lista se contribuye en el espíritu de **CC0 1.0** (reutilización libre de las tablas de entradas). Los proyectos enlazados conservan sus propias licencias.
