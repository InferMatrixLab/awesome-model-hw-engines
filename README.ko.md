# Awesome Model × Hardware Inference Engines

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

**Languages:** [English](README.en.md) · [中文](README.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Français](README.fr.md) · [Español](README.es.md)

> **모델 × 하드웨어 전용 추론 엔진 큐레이션** · specialized backends · not a general serving yellow pages  
> 가치가 **모델 계열** 및/또는 **가속기**에 묶인 엔진·플러그인 목록（일반 LLM 서빙 황색 페이지 아님）.

**In scope:** **모델 카테고리**로 정리한 뒤 **하드웨어**로 세분하는 전용 추론 엔진·플러그인; 계층/하이브리드 CPU–GPU 전문가 스케줄링(Strata 계열); 모델족 런타임; 벤더 EP/백엔드 플러그인; 엣지 NPU; 인용 가능한 MoE/Attention 커널.  
**Out of scope:** vLLM / SGLang / TGI / Ollama 등 **일반 서빙 황색 페이지**（하드웨어·모델족 전용 백엔드/플러그인 행만 수록）; 학습 프레임워크; 순수 벤치; 구현 없는 마케팅 페이지.

**표기:** ⭐ 확립/널리 채택 · ☄️ 상승/주시 · **자사** = InferMatrixLab 유지（제3자 Spec 아님）  
**구조:** **L1 = 모델 카테고리** → **L2 = 하드웨어**（NVIDIA / Ascend / Neuron-Trainium / TPU / Apple-Metal / Intel / Edge-NPU / CPU-RAM-SSD tier / Cross-vendor kernels; 미등재 칩은 Other accelerators）  
**언어:** 한국어 판; 주 판은 [中文 README.md](README.md). 프로젝트명·링크는 영어 유지.

### 전용 엔진 ≠ 일반 Serving（먼저 읽기）

| 개념 | 무엇인가 | 이 저장소? |
|---|---|---|
| **전용 엔진** | 칩 ISA / 벤더 runtime / 모델족용으로 컴파일·심층 커스텀된 추론 경로 | ✅ 여기 |
| **일반 Serving** | 다중 모델·다중 GPU 통합 스케줄링（vLLM, SGLang, TGI…） | ❌ 황색 페이지 없음; **하드/모델 전용 플러그인 행만** |
| **커널 라이브러리** | 여러 엔진이 호출하는 연산자 층 | ✅ 해당 모델류 → Cross-vendor kernels |
| **포맷/변환 도구** | ONNX/GGUF 내보내기만, 추론 runtime 없음 | ❌ 원칙 거부（Core ML Tools 등은 예외 가능） |

---

## 기여 규칙

