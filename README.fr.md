# Awesome Model × Hardware Inference Engines

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

**Languages:** [English](README.en.md) · [中文](README.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Français](README.fr.md) · [Español](README.es.md)

> **Moteurs d'inférence spécialisés modèle × matériel** · specialized backends · not a general serving yellow pages  
> Liste curatée de **moteurs d'inférence spécialisés modèle/matériel** — moteurs et plugins dont la valeur est liée à une **famille de modèles** et/ou un **accélérateur**, pas des stacks de serving LLM génériques.

**Dans le périmètre :** moteurs spécialisés à ordonnancement d’experts stratifié / hybride CPU–GPU（famille de méthodes Strata）；moteurs d'inférence compile-time ou au niveau kernel pour puces / runtimes spécifiques ; runtimes spécialisés par famille de modèles (ex. classe DeepSeek) ; plugins EP / backend vendeur (Ascend, Neuron, TPU, Tenstorrent…) ; stacks LLM NPU edge ; bibliothèques de kernels MoE / attention (citables comme « couche moteur »).  
**Hors périmètre :** pages jaunes de megapacks serving génériques (vLLM / SGLang / TGI / Ollama) — n'inclure une ligne que si c'est clairement un **backend / plugin spécifique accélérateur ou famille de modèles** ; frameworks d'entraînement ; tableaux de benchmarks purs ; pages marketing sans implémentation OSS/docs.

**Marques :** ⭐ Établi / largement adopté · ☄️ En hausse / à surveiller  
**Structure :** Method Family × Hardware Domain  
**Langues :** édition française ; le chinois est la version principale dans [README.md](README.md). Noms de projets et liens restent en anglais.

### Moteur spécialisé ≠ Serving générique (lire d'abord)

| Concept | Qu'est-ce que c'est | Ce dépôt ? |
|---|---|---|
| **Moteur spécialisé** | Chemin d'inférence compilé ou profondément custom pour une ISA de puce / runtime vendeur / famille de modèles | ✅ Ici |
| **Serving générique** | Stack d'ordonnancement multi-modèles multi-GPU (vLLM, SGLang, TGI…) | ❌ Pas de pages jaunes ; seulement leurs **lignes de plugins hard/modèle** |
| **Bibliothèque de kernels** | Couche d'opérateurs appelable par plusieurs moteurs (FlashAttention / DeepGEMM…) | ✅ OK dans « Kernels / MoE » |
| **Outils format / conversion** | Export ONNX/GGUF seul, sans runtime d'inférence | ❌ En général non (chaîne Core ML Tools conversion+déploiement possible) |

---

## Règles de contribution

- **⭐ Established :** docs solides ; chemin build/run reproductible ; public ~≥ 6 mois ou standard de fait pour une stack de puce.
- **☄️ Rising :** actif sur les 12 derniers mois ; peut nommer la famille de modèles ou le matériel lié ; lien repo/docs vérifiable.
- **Requis :** quel modèle/matériel, définition du problème en une phrase, lien, section, ⭐/☄️.
- **Rejet :** pubs de dépôt serving générique entier ; pas de spécialisation hard/modèle ; wrappers API seuls.
- PR bienvenues ; ouvrir une issue d'abord si la section est floue.

---

## Table des matières

