<div align="center">
  <img src="assets/banner.svg" alt="Awesome Self-Supervised Learning Banner" width="100%" />
</div>

<div align="center">
  <a href="https://github.com/ishandutta2007/Awesome-Awesome-Awesome"><img src="https://img.shields.io/badge/Awesome-%E2%9C%94-blueviolet?style=flat-square&logo=github" alt="Awesome"/></a><a href="https://discord.gg/jc4xtF58Ve"><img src="https://img.shields.io/badge/Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white" alt="Discord" /></a>
  <img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square" alt="PRs Welcome" />
  <a href="https://github.com/ishandutta2007"><img alt="GitHub followers" src="https://img.shields.io/github/followers/ishandutta2007?label=Follow" /></a>
</div>

# 🚀 Awesome-Self-Supervised-Learning

> A curated list of resources, algorithms, and applications related to Self-Supervised Learning (SSL), improving representation learning without large labeled datasets.

## 🧠 Self-Supervised Learning (SSL): Evolution, Variants, Types, & Applications

Self-Supervised Learning (SSL) is a machine learning paradigm that eliminates the need for expensive, human-annotated datasets by generating training signals directly from the raw data itself. The algorithm treats part of the data as a target to predict (e.g., masking a word or an image patch) and uses the remaining data as context. By designing specialized "pretext tasks," SSL allows models to learn rich, foundational semantic representations from billions of uncurated images, audio files, or text streams, which can then be fine-tuned on downstream tasks using minimal labels.

---

## ⏳ 1. The Chronological Evolution

The algorithmic progression of SSL reflects a transition from rigid, hand-crafted geometric pretext tasks to dual-tower contrastive networks, moving toward non-contrastive feature prediction and unified masked autoencoders.

```mermaid
flowchart LR
    A["Heuristic Pretext Tasks (2014-2018)<br/>(Jigsaw / Image Rotation)"]
    --> B["Contrastive Learning (SimCLR, 2020)<br/>(Negative Samples / InfoNCE Loss)"]
    --> C["Masked Autoencoders (MAE/JEPA, 2022+)<br/>(Direct Token Reconstruction / Features)"]
```

