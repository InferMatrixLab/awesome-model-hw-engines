# Awesome Model × Hardware Inference Engines

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

**Languages:** [English](README.en.md) · [中文](README.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Français](README.fr.md) · [Español](README.es.md)

> **모델 × 하드웨어 전용 추론 엔진 큐레이션** · specialized backends · not a general serving yellow pages  
> **모델 패밀리 및/또는 가속기**에 가치가 묶인 엔진·플러그인 목록. 범용 LLM serving 스택 디렉터리가 아닙니다.

**포함：** 계층 / 하이브리드 CPU–GPU 전문가 스케줄링 전용 엔진(Strata 방법족); 특정 칩 / 런타임용 컴파일형 또는 커널급 추론 엔진; 모델 패밀리 전용 runtime(예: DeepSeek급); 벤더 EP / 백엔드 플러그인(Ascend, Neuron, TPU, Tenstorrent…); 엣지 NPU LLM 스택; MoE / attention 전용 커널 라이브러리(「엔진 계층」으로 독립 인용 가능할 때).  
**제외：** vLLM / SGLang / TGI / Ollama 등**범용 serving 일괄 디렉터리**(행이 명확히 「특정 가속기 또는 모델 패밀리 전용 백엔드 / 플러그인」일 때만 수록); 학습 프레임워크; 순수 벤치보드; OSS/문서 구현 없는 마케팅 페이지.

**표시：** ⭐ 성숙 / 널리 채택 · ☄️ 상승 중 / 주시  
**구조：** Method Family × Hardware Domain  
**언어：** 한국어판; 중국어 주판은 [README.md](README.md). 프로젝트명과 링크는 영어 유지.

### 전용 엔진 ≠ 범용 Serving (먼저 읽기)

| 개념 | 무엇인가 | 이 저장소? |
|---|---|---|
| **전용 엔진** | 칩 ISA / 벤더 runtime / 모델 패밀리용으로 컴파일·깊게 커스텀된 추론 경로 | ✅ 여기 |
| **범용 Serving** | 다중 모델·다중 GPU 통합 스케줄링(vLLM, SGLang, TGI…) | ❌ 디렉터리 미수록; **하드/모델 전용 플러그인 행**만 |
| **커널 라이브러리** | 여러 엔진이 호출하는 연산자 계층(FlashAttention / DeepGEMM…) | ✅ 「Kernels / MoE」 가능 |
| **포맷/변환 도구** | ONNX/GGUF 내보내기만, 추론 runtime 없음 | ❌ 원칙 거절(Core ML Tools 변환+배포 체인은 예외 가능) |

---

## 기여 / 수록 규칙

- **⭐ Established：** 문서 완비; 재현 가능한 빌드/실행 경로; 공개 약 ≥ 6개월 또는 특정 칩 스택 사실상 표준.
- **☄️ Rising：** 최근 12개월 활발; 묶인 모델 패밀리 또는 하드웨어 설명 가능; 검증 가능한 저장소/문서.
- **필수：** 대상 모델/하드, 한 줄 문제 정의, 링크, 구역, ⭐/☄️.
- **거절：** 범용 serving 전체 광고; 하드/모델 전용성 없음; API 래퍼만.
- PR 환영; 구역이 불명확하면 먼저 issue.

---

## 목차