- [Hardware · NVIDIA (famille TensorRT)](#hardware--nvidia-famille-tensorrt)
- [Hardware · Ascend / NPU domestique](#hardware--ascend--npu-domestique)
- [Hardware · AWS Inferentia / Trainium](#hardware--aws-inferentia--trainium)
- [Hardware · TPU](#hardware--tpu)
- [Hardware · Apple / Metal](#hardware--apple--metal)
- [Hardware · Intel OpenVINO / CPU·iGPU·NPU](#hardware--intel-openvino--cpuiGPUnpu)
- [Hardware · NPU edge / mobile](#hardware--npu-edge--mobile)
- [Hardware · Autres plugins accélérateurs](#hardware--autres-plugins-accélérateurs)
- [Model · Runtime spécialisé famille de modèles](#model--runtime-spécialisé-famille-de-modèles)
- [Method · Ordonnancement stratifié / spécialisé（classe Strata）](#method--ordonnancement-stratifié--spécialiséclasse-strata)
- [Propre · InferMatrixLab（pas une Spec tierce）](#propre--infermatrixlabpas-une-spec-tierce)
- [Kernels · Ops spécialisées MoE / Attention](#kernels--ops-spécialisées-moe--attention)
- [Contrast · Frontière vs Serving générique](#contrast--frontière-vs-serving-générique)
- [Related](#related)
- [License](#license)

---

## Hardware · NVIDIA (famille TensorRT)

Moteurs LLM et d'optimisation de graphes **compile-time / grade vendeur** pour GPU NVIDIA (pas « encore un serveur compatible OpenAI »).

| Marque | Projet | En une phrase | Lien |
|---|---|---|---|
| ⭐ | **NVIDIA/TensorRT-LLM** | Moteur d'inférence LLM/VLM officiel NVIDIA : kernels CUDA custom, build d'engine, batching in-flight ; lié aux GPU NVIDIA | https://github.com/NVIDIA/TensorRT-LLM |
| ⭐ | **NVIDIA/TensorRT** | Optimiseur & runtime d'inférence NVIDIA général ; point d'entrée pour de nombreux moteurs CV/diffusion/réseaux custom | https://github.com/NVIDIA/TensorRT |

---

## Hardware · Ascend / NPU domestique

Backends et plugins spécialisés sur Ascend et NPU similaires (le cœur vLLM générique n'est pas listé — seulement les chemins Ascend).

| Marque | Projet | En une phrase | Lien |
|---|---|---|---|
| ☄️ | **vllm-project/vllm-ascend** | Plugin matériel Ascend (昇腾) pour vLLM ; backend NPU dédié, pas une page jaune générique | https://github.com/vllm-project/vllm-ascend |

> Les stacks officielles MindIE / CANN passent surtout par la doc et le firmware Huawei ; ajouter une ligne ⭐ dès qu'un miroir public stable existe.

---

## Hardware · AWS Inferentia / Trainium

| Marque | Projet | En une phrase | Lien |
|---|---|---|---|
| ☄️ | **aws-neuron/neuronx-distributed-inference** | NeuronX Distributed Inference (NxDI) : inférence LLM distribuée sur Inferentia/Trainium | https://github.com/aws-neuron/neuronx-distributed-inference |
| ☄️ | **vllm-project/vllm-neuron** | Chemin plugin vLLM × Neuron ; backend dédié Trainium/Inferentia | https://github.com/vllm-project/vllm-neuron |

---

## Hardware · TPU

| Marque | Projet | En une phrase | Lien |
|---|---|---|---|
| ☄️ | **vllm-project/tpu-inference** | Backend d'inférence TPU de vLLM (tpu-inference) ; lié aux TPU Google | https://github.com/vllm-project/tpu-inference |
| ☄️ | **huggingface/optimum-tpu** | Hugging Face Optimum TPU : chemin dédié pour déployer des Transformers sur TPU | https://github.com/huggingface/optimum-tpu |

---

## Hardware · Apple / Metal

| Marque | Projet | En une phrase | Lien |
|---|---|---|---|
| ⭐ | **ml-explore/mlx** | Framework de tableaux style officiel pour Apple Silicon ; substrat d'exécution modèle sur Metal | https://github.com/ml-explore/mlx |
| ⭐ | **ml-explore/mlx-lm** | Chaîne d'outils d'inférence & serving LLM sur MLX ; liée à Apple Silicon | https://github.com/ml-explore/mlx-lm |
| ⭐ | **apple/coremltools** | Chaîne de conversion & déploiement Core ML ; chemin Neural Engine / GPU iOS/macOS | https://github.com/apple/coremltools |

---

## Hardware · Intel OpenVINO / CPU·iGPU·NPU

| Marque | Projet | En une phrase | Lien |
|---|---|---|---|
| ⭐ | **openvinotoolkit/openvino.genai** | OpenVINO GenAI : runtime & pipelines d'IA générative sur CPU/GPU/NPU Intel | https://github.com/openvinotoolkit/openvino.genai |

---

## Hardware · NPU edge / mobile

| Marque | Projet | En une phrase | Lien |
|---|---|---|---|
| ☄️ | **airockchip/rknn-llm** | Rockchip RKNN-LLM : stack d'inférence LLM sur NPU embarqués (ex. RK3588) | https://github.com/airockchip/rknn-llm |
| ☄️ | **hailo-ai/hailort** | HailoRT : runtime d'inférence léger haute perf. sur accélérateurs edge Hailo | https://github.com/hailo-ai/hailort |

---

## Hardware · Autres plugins accélérateurs

| Marque | Projet | En une phrase | Lien |
|---|---|---|---|
| ☄️ | **tenstorrent/vllm-tt-plugin** | Plugin backend vLLM Tenstorrent ; s'appuie sur la stack d'opérateurs TT-Metalium | https://github.com/tenstorrent/vllm-tt-plugin |
| ☄️ | **tenstorrent/tt-metal** | TT-Metalium / TT-NN : modèle de programmation opérateurs & kernels sur puces Tenstorrent | https://github.com/tenstorrent/tt-metal |

---

## Model · Runtime spécialisé famille de modèles

Moteurs profondément custom pour des structures de modèles spécifiques (DeepSeek MoE, layouts quantifiés haute compression, offload d'experts hybride, etc.).

> Voir aussi [Method · Ordonnancement stratifié / spécialisé（classe Strata）](#method--ordonnancement-stratifié--spécialiséclasse-strata) plus bas.

| Marque | Projet | En une phrase | Lien |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepInfer** | Framework d'inférence production DeepSeek (OSS) ; lié à DeepSeek-V4.1-Flash sur NVIDIA SM100 / Ascend 950 | https://github.com/deepseek-ai/DeepInfer |
| ☄️ | **turboderp-org/exllamav3** | Inférence LLM quantifiée haute vitesse pour GPU NVIDIA grand public modernes (ligne ExLlama) | https://github.com/turboderp-org/exllamav3 |
| ⭐ | **kvcache-ai/ktransformers** | Framework d'inférence MoE / grands modèles hybride CPU/GPU ; offload d'experts & chemins kernels | https://github.com/kvcache-ai/ktransformers |

---

## Method · Ordonnancement stratifié / spécialisé（classe Strata）

> **Note de nommage :** Ici, « Strata » désigne surtout [Niko1221/Strata](https://github.com/Niko1221/Strata) — un moteur **spécialisé modèle** pour grands MoE（ex. Qwen3.8-Flash-Next）sur PC grand public, avec **tiers VRAM / RAM système / SSD** et **CPU calculant en parallèle les experts non mis en cache**. La même famille de méthodes couvre les généralisations à d’autres MoE, l’offload hôte/SSD et l’orchestration CPU–GPU. En cas d’homonymes, **les liens et une-lignes ci-dessous font foi**.

| Marque | Projet | Une ligne | Lien |
|---|---|---|---|
| ⭐ | **Niko1221/Strata** | Moteur grand public pour MoE type Qwen3.8-Flash-Next : experts denses/chauds sur GPU, tous les experts épinglés en RAM avec calcul CPU parallèle des ratés, n-gram sur SSD ; CUDA/HIP | https://github.com/Niko1221/Strata |
| ☄️ | **voidstackloop/extended-strata-moe** | Généralise le tiering async GPU/CPU style Strata à de nombreuses architectures MoE llama.cpp (aligné méthode ; dépôt encore jeune) | https://github.com/voidstackloop/extended-strata-moe |
| ☄️ | **EfficientMoE/MoE-Infinity** | Offload d’experts MoE vers mémoire hôte/SSD + cache et prefetch sensibles à l’activation ; bibliothèque + chemin de service | https://github.com/EfficientMoE/MoE-Infinity |
| ☄️ | **efeslab/fiddler** | ICLR'25 : orchestration CPU–GPU pour MoE local (experts manquants calculés sur CPU plutôt que transfert de poids) | https://github.com/efeslab/fiddler |

---

## Propre · InferMatrixLab（pas une Spec tierce）

> **Frontière（obligatoire）:** Lignes ci-dessous = moteurs et recettes **spécialisés** modèle/matériel maintenus par **InferMatrixLab**, pour liens internes et transparence. **Ce n’est pas** une Spec industrielle tierce et **ne doit pas** être cité comme « norme officielle » ni comme ligne d’autorité Hardware/Model. **Séparé** des lignes tierces ci-dessus.

| Marque | Projet | Une ligne | Lien |
|---|---|---|---|
| ☄️ | **InferMatrixLab/system1-omni** | Moteur d’inférence haute perf. maintenu par la communauté pour la famille System1 (Rust ; style vLLM / vLLM-Omni) | https://github.com/InferMatrixLab/system1-omni |
| ☄️ | **InferMatrixLab/vllm-rlt** | Moteur pour transformers bouclés : ordonnancement au niveau loop et étapes composables | https://github.com/InferMatrixLab/vllm-rlt |
| ☄️ | **InferMatrixLab/minicpm-o-4.5-single-gpu-engine** | Moteur vocal streaming mono-GPU spécialisé MiniCPM-o 4.5 (comparable à vLLM-Omni / SGLang-Omni) | https://github.com/InferMatrixLab/minicpm-o-4.5-single-gpu-engine |
| ☄️ | **InferMatrixLab/vllm-omni-mlx** | Serveur d’inférence omni-modalité sur Apple Silicon (API compatible OpenAI / Anthropic) | https://github.com/InferMatrixLab/vllm-omni-mlx |
| ☄️ | **InferMatrixLab/qwen3-tts-rsi-npu-engine** | Inférence Qwen3-TTS autonome rapide sur NPU Ascend (ex. 910B) via chemin RSI | https://github.com/InferMatrixLab/qwen3-tts-rsi-npu-engine |
| ☄️ | **InferMatrixLab/drama-3-single-b300-engine** | Moteur TTS streaming spécialisé Fish Audio Drama 3 sur un seul NVIDIA B300 | https://github.com/InferMatrixLab/drama-3-single-b300-engine |
| ☄️ | **InferMatrixLab/recipe** | Catalogue communautaire de recettes « modèle × moteur × matériel » (pas un annuaire serving générique) | https://github.com/InferMatrixLab/recipe |

---

## Kernels · Ops spécialisées MoE / Attention

**Bibliothèques de kernels spécialisées** composables par les moteurs amont (pas des produits serving complets, mais la couche de perf « modèle×matériel »).

| Marque | Projet | En une phrase | Lien |
|---|---|---|---|
| ⭐ | **flashinfer-ai/flashinfer** | Bibliothèque de kernels Attention / sampling pour LLM serving ; intégrable par plusieurs moteurs | https://github.com/flashinfer-ai/flashinfer |
| ⭐ | **deepseek-ai/DeepGEMM** | Bibliothèque de kernels GPU BLAS/GEMM haute efficacité (OSS DeepSeek) | https://github.com/deepseek-ai/DeepGEMM |
| ⭐ | **deepseek-ai/DeepEP** | Bibliothèque de communication Expert Parallel (OSS DeepSeek) ; spécifique MoE | https://github.com/deepseek-ai/DeepEP |

---

## Contrast · Frontière vs Serving générique

| Projet courant | Position ici | Note |
|---|---|---|
| vLLM / SGLang / TGI | Pas de pages jaunes | Seulement leurs lignes de plugins **Ascend / Neuron / TPU / TT** |
| Ollama / llama.cpp | Rejet par défaut | Runtime portable cross-hardware ; discuter une ligne séparée si un backend devient « chemin officiel de puce » |
| Triton Inference Server | Pas de pages jaunes produit | Coque d'orchestration/serving ; moteurs backend (TRT-LLM etc.) déjà listés ci-dessus |

---

## Related

- **Moteurs propres :** voir [Propre · InferMatrixLab](#propre--infermatrixlabpas-une-spec-tierce)（projets org, pas Spec）
- Autres docs et comparaisons d'ingénierie d'inférence InferMatrixLab (liens croisés dans l'org plus tard)
- Pour le choix de serving générique, utiliser un awesome / manuel séparé — ne pas mélanger les tableaux avec ce dépôt

---

## License

Le contenu de la liste est contribué dans l'esprit **CC0 1.0** (réutilisation libre des tableaux d'entrées). Les projets liés gardent leurs propres licences.
