# Awesome Model × Hardware Inference Engines

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

**Languages:** [English](README.en.md) · [中文](README.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Français](README.fr.md) · [Español](README.es.md)

> **モデル × ハードウェア専用推論エンジン精選** · specialized backends · not a general serving yellow pages  
> **モデル族 / アクセラレータに価値が紐づく**推論エンジンとプラグインのキュレーション一覧。汎用 LLM serving スタックの黄ページではありません。

**収録範囲：** 階層 / ハイブリッド CPU–GPU エキスパート・スケジューリング専用エンジン（Strata 方法族）；特定チップ / ランタイム向けのコンパイル型またはカーネル級推論エンジン；モデル族専用 runtime（例：DeepSeek 系）；ベンダー EP / バックエンドプラグイン（Ascend、Neuron、TPU、Tenstorrent…）；エッジ NPU LLM スタック；MoE / attention 専用カーネルライブラリ（「エンジン層」として独立引用できる場合）。  
**対象外：** vLLM / SGLang / TGI / Ollama などの**汎用 serving 全家桶の黄ページ**（行が明確に「某アクセラレータまたはモデル族の専用バックエンド / プラグイン」である場合のみ収録）；学習フレームワーク；純粋なベンチマーク表；OSS/ドキュメント実装のないマーケページ。

**印：** ⭐ 成熟 / 広く採用 · ☄️ 上昇中 / 要ウォッチ  
**構造：** Method Family × Hardware Domain  
**言語：** 日本語版；中国語主版は [README.md](README.md)。プロジェクト名とリンクは英語のまま。

### 専用エンジン ≠ 汎用 Serving（先に読む）

| 概念 | 何か | 本リポ？ |
|---|---|---|
| **専用エンジン** | チップ ISA / ベンダー runtime / モデル族向けにコンパイルまたは深くカスタムした推論経路 | ✅ 本リポ |
| **汎用 Serving** | 多モデル多 GPU 統一スケジューリング（vLLM、SGLang、TGI…） | ❌ 黄ページ不可；**ハード/モデル専用プラグイン行**のみ |
| **カーネルライブラリ** | 複数エンジンから呼べる演算子層（FlashAttention / DeepGEMM など） | ✅ 「Kernels / MoE」可 |
| **形式/変換ツール** | ONNX/GGUF エクスポートのみで推論 runtime なし | ❌ 原則不収（Core ML Tools の変換+デプロイ連鎖は例外可） |

---

## 貢献 / 収録ルール

- **⭐ Established：** ドキュメントが揃い；再現可能なビルド/実行経路；公開約 ≥ 6 か月または某チップスタックの事実上の標準。
- **☄️ Rising：** 直近 12 か月で活発；紐づくモデル族またはハードを説明できる；検証可能なリポ/ドキュメント。
- **必須：** 対象モデル/ハード、一言の問題定義、リンク、分区、⭐/☄️。
- **却下：** 汎用 serving の倉庫広告；ハード/モデル専用性なし；API ラッパのみ。
- PR 歓迎；分区が不明なら先に issue。

---

## 目次