| Era | Description | Year First Used | Paper Link |
|---|---|---|---|
| **[The Early Heuristic Pretext Era (~2014–2018)](pages/heuristic_pretext.md)** | **Concept:** Models were trained on engineered, pseudo-label tasks. Common computer vision methods included predicting the rotation angle of an image (0°, 90°, 180°, 270°) or solving a scrambled 3x3 patch jigsaw puzzle.<br>**Limitation:** Representations were often tied too closely to the specific tricks of the pretext task, lacking global semantic generalization. | 2014 | [Discriminative Unsupervised Feature Learning with Convolutional Neural Networks](https://arxiv.org/abs/1406.6909) |
| **[The Contrastive Learning Era (~2020–2022)](pages/contrastive_era.md)** | **Concept:** Popularized by architectures like **SimCLR** and **MoCo**. It defined representation learning as a matching game: augment an image twice (e.g., crop and color jitter) and push their vectors close together in embedding space while pushing apart "negative" samples (different images) using the InfoNCE loss function.<br>**Limitation:** Requires massive batch sizes or memory banks to host enough negative samples to prevent the embedding space from collapsing. | 2020 | [SimCLR](https://arxiv.org/abs/2002.05709) |
| **[The Masked Autoencoding & Joint Embedding Era (~2022–Present)](pages/masked_autoencoding_era.md)** | **Concept:** Pioneered in text by BERT and adapted to vision by Meta's **Masked Autoencoders (MAE)** and **Joint Embedding Predictive Architectures (I-JEPA)**. MAE hides up to 75% of an image's pixel patches and forces a transformer to reconstruct them, while JEPA avoids pixel-level noise entirely by predicting hidden *feature representations* rather than raw pixels. | 2021 | [MAE](https://arxiv.org/abs/2111.06377) |

---

## ⚙️ 2. Core Algorithmic & Objective Variants

Self-supervised frameworks are strictly categorized based on how they calculate their loss functions and prevent mathematical representation collapse (where the model maps all inputs to a single static vector).

| Variant | Mechanism & Examples | Year First Used | Paper Link |
|---|---|---|---|
| **[Contrastive Learning](pages/contrastive_learning.md)** | **Mechanism:** Directly measures similarities and differences between pairs of data points. It uses a cross-entropy-style loss (InfoNCE) to attract positive views and repel negative views.<br>**Examples:** SimCLR, MoCo (Momentum Contrast), and CLIP (Vision-Language Contrast). | 2018 | [Representation Learning with Contrastive Predictive Coding](https://arxiv.org/abs/1807.03748) |
| **[Non-Contrastive / Clustering Methods](pages/non_contrastive.md)** | **Mechanism:** Eliminates negative samples entirely. It trains a dual-tower network where both branches look at different augmentations of the *same* image, using architectural constraints (like stop-gradients or clustering layers) to prevent collapse.<br>**Examples:** **BYOL** (Bootstrap Your Own Latent), **SwAV**, and **SimSiam**. | 2020 | [Bootstrap Your Own Latent (BYOL)](https://arxiv.org/abs/2006.07733) |
| **[Information-Maximization (Variance-Covariance Regularization)](pages/info_max.md)** | **Mechanism:** Operates on the principle of information theory. It decorrelates the features across the embedding dimensions, mathematically forcing the network to utilize its entire capacity rather than compressing data onto a single redundant axis.<br>**Examples:** **Barlow Twins** and **VICReg** (Variance-Covariance-Invariance Regularization). | 2021 | [Barlow Twins](https://arxiv.org/abs/2103.03230) |
| **[Masked Prediction (Autoregressive & Masked Autoencoding)](pages/masked_prediction.md)** | **Mechanism:** Randomly hides parts of the token sequence or pixel patches and uses the surrounding visible elements to infer the missing contents.<br>**Examples:** GPT (causal autoregressive), BERT (masked language modeling), and MAE (masked vision autoencoding). | 2018 | [BERT](https://arxiv.org/abs/1810.04805) |

---

## 📊 3. Modality Implementation Types

SSL operates cross-modally, serving as the foundational engine for modern multi-modal and specialized deep learning architectures.

| Modality | Implementation | Year First Used | Paper Link |
|---|---|---|---|
| **[Natural Language Processing (NLP)](pages/nlp.md)** | Uses massive unannotated text corpora to predict the next word or fill in omitted sentence blanks, capturing grammatical syntax, logic boundaries, and world knowledge naturally. | 2013 | [Word2Vec](https://arxiv.org/abs/1301.3781) |
| **[Computer Vision (Self-Supervised Vision)](pages/cv.md)** | Splits images into grids of visual tokens or patches. Models learn spatial geometries, color textures, and edge constraints through contrastive pairings or masked patch restoration. | 2015 | [Unsupervised Visual Representation Learning by Context Prediction](https://arxiv.org/abs/1505.05192) |
| **[Audio & Speech Processing](pages/audio_speech.md)** | Models like **wav2vec 2.0** mask sections of raw audio waveforms and pass them through convolutional and transformer layers to predict quantized latent representations, learning phonemes and vocal cadences without text transcripts. | 2019 | [wav2vec](https://arxiv.org/abs/1904.05862) |

---

## 🛡️ 4. Fundamental Challenges & Mitigations

| Challenge | Phenomenon & Mitigation | Year First Used | Paper Link |
|---|---|---|---|
| **[Representation Collapse](pages/rep_collapse.md)** | **The Phenomenon:** If a network is trained to output identical vectors for two views of the same image without a regularizing force, it will quickly learn a trivial solution: outputting a constant vector (e.g., all zeros) for *every* image.<br>**Mitigation:** Implementing **asymmetric architectures** (adding a predictor MLP to only one tower), utilizing **stop-gradient operations** (BYOL), or enforcing **identity covariance matrices** (Barlow Twins). | 2020 | [BYOL](https://arxiv.org/abs/2006.07733) |
| **[High Computational Footprint](pages/high_compute.md)** | **The Phenomenon:** Contrastive setups depend heavily on viewing vast amounts of negative comparisons simultaneously to build accurate boundaries.<br>**Mitigation:** Deploying **Momentum Consumers (MoCo)** which use a continuous queue system to decouple negative batch size scaling from active GPU memory constraints. | 2019 | [MoCo](https://arxiv.org/abs/1911.05722) |

---

## 🌍 5. Frontier Real-World Applications

| Application | Description | Year First Used | Paper Link |
|---|---|---|---|
| **[Medical Image Diagnostics (Sparse Label Adaptation)](pages/medical_image.md)** | Hospitals possess millions of medical scans (X-rays, MRIs) but very few high-quality annotations. SSL pre-trains a vision encoder on the raw imagery to learn clinical anatomy markers, allowing a final downstream model to diagnose rare pathologies using fewer than 100 labeled patient cases. | 2020 | [Self-Supervised Learning for Medical Image Classification](https://arxiv.org/abs/2012.02927) |
| **[Foundation Multi-Lingual Foundation Models](pages/multi_lingual.md)** | Web crawls provide trillions of lines of unannotated multilingual text. Masked and autoregressive SSL objectives allow models to construct shared linguistic embedding maps, translating or reasoning across resource-scarce languages without explicit bilingual dictionaries. | 2019 | [XLM](https://arxiv.org/abs/1901.07291) |
| **[Industrial Robotics & Autonomous Exploration](pages/robotics.md)** | Robots running **World Models** (like JEPA) map physical mechanics and object movements via video inputs. By predicting the next semantic frame feature during mock tasks, the robot learns physical acceleration, depth constraints, and collision rules without manual code configuration. | 2018 | [World Models](https://arxiv.org/abs/1803.10122) |

## 🌟 Star History
<div align="center">
<a href="https://www.star-history.com/?repos=ishandutta2007%2FAwesome-Self-Supervised-Learning&type=date&legend=bottom-right">
<picture>
<source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/chart?repos=ishandutta2007/Awesome-Self-Supervised-Learning&type=date&theme=dark&legend=bottom-right" />
<source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/chart?repos=ishandutta2007/Awesome-Self-Supervised-Learning&type=date&legend=bottom-right" />
<img alt="Star History Chart" src="https://api.star-history.com/chart?repos=ishandutta2007/Awesome-Self-Supervised-Learning&type=date&legend=bottom-right" />
</picture>
</a>
</div>
