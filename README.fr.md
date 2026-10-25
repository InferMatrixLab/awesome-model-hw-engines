# Awesome Model × Hardware Inference Engines

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

**Languages:** [English](README.en.md) · [中文](README.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Français](README.fr.md) · [Español](README.es.md)

> **Moteurs d’inférence spécialisés modèle × matériel** · specialized backends · pas un annuaire serving générique  
> Liste curatée d’**engines et plugins** dont la valeur est liée à une **famille de modèles** et/ou un **accélérateur**.

**Dans le périmètre :** engines/plugins organisés par **catégorie de modèle**, puis par **matériel** ; ordonnancement d’experts stratifié / hybride CPU–GPU (famille Strata) ; runtimes de famille de modèles ; plugins EP / backends vendeur ; stacks NPU edge ; bibliothèques de kernels MoE / Attention citables.  
**Hors périmètre :** annuaires serving génériques vLLM / SGLang / TGI / Ollama (n’inclure une ligne que si c’est clairement un **backend / plugin** lié à un accélérateur ou une famille de modèles) ; frameworks d’entraînement ; purs benchmarks ; pages marketing sans OSS/docs.

**Marqueurs :** ⭐ Établi / largement adopté · ☄️ En hausse / à suivre · **First-party** = maintenu par InferMatrixLab (pas une Spec tierce)  
**Structure :** **L1 = catégorie de modèle** → **L2 = matériel** (NVIDIA / Ascend / Neuron-Trainium / TPU / Apple-Metal / Intel / Edge-NPU / CPU-RAM-SSD tier / Cross-vendor kernels ; puces non listées sous Other accelerators)  
**Langues :** édition française ; primaire chinoise [README.md](README.md). Noms de projets et liens restent en anglais.

### Engine spécialisé ≠ Serving générique (à lire d’abord)

| Concept | Qu’est-ce ? | Ce dépôt ? |
|---|---|---|
| **Engine spécialisé** | Chemin d’inférence compilé ou profondément customisé pour une ISA / runtime vendeur / famille de modèles | ✅ Ici |
| **Serving générique** | Stack multi-modèles multi-GPU (vLLM, SGLang, TGI…) | ❌ Pas d’annuaire ; seulement les **lignes plugin hard/modèle** |
| **Bibliothèque de kernels** | Couche d’opérateurs appellable par plusieurs engines | ✅ OK sous la classe de modèles → Cross-vendor kernels |
| **Outils format / conversion** | Export ONNX/GGUF seul, sans runtime d’inférence | ❌ En général non (Core ML Tools conversion+déploiement peut qualifier) |

---

## Règles de contribution