- [Hardware · NVIDIA（TensorRT 系）](#hardware--nvidiatensorrt-系)
- [Hardware · Ascend / 国産 NPU](#hardware--ascend--国産-npu)
- [Hardware · AWS Inferentia / Trainium](#hardware--aws-inferentia--trainium)
- [Hardware · TPU](#hardware--tpu)
- [Hardware · Apple / Metal](#hardware--apple--metal)
- [Hardware · Intel OpenVINO / CPU·iGPU·NPU](#hardware--intel-openvino--cpuiGPUnpu)
- [Hardware · エッジ NPU / モバイル](#hardware--エッジ-npu--モバイル)
- [Hardware · その他アクセラレータプラグイン](#hardware--その他アクセラレータプラグイン)
- [Model · モデル族専用 Runtime](#model--モデル族専用-runtime)
- [Method · 階層 / 専用スケジューリング（Strata 系）](#method--階層--専用スケジューリングstrata-系)
- [自社 · InferMatrixLab（第三者 Spec ではない）](#自社--infermatrixlab第三者-spec-ではない)
- [Kernels · MoE / Attention 専用演算子](#kernels--moe--attention-専用演算子)
- [Contrast · 汎用 Serving との境界](#contrast--汎用-serving-との境界)
- [Related](#related)
- [License](#license)

---

## Hardware · NVIDIA（TensorRT 系）

NVIDIA GPU 向けの**コンパイル型 / ベンダー級** LLM およびグラフ最適化エンジン（「また一つの OpenAI 互換 server」ではない）。

| 印 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ⭐ | **NVIDIA/TensorRT-LLM** | NVIDIA 公式の LLM/VLM 推論エンジン：カスタム CUDA カーネル、エンジン構築、インフライトバッチ；NVIDIA GPU 向け | https://github.com/NVIDIA/TensorRT-LLM |
| ⭐ | **NVIDIA/TensorRT** | 汎用 NVIDIA 推論オプティマイザ & runtime；CV/拡散/独自ネットの専用エンジン構築入口 | https://github.com/NVIDIA/TensorRT |

---

## Hardware · Ascend / 国産 NPU

昇騰など NPU 上の専用バックエンドとプラグイン（汎用 vLLM 本体は非収録、Ascend 経路のみ）。

| 印 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ☄️ | **vllm-project/vllm-ascend** | vLLM の Ascend（昇騰）ハードウェアプラグイン；NPU 専用バックエンド（汎用一覧ではない） | https://github.com/vllm-project/vllm-ascend |

> MindIE / CANN 公式スタックは主にファーウェイ文書とファームウェア経路；安定した公開ミラーができたら ⭐ 行を追加。

---

## Hardware · AWS Inferentia / Trainium

| 印 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ☄️ | **aws-neuron/neuronx-distributed-inference** | NeuronX Distributed Inference（NxDI）：Inferentia/Trainium 上の分散 LLM 推論ライブラリ | https://github.com/aws-neuron/neuronx-distributed-inference |
| ☄️ | **vllm-project/vllm-neuron** | vLLM × Neuron プラグイン経路；Trainium/Inferentia 専用バックエンド | https://github.com/vllm-project/vllm-neuron |

---

## Hardware · TPU

| 印 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ☄️ | **vllm-project/tpu-inference** | vLLM の TPU 推論バックエンド（tpu-inference）；Google TPU 向け | https://github.com/vllm-project/tpu-inference |
| ☄️ | **huggingface/optimum-tpu** | Hugging Face Optimum TPU：TPU 上に Transformer をデプロイする専用経路 | https://github.com/huggingface/optimum-tpu |

---

## Hardware · Apple / Metal

| 印 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ⭐ | **ml-explore/mlx** | 公式スタイルの Apple Silicon 配列フレームワーク；Metal 上のモデル実行基盤 | https://github.com/ml-explore/mlx |
| ⭐ | **ml-explore/mlx-lm** | MLX ベースの LLM 推論・サービングツールチェーン；Apple Silicon 向け | https://github.com/ml-explore/mlx-lm |
| ⭐ | **apple/coremltools** | Core ML 変換・デプロイツールチェーン；iOS/macOS Neural Engine / GPU 経路 | https://github.com/apple/coremltools |

---

## Hardware · Intel OpenVINO / CPU·iGPU·NPU

| 印 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ⭐ | **openvinotoolkit/openvino.genai** | OpenVINO GenAI：Intel CPU/GPU/NPU 上の生成 AI 推論 runtime とパイプライン | https://github.com/openvinotoolkit/openvino.genai |

---

## Hardware · エッジ NPU / モバイル

| 印 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ☄️ | **airockchip/rknn-llm** | Rockchip RKNN-LLM：RK3588 などボード NPU 上の LLM 推論スタック | https://github.com/airockchip/rknn-llm |
| ☄️ | **hailo-ai/hailort** | HailoRT：Hailo エッジ AI アクセラレータ上の軽量高性能推論 runtime | https://github.com/hailo-ai/hailort |

---

## Hardware · その他アクセラレータプラグイン

| 印 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ☄️ | **tenstorrent/vllm-tt-plugin** | Tenstorrent の vLLM バックエンドプラグイン；TT-Metalium 演算子スタックと連携 | https://github.com/tenstorrent/vllm-tt-plugin |
| ☄️ | **tenstorrent/tt-metal** | TT-Metalium / TT-NN：Tenstorrent チップ上の演算子・カーネルプログラミングモデル | https://github.com/tenstorrent/tt-metal |

---

## Model · モデル族専用 Runtime

特定モデル構造（DeepSeek MoE、高圧縮量子化レイアウト、ハイブリッド専門家オフロードなど）向けに深くカスタムしたエンジン。

> あわせて下方の [Method · 階層 / 専用スケジューリング（Strata 系）](#method--階層--専用スケジューリングstrata-系) を参照。

| 印 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepInfer** | DeepSeek 本番推論フレームワークの OSS；DeepSeek-V4.1-Flash、NVIDIA SM100 / Ascend 950 向け | https://github.com/deepseek-ai/DeepInfer |
| ☄️ | **turboderp-org/exllamav3** | 現代のコンシューマ向け NVIDIA GPU 向け高速量子化 LLM 推論ライブラリ（ExLlama 系） | https://github.com/turboderp-org/exllamav3 |
| ⭐ | **kvcache-ai/ktransformers** | CPU/GPU 混在の MoE / 大規模モデル推論最適化；エキスパートオフロードとカーネル経路を重視 | https://github.com/kvcache-ai/ktransformers |

---

## Method · 階層 / 専用スケジューリング（Strata 系）

> **名称メモ：** 本リストで「Strata」は主に [Niko1221/Strata](https://github.com/Niko1221/Strata) を指す——特定の大規模 MoE（例: Qwen3.8-Flash-Next）向けに、**VRAM / システム RAM / SSD の階層**と**未キャッシュ専門家の CPU 並列計算**を行うコンシューマ PC 専用エンジン。同方法族には、より多くの MoE への一般化やホスト/SSD オフロード、CPU–GPU 協調も含む。同名リポジトリが複数ある場合は**下表のリンクと一文を優先**。

| 印 | プロジェクト | 一文 | リンク |
|---|---|---|---|
| ⭐ | **Niko1221/Strata** | Qwen3.8-Flash-Next 系向けコンシューマ専用エンジン：GPU に稠密/ホット専門家、RAM に全専門家をピン留めし CPU がミスを並列計算、SSD が n-gram；CUDA/HIP | https://github.com/Niko1221/Strata |
| ☄️ | **voidstackloop/extended-strata-moe** | Strata 式の非同期 GPU/CPU 専門家階層を llama.cpp 対応の多数 MoE に一般化（方法整合；初期リポジトリ） | https://github.com/voidstackloop/extended-strata-moe |
| ☄️ | **EfficientMoE/MoE-Infinity** | MoE 専門家をホストメモリ/SSD へオフロードし、活性化対応キャッシュとプリフェッチを備える推論ライブラリ＋サービング | https://github.com/EfficientMoE/MoE-Infinity |
| ☄️ | **efeslab/fiddler** | ICLR'25：ローカル機器向け MoE の CPU–GPU 協調（欠落専門家は重み転送ではなく CPU 計算） | https://github.com/efeslab/fiddler |

---

## 自社 · InferMatrixLab（第三者 Spec ではない）

> **境界（必読）：** 以下は組織 **InferMatrixLab** が保守するモデル/ハードウェア**専用**推論エンジンとレシピ入口。組織内相互リンクと透明性のための掲載。**第三者の業界 Spec ではない**。「公式標準」や Hardware/Model 区のベンダー権威行として引用してはならない。上記の第三者キュレーションと**分表**。

| 印 | プロジェクト | 一文 | リンク |
|---|---|---|---|
| ☄️ | **InferMatrixLab/system1-omni** | System1 モデル族向けコミュニティ保守の高性能推論エンジン（Rust；vLLM / vLLM-Omni スタイル） | https://github.com/InferMatrixLab/system1-omni |
| ☄️ | **InferMatrixLab/vllm-rlt** | looped transformer 向け推論エンジン：loop レベル・スケジューリングと合成可能な段階実行 | https://github.com/InferMatrixLab/vllm-rlt |
| ☄️ | **InferMatrixLab/minicpm-o-4.5-single-gpu-engine** | MiniCPM-o 4.5 向け単一 GPU ストリーミング音声専用エンジン（vLLM-Omni / SGLang-Omni と比較可） | https://github.com/InferMatrixLab/minicpm-o-4.5-single-gpu-engine |
| ☄️ | **InferMatrixLab/vllm-omni-mlx** | Apple Silicon 上の全モダリティ推論サーバ（OpenAI / Anthropic 互換 API） | https://github.com/InferMatrixLab/vllm-omni-mlx |
| ☄️ | **InferMatrixLab/qwen3-tts-rsi-npu-engine** | Ascend NPU（例: 910B）上の Qwen3-TTS 独立高速推論エンジン（RSI 経路） | https://github.com/InferMatrixLab/qwen3-tts-rsi-npu-engine |
| ☄️ | **InferMatrixLab/drama-3-single-b300-engine** | Fish Audio Drama 3 向け単一 NVIDIA B300 ストリーミング TTS 専用エンジン | https://github.com/InferMatrixLab/drama-3-single-b300-engine |
| ☄️ | **InferMatrixLab/recipe** | 「モデル × エンジン × ハードウェア」のコミュニティ推論レシピ目録（汎用 serving 黄頁ではない） | https://github.com/InferMatrixLab/recipe |

---

## Kernels · MoE / Attention 専用演算子

上位エンジンが組み合わせる**専用カーネルライブラリ**（完全な serving 製品ではないが、「モデル×ハード」性能のコア層）。

| 印 | プロジェクト | 一言 | リンク |
|---|---|---|---|
| ⭐ | **flashinfer-ai/flashinfer** | LLM Serving 向け Attention / サンプリング等カーネルライブラリ；複数エンジンに組み込み可能 | https://github.com/flashinfer-ai/flashinfer |
| ⭐ | **deepseek-ai/DeepGEMM** | DeepSeek OSS の高効率 GPU BLAS/GEMM カーネルライブラリ | https://github.com/deepseek-ai/DeepGEMM |
| ⭐ | **deepseek-ai/DeepEP** | DeepSeek OSS の Expert Parallel 通信ライブラリ；MoE 専用 | https://github.com/deepseek-ai/DeepEP |

---

## Contrast · 汎用 Serving との境界

| よくあるプロジェクト | 本リポの態度 | 説明 |
|---|---|---|
| vLLM / SGLang / TGI | 黄ページ不可 | **Ascend / Neuron / TPU / TT** など専用プラグイン行のみ |
| Ollama / llama.cpp | 原則不収 | クロスハード便携 runtime；某バックエンドが「チップ公式経路」になったら別行で議論可 |
| Triton Inference Server | 製品黄ページ不可 | オーケストレーション/serving 外壳；バックエンドエンジン（TRT-LLM 等）は上表にあり |

---

## Related

- **自社エンジン：** [自社 · InferMatrixLab](#自社--infermatrixlab第三者-spec-ではない)（組織プロジェクト、Spec ではない）
- InferMatrixLab の他の推論エンジニアリング文書と比較（組織内で後続相互リンク）
- 汎用 serving 選定は別の inference serving awesome / エンジニアリングハンドブックへ——本リポと表を混ぜない

---

## License

本リスト内容は **CC0 1.0** の精神で貢献（エントリ表の自由な再利用を許容）。リンク先プロジェクトは各自のライセンスを保持。