- [Hardware · NVIDIA (TensorRT 계열)](#hardware--nvidia-tensorrt-계열)
- [Hardware · Ascend / 국산 NPU](#hardware--ascend--국산-npu)
- [Hardware · AWS Inferentia / Trainium](#hardware--aws-inferentia--trainium)
- [Hardware · TPU](#hardware--tpu)
- [Hardware · Apple / Metal](#hardware--apple--metal)
- [Hardware · Intel OpenVINO / CPU·iGPU·NPU](#hardware--intel-openvino--cpuiGPUnpu)
- [Hardware · 엣지 NPU / 모바일](#hardware--엣지-npu--모바일)
- [Hardware · 기타 가속기 플러그인](#hardware--기타-가속기-플러그인)
- [Model · 모델 패밀리 전용 Runtime](#model--모델-패밀리-전용-runtime)
- [Method · 계층 / 전용 스케줄링（Strata 계）](#method--계층--전용-스케줄링strata-계)
- [자사 · InferMatrixLab（제3자 Spec 아님）](#자사--infermatrixlab제3자-spec-아님)
- [Kernels · MoE / Attention 전용 연산자](#kernels--moe--attention-전용-연산자)
- [Contrast · 범용 Serving과의 경계](#contrast--범용-serving과의-경계)
- [Related](#related)
- [License](#license)

---

## Hardware · NVIDIA (TensorRT 계열)

NVIDIA GPU용 **컴파일형 / 벤더급** LLM 및 그래프 최적화 엔진(「또 하나의 OpenAI 호환 server」가 아님).

| 표시 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ⭐ | **NVIDIA/TensorRT-LLM** | NVIDIA 공식 LLM/VLM 추론 엔진: 커스텀 CUDA 커널, 엔진 빌드, 인플라이트 배치; NVIDIA GPU 전용 | https://github.com/NVIDIA/TensorRT-LLM |
| ⭐ | **NVIDIA/TensorRT** | 범용 NVIDIA 추론 옵티마이저 & runtime; CV/확산/커스텀 네트워크 전용 엔진 구축 입구 | https://github.com/NVIDIA/TensorRT |

---

## Hardware · Ascend / 국산 NPU

昇腾 등 NPU 전용 백엔드·플러그인(범용 vLLM 본체 미수록, Ascend 경로만).

| 표시 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ☄️ | **vllm-project/vllm-ascend** | vLLM Ascend(昇騰) 하드웨어 플러그인; NPU 전용 백엔드(범용 목록 아님) | https://github.com/vllm-project/vllm-ascend |

> MindIE / CANN 공식 스택은 주로 화웨이 문서·펌웨어 경로; 안정적 공개 미러가 생기면 ⭐ 행 추가.

---

## Hardware · AWS Inferentia / Trainium

| 표시 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ☄️ | **aws-neuron/neuronx-distributed-inference** | NeuronX Distributed Inference(NxDI): Inferentia/Trainium 분산 LLM 추론 라이브러리 | https://github.com/aws-neuron/neuronx-distributed-inference |
| ☄️ | **vllm-project/vllm-neuron** | vLLM × Neuron 플러그인 경로; Trainium/Inferentia 전용 백엔드 | https://github.com/vllm-project/vllm-neuron |

---

## Hardware · TPU

| 표시 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ☄️ | **vllm-project/tpu-inference** | vLLM TPU 추론 백엔드(tpu-inference); Google TPU 전용 | https://github.com/vllm-project/tpu-inference |
| ☄️ | **huggingface/optimum-tpu** | Hugging Face Optimum TPU: TPU에 Transformer 배포하는 전용 경로 | https://github.com/huggingface/optimum-tpu |

---

## Hardware · Apple / Metal

| 표시 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ⭐ | **ml-explore/mlx** | 공식 스타일 Apple Silicon 배열 프레임워크; Metal 위 모델 실행 기반 | https://github.com/ml-explore/mlx |
| ⭐ | **ml-explore/mlx-lm** | MLX 기반 LLM 추론·서빙 툴체인; Apple Silicon 전용 | https://github.com/ml-explore/mlx-lm |
| ⭐ | **apple/coremltools** | Core ML 변환·배포 툴체인; iOS/macOS Neural Engine / GPU 경로 | https://github.com/apple/coremltools |

---

## Hardware · Intel OpenVINO / CPU·iGPU·NPU

| 표시 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ⭐ | **openvinotoolkit/openvino.genai** | OpenVINO GenAI: Intel CPU/GPU/NPU 생성형 AI 추론 runtime과 파이프라인 | https://github.com/openvinotoolkit/openvino.genai |

---

## Hardware · 엣지 NPU / 모바일

| 표시 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ☄️ | **airockchip/rknn-llm** | Rockchip RKNN-LLM: RK3588 등 보드 NPU LLM 추론 스택 | https://github.com/airockchip/rknn-llm |
| ☄️ | **hailo-ai/hailort** | HailoRT: Hailo 엣지 AI 가속기 경량 고성능 추론 runtime | https://github.com/hailo-ai/hailort |

---

## Hardware · 기타 가속기 플러그인

| 표시 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ☄️ | **tenstorrent/vllm-tt-plugin** | Tenstorrent vLLM 백엔드 플러그인; TT-Metalium 연산자 스택과 연동 | https://github.com/tenstorrent/vllm-tt-plugin |
| ☄️ | **tenstorrent/tt-metal** | TT-Metalium / TT-NN: Tenstorrent 칩 연산자·커널 프로그래밍 모델 | https://github.com/tenstorrent/tt-metal |

---

## Model · 모델 패밀리 전용 Runtime

특정 모델 구조(DeepSeek MoE, 고압축 양자화 레이아웃, 하이브리드 전문가 오프로드 등)에 깊게 커스텀된 엔진.

> 또한 아래 [Method · 계층 / 전용 스케줄링（Strata 계）](#method--계층--전용-스케줄링strata-계)를 참고.

| 표시 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepInfer** | DeepSeek 프로덕션 추론 프레임워크 OSS; DeepSeek-V4.1-Flash, NVIDIA SM100 / Ascend 950 | https://github.com/deepseek-ai/DeepInfer |
| ☄️ | **turboderp-org/exllamav3** | 현대 컨슈머 NVIDIA GPU용 고속 양자화 LLM 추론 라이브러리(ExLlama 계열) | https://github.com/turboderp-org/exllamav3 |
| ⭐ | **kvcache-ai/ktransformers** | CPU/GPU 혼합 MoE / 대형 모델 추론 최적화; 전문가 오프로드와 커널 경로 강조 | https://github.com/kvcache-ai/ktransformers |

---

## Method · 계층 / 전용 스케줄링（Strata 계）

> **이름 안내:** 이 목록에서 「Strata」는 주로 [Niko1221/Strata](https://github.com/Niko1221/Strata)를 가리킴——특정 대형 MoE(예: Qwen3.8-Flash-Next)를 위한 **VRAM / 시스템 RAM / SSD 계층**과 **캐시되지 않은 전문가를 CPU가 병렬 계산**하는 소비자 PC 전용 엔진. 같은 방법족에는 더 많은 MoE로의 일반화, 호스트/SSD 오프로드, CPU–GPU 조율도 포함. 동명 저장소가 있으면 **아래 링크와 한 줄을 우선**.

| 표시 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ⭐ | **Niko1221/Strata** | Qwen3.8-Flash-Next 계 소비자 전용 엔진: GPU에 밀집/핫 전문가, RAM에 전 전문가 핀 + CPU가 미스 병렬 계산, SSD n-gram; CUDA/HIP | https://github.com/Niko1221/Strata |
| ☄️ | **voidstackloop/extended-strata-moe** | Strata식 비동기 GPU/CPU 전문가 계층을 llama.cpp 지원 다수 MoE로 일반화(방법 정렬; 초기 저장소) | https://github.com/voidstackloop/extended-strata-moe |
| ☄️ | **EfficientMoE/MoE-Infinity** | MoE 전문가를 호스트 메모리/SSD로 오프로드 + 활성화 인지 캐시·프리페치 추론 라이브러리 및 서빙 | https://github.com/EfficientMoE/MoE-Infinity |
| ☄️ | **efeslab/fiddler** | ICLR'25: 로컬 장치 MoE용 CPU–GPU 조율(누락 전문가는 가중치 이동 대신 CPU 계산) | https://github.com/efeslab/fiddler |

---

## 자사 · InferMatrixLab（제3자 Spec 아님）

> **경계(필수):** 아래는 조직 **InferMatrixLab**이 유지하는 모델/하드웨어**전용** 추론 엔진과 레시피 입구. 조직 상호 링크·투명성용. **제3자 산업 Spec이 아니며**, 「공식 표준」이나 Hardware/Model 구간의 벤더 권위 행으로 인용하면 안 됨. 위 제3자 큐레이션과 **분리**.

| 표시 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ☄️ | **InferMatrixLab/system1-omni** | System1 모델족용 커뮤니티 유지 고성능 추론 엔진(Rust; vLLM / vLLM-Omni 스타일) | https://github.com/InferMatrixLab/system1-omni |
| ☄️ | **InferMatrixLab/vllm-rlt** | looped transformer용 추론 엔진: loop 수준 스케줄링과 조합 가능한 단계 실행 | https://github.com/InferMatrixLab/vllm-rlt |
| ☄️ | **InferMatrixLab/minicpm-o-4.5-single-gpu-engine** | MiniCPM-o 4.5 전용 단일 GPU 스트리밍 음성 엔진(vLLM-Omni / SGLang-Omni 대비 가능) | https://github.com/InferMatrixLab/minicpm-o-4.5-single-gpu-engine |
| ☄️ | **InferMatrixLab/vllm-omni-mlx** | Apple Silicon 전모달 추론 서버(OpenAI / Anthropic 호환 API) | https://github.com/InferMatrixLab/vllm-omni-mlx |
| ☄️ | **InferMatrixLab/qwen3-tts-rsi-npu-engine** | Ascend NPU(예: 910B)상 Qwen3-TTS 독립 고속 추론 엔진(RSI 경로) | https://github.com/InferMatrixLab/qwen3-tts-rsi-npu-engine |
| ☄️ | **InferMatrixLab/drama-3-single-b300-engine** | Fish Audio Drama 3용 단일 NVIDIA B300 스트리밍 TTS 전용 엔진 | https://github.com/InferMatrixLab/drama-3-single-b300-engine |
| ☄️ | **InferMatrixLab/recipe** | 「모델 × 엔진 × 하드웨어」커뮤니티 추론 레시피 목록(범용 serving 전화번호부 아님) | https://github.com/InferMatrixLab/recipe |

---

## Kernels · MoE / Attention 전용 연산자

상위 엔진이 조합하는 **전용 커널 라이브러리**(완전한 serving 제품은 아니나 「모델×하드」 성능의 핵심 계층).

| 표시 | 프로젝트 | 한 줄 | 링크 |
|---|---|---|---|
| ⭐ | **flashinfer-ai/flashinfer** | LLM Serving용 Attention / 샘플링 커널 라이브러리; 다중 엔진에 임베드 가능 | https://github.com/flashinfer-ai/flashinfer |
| ⭐ | **deepseek-ai/DeepGEMM** | DeepSeek OSS 고효율 GPU BLAS/GEMM 커널 라이브러리 | https://github.com/deepseek-ai/DeepGEMM |
| ⭐ | **deepseek-ai/DeepEP** | DeepSeek OSS Expert Parallel 통신 라이브러리; MoE 전용 | https://github.com/deepseek-ai/DeepEP |

---

## Contrast · 범용 Serving과의 경계

| 흔한 프로젝트 | 이 저장소 태도 | 설명 |
|---|---|---|
| vLLM / SGLang / TGI | 디렉터리 미수록 | **Ascend / Neuron / TPU / TT** 등 전용 플러그인 행만 |
| Ollama / llama.cpp | 기본 거절 | 크로스하드 휴대 runtime; 어떤 백엔드가 「칩 공식 경로」가 되면 별도 행 논의 가능 |
| Triton Inference Server | 제품 디렉터리 미수록 | 오케스트레이션/serving 껍질; 백엔드 엔진(TRT-LLM 등)은 위 표에 있음 |

---

## Related

- **자사 엔진:** [자사 · InferMatrixLab](#자사--infermatrixlab제3자-spec-아님) (조직 프로젝트, Spec 아님)
- InferMatrixLab의 다른 추론 엔지니어링 문서·비교(조직 내 후속 상호 링크)
- 범용 serving 선정은 별도 inference serving awesome / 엔지니어링 핸드북으로——이 저장소와 표를 섞지 말 것

---

## License

목록 내용은 **CC0 1.0** 정신으로 기여(항목 표 자유 재사용 허용). 링크된 프로젝트는 각자 라이선스 유지.
