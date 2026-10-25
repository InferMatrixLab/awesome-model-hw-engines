# Awesome Model × Hardware Inference Engines

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

**Languages:** [English](README.en.md) · [中文](README.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Français](README.fr.md) · [Español](README.es.md)

> **モデル × ハードウェア専用推論エンジン精選** · specialized backends · not a general serving yellow pages  
> **モデル系統 / アクセラレータ** に価値が結びつくエンジンとプラグインの精選リスト（汎用 LLM サービング黄頁ではない）。

**対象（In）：** **モデルカテゴリ** で整理し、次に **ハードウェア** で細分する専用推論エンジンとプラグイン；階層 / ハイブリッド CPU–GPU エキスパートスケジューリング（Strata 手法族）；モデル族 runtime；ベンダー EP / バックエンドプラグイン；エッジ NPU；引用可能な MoE / Attention カーネル。  
**対象外（Out）：** vLLM / SGLang / TGI / Ollama 等の**汎用サービング黄頁**（明確にハードウェア / モデル族専用バックエンド / プラグインの行のみ収録）；学習フレームワーク；純ベンチ；実装なきマーケ頁。

**標記：** ⭐ 確立 / 広く採用 · ☄️ 上昇中 / 注目 · **自社** = InferMatrixLab 保守（第三者 Spec ではない）  
**構造：** **L1 = モデルカテゴリ** → **L2 = ハードウェア**（NVIDIA / Ascend / Neuron-Trainium / TPU / Apple-Metal / Intel / Edge-NPU / CPU-RAM-SSD tier / Cross-vendor kernels；未掲載チップは Other accelerators）  
**言語：** 日本語版；主版は [中文 README.md](README.md)。プロジェクト名とリンクは英語のまま。

### 専用エンジン ≠ 汎用 Serving（先に読む）

| 概念 | 何か | 本リポ？ |
|---|---|---|
| **専用エンジン** | チップ ISA / ベンダー runtime / モデル族向けにコンパイルまたは深くカスタムした推論経路 | ✅ 本リポ |
| **汎用 Serving** | 多モデル多 GPU 統一スケジューリング（vLLM、SGLang、TGI…） | ❌ 黄頁なし；**ハード/モデル専用プラグイン行のみ** |
| **カーネルライブラリ** | 多エンジンから呼べる演算子層 | ✅ 対応モデル類 → Cross-vendor kernels |
| **形式 / 変換ツール** | ONNX/GGUF エクスポートのみで推論 runtime なし | ❌ 原則却下（Core ML Tools 等は例外可） |

---

## 貢献ルール

