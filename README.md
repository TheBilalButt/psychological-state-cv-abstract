# Psychological State Analysis Using Multimodal AI
### Computer Vision & Multimodal Affective Computing Research Lab

This repository contains academic research materials, comparative literature analyses, and the official laboratory abstract for the undergraduate research project **"Psychological State Analysis Using Multimodal AI."**

The research methodology is directly inspired by and adapted from the cross-modal diagnostic framework established by Afzal et al. (*Frontiers in Oncology*, 2026), translating dual-branch transformer architectures and cross-attention feature alignment into mental health assessment.

---

## Repository Structure

| File | Description |
| :--- | :--- |
| [`abstract.md`](abstract.md) | Official lab submission abstract formulated at **exactly 100 words**. |
| [`reference_paper.md`](reference_paper.md) | Full bibliographic details, official links, DOIs, and relevance analysis of the primary matching paper and three alternatives. |
| [`research_notes.md`](research_notes.md) | Detailed comparative technical notes breaking down the professor's reference paper and the selected benchmark paper. |

---

## Research Problem Statement

Automated evaluation of human psychological states (e.g., Major Depressive Disorder, clinical anxiety) presents fundamental challenges for unimodal Computer Vision:
1. **Visual Subtlety & Affective Blunting:** Facial expressions of depressed individuals often exhibit subtle micro-expressions, facial rigidity, reduced blink rates, or flattened affect that traditional Convolutional Neural Networks (CNNs) fail to model due to limited local receptive fields.
2. **Context Blindness in Standalone CV:** Standalone facial video analysis cannot differentiate between transient facial movements and pathological depressive symptoms without semantic context regarding the subject's cognitive state.
3. **Data Scarcity & Subject Variation:** Clinical datasets suffer from significant inter-subject variability, class imbalance, and privacy constraints, necessitating robust foundation backbones and principled cross-modal alignment.

---

## Reference Paper Benchmark Details

### Primary Benchmark Match
* **Title:** *A cross-modal transformer framework for multimodal depression assessment*
* **Authors:** Hafiz Tayyab Mustafa, Alia Batool, Hamza Mustafa, Mujtaba Asad, Najam Ul Sabeeh, and Nadia Rehman
* **Journal:** *Brain Network Disorders* (Elsevier), 2026
* **DOI:** [10.1016/j.bnd.2026.09.001](https://doi.org/10.1016/j.bnd.2026.09.001)
* **Official Source Link:** [https://doi.org/10.1016/j.bnd.2026.09.001](https://doi.org/10.1016/j.bnd.2026.09.001)

### Professor's Foundation Paper
* **Title:** *Visual and lesion descriptor fusion using cross-attention for skin disease diagnosis*
* **Authors:** Maira Afzal, Jamal Hussain Shah, Rabia Saleem, Muhammad Usman Younas, Ali Tahir, and Mutaz Elradi S. Saeed
* **Journal:** *Frontiers in Oncology*, Vol. 16, Article 1885137 (2026)
* **DOI:** [10.3389/fonc.2026.1885137](https://doi.org/10.3389/fonc.2026.1885137)
* **Official Open Access Link:** [https://doi.org/10.3389/fonc.2026.1885137](https://doi.org/10.3389/fonc.2026.1885137)

---

## Relevance to Project

Our project explores psychological indicators across three primary behavioral domains:
1. **Affective Domain (Facial Computer Vision):** Investigates sadness, flattened affect, anxiety, and micro-expressions extracted through a **Vision Transformer (ViT)** operating on dynamic facial regions of interest and Action Units (AUs).
2. **Cognitive Domain (Linguistic NLP):** Captures verbalized hopelessness, worthlessness, and negative thought patterns extracted using **BERT / RoBERTa** contextual embeddings.
3. **Psychomotor Domain (Behavioral Dynamics):** Tracks observable psychomotor retardation, head orientation shifts, and facial movement velocity.
4. **Cross-Attention Alignment:** Paralleling Afzal et al.'s design where visual features act as Queries ($Q$) and clinical descriptors act as Keys ($K$) and Values ($V$), our proposed system applies cross-attention to allow semantic affective cues to guide and refine visual facial representations.

---

## Official 100-Word Abstract

> **Automated psychological state analysis struggles to capture subtle nonverbal indicators such as microexpressions, psychomotor retardation, and affective blunting from facial video alone. This project proposes a Computer Vision framework leveraging a Vision Transformer to extract spatial facial representations and dynamic Action Units from video. To overcome unimodal visual limitations, visual feature embeddings will be integrated with structured psychological descriptors through a cross attention mechanism, allowing semantic affective cues to guide visual feature refinement. The proposed architecture will be evaluated on the benchmark Extended Distress Analysis Interview Corpus using subject independent cross validation to assess clinical diagnostic accuracy and model generalizability.**

*(Verified: Exactly 100 words)*

---

## Academic Source Links & Verified Literature

* Elsevier *Brain Network Disorders*: [doi.org/10.1016/j.bnd.2026.09.001](https://doi.org/10.1016/j.bnd.2026.09.001)
* Frontiers in Oncology: [doi.org/10.3389/fonc.2026.1885137](https://doi.org/10.3389/fonc.2026.1885137)
* IEEE Transactions on Circuits and Systems for Video Technology: [doi.org/10.1109/TCSVT.2024.3491098](https://doi.org/10.1109/TCSVT.2024.3491098)
* Nature npj Mental Health Research: [doi.org/10.1038/s44184-024-00112-8](https://doi.org/10.1038/s44184-024-00112-8)
* Frontiers in Neuroscience: [doi.org/10.3389/fnins.2023.1188434](https://doi.org/10.3389/fnins.2023.1188434)