- **⭐ Established :** docs solides ; build/run reproductible ; public ~≥ 6 mois ou standard de fait d’une stack puce.
- **☄️ Rising :** actif sur 12 mois ; famille de modèles ou matériel nommé ; lien vérifiable.
- **Requis :** catégorie de modèle, matériel, définition en une ligne, lien, ⭐/☄️ ; marquer les lignes first-party.
- **Rejet :** pubs de serving générique ; aucune spécialisation ; simples wrappers API.
- PR bienvenues ; ouvrir une issue si la section est floue.

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
- [Index first-party · InferMatrixLab (pas Spec tierce)](#index-first-party--infermatrixlab-pas-spec-tierce)
- [Contrast · Frontière vs Serving générique](#contrast--frontière-vs-serving-générique)
- [Related](#related)
- [License](#license)

---

## Dense LLM

Engines et backends matériels pour LLM Transformer / décodeur dense (hors MoE principal).

### NVIDIA

| Marque | Projet | En une ligne | Lien |
|---|---|---|---|
| ⭐ | **NVIDIA/TensorRT-LLM** | Engine LLM/VLM officiel NVIDIA : kernels CUDA custom, build d’engine, batching in-flight ; GPU NVIDIA | https://github.com/NVIDIA/TensorRT-LLM |
| ☄️ | **turboderp-org/exllamav3** | Inférence LLM quantifiée haute vitesse pour GPU NVIDIA grand public (ligne ExLlama) | https://github.com/turboderp-org/exllamav3 |

### Ascend

| Marque | Projet | En une ligne | Lien |
|---|---|---|---|
| ☄️ | **vllm-project/vllm-ascend** | Plugin matériel Ascend pour vLLM ; backend NPU dédié | https://github.com/vllm-project/vllm-ascend |

> Stacks MindIE / CANN surtout via docs/firmware Huawei ; ajouter une ligne ⭐ dès qu’un miroir public stable existe.

### Neuron-Trainium

| Marque | Projet | En une ligne | Lien |
|---|---|---|---|
| ☄️ | **aws-neuron/neuronx-distributed-inference** | NeuronX Distributed Inference (NxDI) : inférence LLM distribuée sur Inferentia/Trainium | https://github.com/aws-neuron/neuronx-distributed-inference |
| ☄️ | **vllm-project/vllm-neuron** | Chemin plugin vLLM × Neuron ; backend Trainium/Inferentia | https://github.com/vllm-project/vllm-neuron |

### TPU

| Marque | Projet | En une ligne | Lien |
|---|---|---|---|
| ☄️ | **vllm-project/tpu-inference** | Backend d’inférence TPU pour vLLM ; lié à Google TPU | https://github.com/vllm-project/tpu-inference |
| ☄️ | **huggingface/optimum-tpu** | Hugging Face Optimum TPU : chemin dédié pour déployer des Transformers sur TPU | https://github.com/huggingface/optimum-tpu |

### Apple-Metal

| Marque | Projet | En une ligne | Lien |
|---|---|---|---|
| ⭐ | **ml-explore/mlx** | Framework de tableaux Apple Silicon ; substrat d’exécution modèle sur Metal | https://github.com/ml-explore/mlx |
| ⭐ | **ml-explore/mlx-lm** | Chaîne d’inférence & serving LLM sur MLX ; Apple Silicon | https://github.com/ml-explore/mlx-lm |
| ⭐ | **apple/coremltools** | Conversion & déploiement Core ML ; Neural Engine / GPU iOS/macOS | https://github.com/apple/coremltools |

### Intel

| Marque | Projet | En une ligne | Lien |
|---|---|---|---|
| ⭐ | **openvinotoolkit/openvino.genai** | OpenVINO GenAI : runtime & pipelines d’IA générative sur CPU/GPU/NPU Intel | https://github.com/openvinotoolkit/openvino.genai |

### Edge-NPU

| Marque | Projet | En une ligne | Lien |
|---|---|---|---|
| ☄️ | **airockchip/rknn-llm** | Rockchip RKNN-LLM : stack LLM sur NPU embarqués (ex. RK3588) | https://github.com/airockchip/rknn-llm |
| ☄️ | **hailo-ai/hailort** | HailoRT : runtime d’inférence léger haute perf sur accélérateurs Hailo | https://github.com/hailo-ai/hailort |

### Other accelerators

| Marque | Projet | En une ligne | Lien |
|---|---|---|---|
| ☄️ | **tenstorrent/vllm-tt-plugin** | Plugin backend vLLM Tenstorrent ; avec la stack d’opérateurs TT-Metalium | https://github.com/tenstorrent/vllm-tt-plugin |
| ☄️ | **tenstorrent/tt-metal** | TT-Metalium / TT-NN : modèle de programmation opérateurs/kernels sur puces Tenstorrent | https://github.com/tenstorrent/tt-metal |

### Cross-vendor kernels

| Marque | Projet | En une ligne | Lien |
|---|---|---|---|
| ⭐ | **flashinfer-ai/flashinfer** | Bibliothèque de kernels Attention / sampling pour LLM serving ; embarquable | https://github.com/flashinfer-ai/flashinfer |

---

## MoE

Engines spécialisés Mixture-of-Experts : parallélisme d’experts, offload, ordonnancement stratifié, kernels MoE.

### NVIDIA

| Marque | Projet | En une ligne | Lien |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepInfer** | Framework d’inférence production DeepSeek (OSS) ; DeepSeek-V4.1-Flash sur NVIDIA SM100 / Ascend 950 | https://github.com/deepseek-ai/DeepInfer |

### Ascend

| Marque | Projet | En une ligne | Lien |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepInfer** | Idem ; chemin Ascend 950 (double matériel avec NVIDIA SM100) | https://github.com/deepseek-ai/DeepInfer |

### CPU-RAM-SSD tier

> **Classe Strata :** ici, « Strata » désigne surtout [Niko1221/Strata](https://github.com/Niko1221/Strata) — engine grand public pour gros MoE (ex. Qwen3.8-Flash-Next) avec **tiers VRAM / RAM système / SSD** et **CPU calculant en parallèle les experts non cachés**. Même famille : généralisations MoE, offload hôte/SSD, orchestration CPU–GPU. En cas d’homonymie, **faire confiance aux liens et one-liners ci-dessous**.

| Marque | Projet | En une ligne | Lien |
|---|---|---|---|
| ⭐ | **Niko1221/Strata** | Engine MoE type Qwen3.8-Flash-Next : experts dense/chauds sur GPU, tous les experts épinglés en RAM + CPU parallèle, SSD n-gram ; CUDA/HIP | https://github.com/Niko1221/Strata |
| ☄️ | **voidstackloop/extended-strata-moe** | Généralise le tiering async GPU/CPU Strata à de nombreux MoE llama.cpp (aligné méthode ; repo tôt) | https://github.com/voidstackloop/extended-strata-moe |
| ☄️ | **EfficientMoE/MoE-Infinity** | Offload d’experts MoE vers mémoire hôte/SSD + cache/prefetch aware activation | https://github.com/EfficientMoE/MoE-Infinity |
| ☄️ | **efeslab/fiddler** | ICLR'25 : orchestration CPU–GPU MoE local (calculer les experts manquants sur CPU) | https://github.com/efeslab/fiddler |
| ⭐ | **kvcache-ai/ktransformers** | Inférence MoE / grands modèles hybride CPU/GPU ; offload d’experts & chemins kernels | https://github.com/kvcache-ai/ktransformers |

### Cross-vendor kernels

| Marque | Projet | En une ligne | Lien |
|---|---|---|---|
| ⭐ | **deepseek-ai/DeepGEMM** | Bibliothèque kernels GPU BLAS/GEMM haute efficacité DeepSeek OSS | https://github.com/deepseek-ai/DeepGEMM |
| ⭐ | **deepseek-ai/DeepEP** | Bibliothèque de communication Expert Parallel DeepSeek OSS ; spécifique MoE | https://github.com/deepseek-ai/DeepEP |

---

## Multimodal / Omni

Engines pour familles multimodal / Omni (parole · vision · texte).

### NVIDIA

| Marque | Projet | En une ligne | Lien |
|---|---|---|---|
| ☄️ · First-party | **InferMatrixLab/system1-omni** | Engine haute perf maintenu par la communauté pour System1 (Rust ; style vLLM / vLLM-Omni) | https://github.com/InferMatrixLab/system1-omni |
| ☄️ · First-party | **InferMatrixLab/minicpm-o-4.5-single-gpu-engine** | Engine parole streaming mono-GPU spécialisé MiniCPM-o 4.5 | https://github.com/InferMatrixLab/minicpm-o-4.5-single-gpu-engine |

### Apple-Metal

| Marque | Projet | En une ligne | Lien |
|---|---|---|---|
| ☄️ · First-party | **InferMatrixLab/vllm-omni-mlx** | Serveur d’inférence omni-modalité sur Apple Silicon (API OpenAI / Anthropic) | https://github.com/InferMatrixLab/vllm-omni-mlx |

---

## Diffusion · Image

Chemins d’engine spécialisés ou compile-heavy pour diffusion image / génération d’images.

### NVIDIA

| Marque | Projet | En une ligne | Lien |
|---|---|---|---|
| ⭐ | **NVIDIA/TensorRT** | Optimiseur & runtime d’inférence NVIDIA général ; entrée pour de nombreux engines CV/diffusion/custom | https://github.com/NVIDIA/TensorRT |

---

## Diffusion · Video

Engines spécialisés diffusion / génération vidéo.

> Aucune ligne vérifiée pour l’instant ; PR bienvenues sous catégorie de modèle → matériel.

---

## Speech · TTS / ASR

Engines spécialisés synthèse / reconnaissance vocale.

### NVIDIA

| Marque | Projet | En une ligne | Lien |
|---|---|---|---|
| ☄️ · First-party | **InferMatrixLab/drama-3-single-b300-engine** | Engine TTS streaming pour Fish Audio Drama 3 sur un seul NVIDIA B300 | https://github.com/InferMatrixLab/drama-3-single-b300-engine |

### Ascend

| Marque | Projet | En une ligne | Lien |
|---|---|---|---|
| ☄️ · First-party | **InferMatrixLab/qwen3-tts-rsi-npu-engine** | Inférence Qwen3-TTS rapide autonome sur Ascend NPU (ex. 910B) via chemin RSI | https://github.com/InferMatrixLab/qwen3-tts-rsi-npu-engine |

---

## Embedding / Rerank

Chemins d’inférence spécialisés embedding / rerank.

> Aucune ligne vérifiée pour l’instant ; PR bienvenues sous catégorie de modèle → matériel.

---

## Other

Engines et catalogues de recettes encore modèle×matériel mais hors classes ci-dessus.

### NVIDIA

| Marque | Projet | En une ligne | Lien |
|---|---|---|---|
| ☄️ · First-party | **InferMatrixLab/vllm-rlt** | Engine pour transformers loopés : ordonnancement au niveau loop et stages composables | https://github.com/InferMatrixLab/vllm-rlt |

### Catalogs

| Marque | Projet | En une ligne | Lien |
|---|---|---|---|
| ☄️ · First-party | **InferMatrixLab/recipe** | Catalogue communautaire de recettes « modèle × engine × matériel » | https://github.com/InferMatrixLab/recipe |

---

## Index first-party · InferMatrixLab (pas Spec tierce)

> **Frontière (obligatoire) :** lignes **InferMatrixLab** déjà placées dans les tableaux (marquées First-party). **Ce ne sont pas** des Spec industrielles tierces. Index de transparence uniquement.

| Projet | Emplacement | Lien |
|---|---|---|
| system1-omni | Multimodal / Omni → NVIDIA | https://github.com/InferMatrixLab/system1-omni |
| minicpm-o-4.5-single-gpu-engine | Multimodal / Omni → NVIDIA | https://github.com/InferMatrixLab/minicpm-o-4.5-single-gpu-engine |
| vllm-omni-mlx | Multimodal / Omni → Apple-Metal | https://github.com/InferMatrixLab/vllm-omni-mlx |
| drama-3-single-b300-engine | Speech · TTS / ASR → NVIDIA | https://github.com/InferMatrixLab/drama-3-single-b300-engine |
| qwen3-tts-rsi-npu-engine | Speech · TTS / ASR → Ascend | https://github.com/InferMatrixLab/qwen3-tts-rsi-npu-engine |
| vllm-rlt | Other → NVIDIA | https://github.com/InferMatrixLab/vllm-rlt |
| recipe | Other → Catalogs | https://github.com/InferMatrixLab/recipe |

---

## Contrast · Frontière vs Serving générique

| Projet courant | Position | Note |
|---|---|---|
| vLLM / SGLang / TGI | Pas d’annuaire | Seulement les plugins **Ascend / Neuron / TPU / TT** (sous classe × matériel) |
| Ollama / llama.cpp | Rejet par défaut | Runtime portable cross-matériel ; discuter une ligne si un backend devient « chemin officiel puce » |
| Triton Inference Server | Pas d’annuaire produit | Coque d’orchestration ; backends (TRT-LLM etc.) déjà listés par modèle × matériel |

---

## Related

- **Index first-party :** [Index first-party · InferMatrixLab](#index-first-party--infermatrixlab-pas-spec-tierce)
- Autres docs d’inférence InferMatrixLab (liens croisés org plus tard)
- Pour le serving générique, utiliser un autre awesome / manuel — ne pas mélanger les tableaux

---

## License

Contenu de la liste contribué dans l’esprit **CC0 1.0** (réutilisation libre des tableaux). Les projets liés gardent leurs licences.