- **⭐ Established：** 十分なドキュメント；再現可能なビルド/実行；公開約 ≥ 6 か月またはチップスタックの事実上標準。
- **☄️ Rising：** 直近 12 か月活発；紐づくモデル族またはハードを説明可能；検証可能なリンク。
- **必須：** モデルカテゴリ、ハードウェア、一言の問題定義、リンク、⭐/☄️；自社行は明示。
- **却下：** 汎用サービングの丸ごと広告；専用性なし；API ラッパのみ。
- PR 歓迎；区分が不明なら先に issue。

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
- [自社索引 · InferMatrixLab（第三者 Spec ではない）](#自社索引--infermatrixlab第三者-spec-ではない)]
- [Contrast · Boundary vs generic Serving](#contrast--boundary-vs-generic-serving)
- [Related](#related)
- [License](#license)

---

## Dense LLM

密な Transformer / デコーダ LLM（非 MoE 主体）向けの専用エンジンとハードウェアバックエンド。

### NVIDIA

| 標記 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ⭐ | **NVIDIA/TensorRT-LLM** | NVIDIA 公式 LLM/VLM 推論エンジン：独自 CUDA カーネル、エンジン構築、IB バッチ；NVIDIA GPU 向け | https://github.com/NVIDIA/TensorRT-LLM |
| ☄️ | **turboderp-org/exllamav3** | 現代のコンシューマ向け NVIDIA GPU 向け高速量子化 LLM 推論ライブラリ（ExLlama 系） | https://github.com/turboderp-org/exllamav3 |

### NVIDIA · RTX / Blackwell (SM120)

| 標記 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ☄️ | **NVIDIA/flare-local-inference** | ローカル Agent 推論：PyTorch 構築 + Rust サーブ；完全な対話状態（KV + 再帰）；NVIDIA SM120/SM121；研究プロトタイプ（vLLM の代替ではない） | https://github.com/NVIDIA/flare-local-inference |

### Ascend

| 標記 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ☄️ | **vllm-project/vllm-ascend** | vLLM の Ascend（昇騰）ハードウェアプラグイン；NPU 専用バックエンド | https://github.com/vllm-project/vllm-ascend |

> MindIE / CANN 公式スタックは主に Huawei ドキュメントとファームウェア経路；安定公開ミラー後に ⭐ 行を追加。

### Neuron-Trainium

| 標記 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ☄️ | **aws-neuron/neuronx-distributed-inference** | NeuronX Distributed Inference（NxDI）：Inferentia/Trainium 上の分散 LLM 推論 | https://github.com/aws-neuron/neuronx-distributed-inference |
| ☄️ | **vllm-project/vllm-neuron** | vLLM × Neuron プラグイン；Trainium/Inferentia 専用バックエンド | https://github.com/vllm-project/vllm-neuron |

### TPU

| 標記 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ☄️ | **vllm-project/tpu-inference** | vLLM の TPU 推論バックエンド；Google TPU 向け | https://github.com/vllm-project/tpu-inference |
| ☄️ | **huggingface/optimum-tpu** | Hugging Face Optimum TPU：TPU 上へ Transformer をデプロイする専用経路 | https://github.com/huggingface/optimum-tpu |

### Apple-Metal

| 標記 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ⭐ | **ml-explore/mlx** | Apple Silicon 配列フレームワーク；Metal 上のモデル実行基盤 | https://github.com/ml-explore/mlx |
| ⭐ | **ml-explore/mlx-lm** | MLX 上の LLM 推論・サービングツールチェーン；Apple Silicon 向け | https://github.com/ml-explore/mlx-lm |
| ⭐ | **apple/coremltools** | Core ML 変換・デプロイツールチェーン；iOS/macOS Neural Engine / GPU 経路 | https://github.com/apple/coremltools |

### Intel

| 標記 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ⭐ | **openvinotoolkit/openvino.genai** | OpenVINO GenAI：Intel CPU/GPU/NPU 上の生成 AI 推論ランタイムとパイプライン | https://github.com/openvinotoolkit/openvino.genai |

### Edge-NPU

| 標記 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ☄️ | **airockchip/rknn-llm** | Rockchip RKNN-LLM：RK3588 等ボード NPU 上の LLM 推論スタック | https://github.com/airockchip/rknn-llm |
| ☄️ | **hailo-ai/hailort** | HailoRT：Hailo エッジ AI アクセラレータ上の軽量高性能推論 runtime | https://github.com/hailo-ai/hailort |

### Other accelerators

| 標記 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ☄️ | **tenstorrent/vllm-tt-plugin** | Tenstorrent の vLLM バックエンドプラグイン；TT-Metalium 演算子スタックと連携 | https://github.com/tenstorrent/vllm-tt-plugin |
| ☄️ | **tenstorrent/tt-metal** | TT-Metalium / TT-NN：Tenstorrent チップ上の演算子・カーネル・プログラミングモデル | https://github.com/tenstorrent/tt-metal |

### Cross-vendor kernels

| 標記 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ⭐ | **flashinfer-ai/flashinfer** | LLM Serving 向け Attention / サンプリング等カーネルライブラリ；多エンジン組込み可 | https://github.com/flashinfer-ai/flashinfer |

---

## MoE

Mixture-of-Experts 専用：エキスパート並列、オフロード、階層スケジューリング、MoE カーネル。

### NVIDIA

| 標記 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepInfer** | DeepSeek 本番推論フレームワーク OSS；DeepSeek-V4.1-Flash、NVIDIA SM100 / Ascend 950 | https://github.com/deepseek-ai/DeepInfer |

### Ascend

| 標記 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepInfer** | 同上；Ascend 950 経路（NVIDIA SM100 と二重ハードウェア） | https://github.com/deepseek-ai/DeepInfer |

### CPU-RAM-SSD tier

> **Strata 系：** 本リストで「Strata」は主に [Niko1221/Strata](https://github.com/Niko1221/Strata) を指す — 大規模 MoE（例：Qwen3.8-Flash-Next）向けコンシューマ PC 専用エンジンで **VRAM / システム RAM / SSD 階層** と **未キャッシュエキスパートの CPU 並列計算**。同手法族には他 MoE への一般化やホスト/SSD オフロード、CPU–GPU 協調も含む。同名の別リポジトリがある場合は **下表のリンクと一言を正とする**。

| 標記 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ⭐ | **Niko1221/Strata** | Qwen3.8-Flash-Next 級 MoE 向け：GPU に密/ホットエキスパート、RAM に全エキスパート固定＋CPU 並列、SSD n-gram；CUDA/HIP | https://github.com/Niko1221/Strata |
| ☄️ | **voidstackloop/extended-strata-moe** | Strata 式非同期 GPU/CPU エキスパート階層を llama.cpp 対応多アーキ MoE へ一般化（手法整合；早期） | https://github.com/voidstackloop/extended-strata-moe |
| ☄️ | **EfficientMoE/MoE-Infinity** | MoE エキスパートをホストメモリ/SSD へオフロード＋活性化アウェアキャッシュ/プリフェッチ | https://github.com/EfficientMoE/MoE-Infinity |
| ☄️ | **efeslab/fiddler** | ICLR'25：ローカル MoE の CPU–GPU 協調（欠落エキスパートを CPU で計算し重み移送を避ける） | https://github.com/efeslab/fiddler |
| ⭐ | **kvcache-ai/ktransformers** | ハイブリッド CPU/GPU の MoE / 大規模モデル推論最適化；エキスパートオフロードとカーネル経路 | https://github.com/kvcache-ai/ktransformers |
| ⭐ | **Tiiny-AI/PowerInfer** | コンシューマ GPU+CPU ハイブリッド：活性化 locality（ホット/コールドニューロン）；PowerInfer-2 で端末 Mixtral；旧 SJTU-IPADS | https://github.com/Tiiny-AI/PowerInfer |

### Cross-vendor kernels

| 標記 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepGEMM** | DeepSeek OSS 高効率 GPU BLAS/GEMM カーネルライブラリ | https://github.com/deepseek-ai/DeepGEMM |
| ⭐ | **deepseek-ai/DeepEP** | DeepSeek OSS Expert Parallel 通信ライブラリ；MoE 専用 | https://github.com/deepseek-ai/DeepEP |

---

## Multimodal / Omni

マルチモーダル / Omni（音声·視覚·テキスト）モデル族向け専用エンジン。

### NVIDIA

| 標記 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ☄️ · 自社 | **InferMatrixLab/system1-omni** | System1 モデル族向けコミュニティ保守型高性能推論エンジン（Rust；vLLM / vLLM-Omni 系） | https://github.com/InferMatrixLab/system1-omni |
| ☄️ · 自社 | **InferMatrixLab/minicpm-o-4.5-single-gpu-engine** | MiniCPM-o 4.5 単一 GPU ストリーミング音声専用エンジン | https://github.com/InferMatrixLab/minicpm-o-4.5-single-gpu-engine |

### Apple-Metal

| 標記 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ☄️ · 自社 | **InferMatrixLab/vllm-omni-mlx** | Apple Silicon 上の全モーダル推論サーバ（OpenAI / Anthropic 互換 API） | https://github.com/InferMatrixLab/vllm-omni-mlx |

---

## Diffusion · Image

画像拡散 / 画像生成向け専用またはコンパイル型エンジン経路。

### NVIDIA

| 標記 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ⭐ | **NVIDIA/TensorRT** | 汎用 NVIDIA 推論オプティマイザ & runtime；多数の CV/拡散/カスタムネット専用エンジン入口 | https://github.com/NVIDIA/TensorRT |

---

## Diffusion · Video

動画拡散 / 動画生成専用エンジン。

> 検証済み行はまだなし；モデルカテゴリ → ハードウェアで PR 歓迎。

---

## Speech · TTS / ASR

音声合成 / 認識モデル族専用エンジン。

### NVIDIA

| 標記 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ☄️ · 自社 | **InferMatrixLab/drama-3-single-b300-engine** | Fish Audio Drama 3 向け単一 NVIDIA B300 ストリーミング TTS 専用エンジン | https://github.com/InferMatrixLab/drama-3-single-b300-engine |

### Ascend

| 標記 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ☄️ · 自社 | **InferMatrixLab/qwen3-tts-rsi-npu-engine** | Ascend NPU（例：910B）上の独立高速 Qwen3-TTS 推論（RSI 経路） | https://github.com/InferMatrixLab/qwen3-tts-rsi-npu-engine |

---

## Embedding / Rerank

埋め込み / リランクモデル専用推論経路。

> 検証済み行はまだなし；モデルカテゴリ → ハードウェアで PR 歓迎。

---

## Other

上記大類に収まらないが、なおモデル×ハードウェア専用のエンジンとレシピ入口。

### NVIDIA

| 標記 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ☄️ · 自社 | **InferMatrixLab/vllm-rlt** | looped transformer 向け推論エンジン：loop 級スケジューリングと合成可能ステージ | https://github.com/InferMatrixLab/vllm-rlt |

### Catalogs

| 標記 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ☄️ · 自社 | **InferMatrixLab/recipe** | 「モデル × エンジン × ハードウェア」推論レシピのコミュニティ目録 | https://github.com/InferMatrixLab/recipe |


---

## 自社索引 · InferMatrixLab（第三者 Spec ではない）

> **境界（必読）：** 下記は **InferMatrixLab** 保守の専用エンジンとレシピで、上表に既に配置（「自社」標記）。**第三者業界 Spec ではない**。透明性のための索引のみ。

| プロジェクト | 配置先 | リンク |
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

| よくあるプロジェクト | 本リポの立場 | 説明 |
|---|---|---|
| vLLM / SGLang / TGI | 黄頁なし | **Ascend / Neuron / TPU / TT** 等の専用プラグイン行のみ（モデル類 × ハード下） |
| Ollama / llama.cpp | 原則却下 | クロスハード可搬 runtime；チップ公式経路になったバックエンドは別行で議論可 |
| Triton Inference Server | 製品黄頁なし | オーケストレーション外壳；バックエンド（TRT-LLM 等）はモデル×ハードで既掲 |

---

## Related

- **自社索引：** [自社索引 · InferMatrixLab](#自社索引--infermatrixlab第三者-spec-ではない)
- InferMatrixLab の他推論ドキュメント（組織内で後日相互リンク）
- 汎用サービング選定は別の inference-serving awesome / ハンドブックへ——本リポと表を混ぜない

---

## License

リスト内容は **CC0 1.0** の精神で貢献（エントリ表の自由再利用可）。リンク先プロジェクトは各ライセンスを保持。