- **⭐ Established:** 문서 충실; 재현 가능한 빌드/실행; 공개 약 ≥ 6개월 또는 칩 스택 사실상 표준.
- **☄️ Rising:** 최근 12개월 활성; 묶인 모델족/하드웨어 설명 가능; 검증 가능 링크.
- **필수:** 모델 카테고리, 하드웨어, 한 줄 문제 정의, 링크, ⭐/☄️; 자사 행 표기.
- **거부:** 일반 서빙 통째 광고; 전용성 없음; API 래퍼만.
- PR 환영; 구역이 불명확하면 먼저 issue.

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
- [자사 색인 · InferMatrixLab（제3자 Spec 아님）](#자사-색인--infermatrixlab제3자-spec-아님)
- [Contrast · Boundary vs generic Serving](#contrast--boundary-vs-generic-serving)
- [Related](#related)
- [License](#license)

---

## Dense LLM

밀집 Transformer / 디코더 LLM（비 MoE 주체）용 전용 엔진·하드웨어 백엔드.

### NVIDIA

| 표기 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ⭐ | **NVIDIA/TensorRT-LLM** | NVIDIA 공식 LLM/VLM 추론 엔진: 커스텀 CUDA 커널, 엔진 빌드, IB 배칭; NVIDIA GPU | https://github.com/NVIDIA/TensorRT-LLM |
| ☄️ | **turboderp-org/exllamav3** | 현대 소비자 NVIDIA GPU용 고속 양자화 LLM 추론（ExLlama 계열） | https://github.com/turboderp-org/exllamav3 |

### NVIDIA · RTX / Blackwell (SM120)

| 표기 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ☄️ | **NVIDIA/flare-local-inference** | 로컬 Agent 추론: PyTorch 빌드 + Rust 서빙; 전체 대화 상태(KV + recurrent); NVIDIA SM120/SM121; 연구 프로토타입(vLLM 대체 아님) | https://github.com/NVIDIA/flare-local-inference |

### Ascend

| 표기 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ☄️ | **vllm-project/vllm-ascend** | vLLM Ascend（昇腾）하드웨어 플러그인; NPU 전용 백엔드 | https://github.com/vllm-project/vllm-ascend |

> MindIE / CANN 공식 스택은 주로 Huawei 문서·펌웨어 경로; 안정 공개 미러 후 ⭐ 행 추가.

### Neuron-Trainium

| 표기 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ☄️ | **aws-neuron/neuronx-distributed-inference** | NeuronX Distributed Inference（NxDI）: Inferentia/Trainium 분산 LLM 추론 | https://github.com/aws-neuron/neuronx-distributed-inference |
| ☄️ | **vllm-project/vllm-neuron** | vLLM × Neuron 플러그인; Trainium/Inferentia 전용 백엔드 | https://github.com/vllm-project/vllm-neuron |

### TPU

| 표기 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ☄️ | **vllm-project/tpu-inference** | vLLM TPU 추론 백엔드; Google TPU | https://github.com/vllm-project/tpu-inference |
| ☄️ | **huggingface/optimum-tpu** | Hugging Face Optimum TPU: TPU에 Transformer 배포 전용 경로 | https://github.com/huggingface/optimum-tpu |

### Apple-Metal

| 표기 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ⭐ | **ml-explore/mlx** | Apple Silicon 배열 프레임워크; Metal 모델 실행 기반 | https://github.com/ml-explore/mlx |
| ⭐ | **ml-explore/mlx-lm** | MLX LLM 추론·서빙 툴체인; Apple Silicon | https://github.com/ml-explore/mlx-lm |
| ⭐ | **apple/coremltools** | Core ML 변환·배포 툴체인; iOS/macOS Neural Engine / GPU | https://github.com/apple/coremltools |

### Intel

| 표기 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ⭐ | **openvinotoolkit/openvino.genai** | OpenVINO GenAI: Intel CPU/GPU/NPU 생성형 AI 추론 런타임·파이프라인 | https://github.com/openvinotoolkit/openvino.genai |

### Edge-NPU

| 표기 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ☄️ | **airockchip/rknn-llm** | Rockchip RKNN-LLM: RK3588 등 보드 NPU LLM 스택 | https://github.com/airockchip/rknn-llm |
| ☄️ | **hailo-ai/hailort** | HailoRT: Hailo 엣지 AI 가속기 경량 고성능 추론 runtime | https://github.com/hailo-ai/hailort |

### Other accelerators

| 표기 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ☄️ | **tenstorrent/vllm-tt-plugin** | Tenstorrent vLLM 백엔드 플러그인; TT-Metalium 연산자 스택 | https://github.com/tenstorrent/vllm-tt-plugin |
| ☄️ | **tenstorrent/tt-metal** | TT-Metalium / TT-NN: Tenstorrent 칩 연산자·커널 프로그래밍 모델 | https://github.com/tenstorrent/tt-metal |

### Cross-vendor kernels

| 표기 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ⭐ | **flashinfer-ai/flashinfer** | LLM Serving용 Attention/샘플링 커널; 다중 엔진 임베드 가능 | https://github.com/flashinfer-ai/flashinfer |

---

## MoE

Mixture-of-Experts 전용: 전문가 병렬, 오프로드, 계층 스케줄링, MoE 커널.

### NVIDIA

| 표기 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepInfer** | DeepSeek 프로덕션 추론 프레임워크 OSS; DeepSeek-V4.1-Flash, NVIDIA SM100 / Ascend 950 | https://github.com/deepseek-ai/DeepInfer |

### Ascend

| 표기 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepInfer** | 동일; Ascend 950 경로（NVIDIA SM100 이중 하드웨어） | https://github.com/deepseek-ai/DeepInfer |

### CPU-RAM-SSD tier

> **Strata 계열:** 본 목록에서 “Strata”는 주로 [Niko1221/Strata](https://github.com/Niko1221/Strata) — 대형 MoE（예: Qwen3.8-Flash-Next）용 소비자 PC 전용 엔진으로 **VRAM / 시스템 RAM / SSD 계층**과 **미캐시 전문가 CPU 병렬 계산**. 동일 방법족에는 더 많은 MoE 일반화·호스트/SSD 오프로드·CPU–GPU 조율이 포함. 동명 저장소가 있으면 **아래 링크와 한 줄을 기준**.

| 표기 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ⭐ | **Niko1221/Strata** | Qwen3.8-Flash-Next급 MoE: GPU 밀집/핫 전문가, RAM 전체 고정+CPU 병렬, SSD n-gram; CUDA/HIP | https://github.com/Niko1221/Strata |
| ☄️ | **voidstackloop/extended-strata-moe** | Strata식 비동기 GPU/CPU 전문가 계층을 llama.cpp 다중 MoE로 일반화（초기） | https://github.com/voidstackloop/extended-strata-moe |
| ☄️ | **EfficientMoE/MoE-Infinity** | MoE 전문가를 호스트 메모리/SSD로 오프로드+활성화 인지 캐시/프리페치 | https://github.com/EfficientMoE/MoE-Infinity |
| ☄️ | **efeslab/fiddler** | ICLR'25: 로컬 MoE CPU–GPU 조율（누락 전문가를 CPU에서 계산） | https://github.com/efeslab/fiddler |
| ⭐ | **kvcache-ai/ktransformers** | 하이브리드 CPU/GPU MoE/대형 모델 추론 최적화; 전문가 오프로드·커널 경로 | https://github.com/kvcache-ai/ktransformers |
| ⭐ | **Tiiny-AI/PowerInfer** | 소비자 GPU+CPU 하이브리드: activation locality(핫/콜드 뉴런); PowerInfer-2 온디바이스 Mixtral; 구 SJTU-IPADS | https://github.com/Tiiny-AI/PowerInfer |

### Cross-vendor kernels

| 표기 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepGEMM** | DeepSeek OSS 고효율 GPU BLAS/GEMM 커널 | https://github.com/deepseek-ai/DeepGEMM |
| ⭐ | **deepseek-ai/DeepEP** | DeepSeek OSS Expert Parallel 통신 라이브러리; MoE 전용 | https://github.com/deepseek-ai/DeepEP |

---

## Multimodal / Omni

멀티모달 / Omni（음성·시각·텍스트）모델족 전용 엔진.

### NVIDIA

| 표기 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ☄️ · 자사 | **InferMatrixLab/system1-omni** | System1 모델족 커뮤니티 유지 고성능 추론 엔진（Rust; vLLM / vLLM-Omni 계열） | https://github.com/InferMatrixLab/system1-omni |
| ☄️ · 자사 | **InferMatrixLab/minicpm-o-4.5-single-gpu-engine** | MiniCPM-o 4.5 단일 GPU 스트리밍 음성 전용 엔진 | https://github.com/InferMatrixLab/minicpm-o-4.5-single-gpu-engine |

### Apple-Metal

| 표기 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ☄️ · 자사 | **InferMatrixLab/vllm-omni-mlx** | Apple Silicon 전모달 추론 서버（OpenAI / Anthropic 호환 API） | https://github.com/InferMatrixLab/vllm-omni-mlx |

---

## Diffusion · Image

이미지 확산 / 이미지 생성 전용·컴파일형 엔진 경로.

### NVIDIA

| 표기 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ⭐ | **NVIDIA/TensorRT** | 일반 NVIDIA 추론 옵티마이저 & runtime; 다수 CV/확산/커스텀 네트워크 전용 엔진 입구 | https://github.com/NVIDIA/TensorRT |

---

## Diffusion · Video

비디오 확산 / 비디오 생성 전용 엔진.

> 검증된 행 아직 없음; 모델 카테고리 → 하드웨어로 PR 환영.

---

## Speech · TTS / ASR

음성 합성 / 인식 모델족 전용 엔진.

### NVIDIA

| 표기 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ☄️ · 자사 | **InferMatrixLab/drama-3-single-b300-engine** | Fish Audio Drama 3 단일 NVIDIA B300 스트리밍 TTS 전용 엔진 | https://github.com/InferMatrixLab/drama-3-single-b300-engine |

### Ascend

| 표기 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ☄️ · 자사 | **InferMatrixLab/qwen3-tts-rsi-npu-engine** | Ascend NPU（예: 910B）독립 고속 Qwen3-TTS 추론（RSI 경로） | https://github.com/InferMatrixLab/qwen3-tts-rsi-npu-engine |

---

## Embedding / Rerank

임베딩 / 리랭크 모델 전용 추론 경로.

> 검증된 행 아직 없음; 모델 카테고리 → 하드웨어로 PR 환영.

---

## Other

위 대분류에 안 들어가지만 여전히 모델×하드웨어 전용인 엔진·레시피 입구.

### NVIDIA

| 표기 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ☄️ · 자사 | **InferMatrixLab/vllm-rlt** | looped transformer 추론 엔진: loop급 스케줄링·조합 가능 스테이지 | https://github.com/InferMatrixLab/vllm-rlt |

### Catalogs

| 표기 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ☄️ · 자사 | **InferMatrixLab/recipe** | 「모델 × 엔진 × 하드웨어」추론 레시피 커뮤니티 카탈로그 | https://github.com/InferMatrixLab/recipe |

---

## 자사 색인 · InferMatrixLab（제3자 Spec 아님）

> **경계（필수）:** 아래는 **InferMatrixLab** 유지 전용 엔진·레시피로 위 표에 이미 배치（「자사」표기）. **제3자 산업 Spec이 아님**. 투명성 색인만.

| 프로젝트 | 배치 | 링크 |
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

| 흔한 프로젝트 | 입장 | 설명 |
|---|---|---|
| vLLM / SGLang / TGI | 황색 페이지 없음 | **Ascend / Neuron / TPU / TT** 전용 플러그인 행만（모델류 × 하드웨어） |
| Ollama / llama.cpp | 원칙 거부 | 크로스 하드웨어 휴대 runtime; 칩 공식 경로가 되면 별도 행 논의 |
| Triton Inference Server | 제품 황색 페이지 없음 | 오케스트레이션 껍데기; 백엔드（TRT-LLM 등）은 모델×하드웨어에 이미 수록 |

---

## Related

- **자사 색인:** [자사 색인 · InferMatrixLab](#자사-색인--infermatrixlab제3자-spec-아님)
- InferMatrixLab 기타 추론 문서（조직 내 추후 상호 링크）
- 일반 서빙 선정은 별도 inference-serving awesome / 핸드북 — 이 저장소와 표 혼합 금지

---

## License

목록 내용은 **CC0 1.0** 정신으로 기여（항목 표 자유 재사용）. 링크된 프로젝트는 각자 라이선스 유지.