# Comparative Research Notes

This document provides a technical comparative analysis between our professor's reference paper on multimodal cross-attention diagnostics and the selected published research paper applied to automated psychological state analysis.

---

## Part 1: Analysis of Professor's Reference Paper

### Bibliographic Details
* **Title:** Visual and lesion descriptor fusion using cross-attention for skin disease diagnosis
* **Authors:** Maira Afzal, Jamal Hussain Shah, Rabia Saleem, Muhammad Usman Younas, Ali Tahir, and Mutaz Elradi S. Saeed
* **Affiliations:** COMSATS University Islamabad, Government College University Faisalabad, Jazan University, Nile Valley University
* **Journal:** *Frontiers in Oncology* (Section: Cancer Imaging and Image-directed Interventions), 2026
* **Volume / Article:** Vol. 16, Article 1885137
* **DOI:** [10.3389/fonc.2026.1885137](https://doi.org/10.3389/fonc.2026.1885137)

### Research Problem & Motivation
Automated diagnosis of skin lesions presents severe challenges due to high inter-class visual similarity, subtle intra-class variations, and overlapping early-stage symptoms. Conventional deep learning approaches (such as standalone CNNs) rely exclusively on image pixels, failing to incorporate standardized dermatological heuristics. Furthermore, free-form clinical text exhibits high variability and noise. To address these limitations, the paper introduces a framework that derives standardized, structured lesion descriptors directly from images and aligns them with deep visual representations.

### Methodological Architecture
1. **Automated Region of Interest (ROI) Segmentation:**
   * Utilizes the Segment Anything Model (SAM) to isolate lesion regions from background skin and artifacts (hair, reflections), achieving 94.25% Dice score and 92.81% IoU on ISIC 2018.
2. **Visual Feature Encoding:**
   * Employs a fine-tuned Vision Transformer (ViT-Base/16). The segmented lesion $I_{lesion} \in \mathbb{R}^{H \times W \times C}$ is split into $N$ non-overlapping $16 \times 16$ patches, linearly projected with learnable position embeddings and a $[CLS]$ token to capture long-range spatial context and texture dependencies ($Z_{img} \in \mathbb{R}^{D_{img}}$).
3. **Domain-Guided Structured Clinical Descriptors (Algorithm 1):**
   * Computes quantitative attributes based on the dermatological ABCD criteria:
     * **Asymmetry Index ($AI$):** $AI = 1 - \frac{|M \cap M_{flip}|}{|M|}$
     * **Border Irregularity Index ($BII$):** $BII = \frac{P^2}{4\pi A}$ (compactness ratio)
     * **Color Variation Index ($CVI$):** CIELAB color space clustering ($CVI = \sum P_k \cdot \sigma_k$)
     * **Diameter ($D$):** Maximum pairwise boundary distance
     * **Erythema Index ($EI$):** Redness intensity metric
     * **Texture Index ($TI$):** GLCM-based texture feature fusion
   * Maps numerical metrics to standardized categorical terms (e.g., *mildly asymmetric*, *irregular border*) and compiles them into a templated structured descriptor string.
4. **Textual Encoding:**
   * Passes the structured descriptor through a pre-trained `BERT-base-uncased` language model, utilizing the output $[CLS]$ token representation ($Z_{text} \in \mathbb{R}^{D_{text}}$).
5. **Cross-Modal Attention (CMA) Fusion:**
   * Aligns modalities using visual features as Queries ($Q = Z_{img} W_q$) and textual features as Keys ($K = Z_{text} W_k$) and Values ($V = Z_{text} W_v$):
     $$Z_{fusion} = \text{Softmax}\left(\frac{(Z_{img} W_q)(Z_{text} W_k)^T}{\sqrt{d_k}}\right) (Z_{text} W_v)$$
   * Semantic clinical descriptors directly supervise and refine visual spatial attention before final classification.
6. **Class Imbalance & Explainability:**
   * Optimized with inverse-frequency weighted cross-entropy loss to prevent majority-class bias.
   * Employs Grad-CAM on visual attention maps and LIME on textual descriptor tokens to ensure transparency and clinical interpretability.

---

## Part 2: Analysis of the Selected Research Paper

### Bibliographic Details
* **Title:** A cross-modal transformer framework for multimodal depression assessment
* **Authors:** Hafiz Tayyab Mustafa, Alia Batool, Hamza Mustafa, Mujtaba Asad, Najam Ul Sabeeh, and Nadia Rehman
* **Journal:** *Brain Network Disorders* (Elsevier), 2026
* **DOI:** [10.1016/j.bnd.2026.09.001](https://doi.org/10.1016/j.bnd.2026.09.001)
* **Dataset:** Extended Distress Analysis Interview Corpus (E-DAIC)

### Research Problem & Motivation
Major Depressive Disorder is a complex brain network condition characterized by subtle, multi-tiered symptoms across cognitive, affective, and motor domains. Clinical assessments often rely on subjective self-report questionnaires, which suffer from recall bias and high variability. Mustafa et al. propose an automated, objective screening framework that extracts digital behavioral biomarkers from semi-structured clinical interviews using multimodal transformers.

### Methodological Architecture
1. **Computer Vision Modality (Facial Expression Dynamics):**
   * Uses a compact Vision Transformer (ViT) to process facial video frames, extracting spatial patterns of facial muscle activation, eye gaze aversion, and blunted affect.
   * Captures long-range temporal-spatial facial cues that conventional CNNs miss due to localized receptive fields.
2. **Textual Modality (Linguistic Markers):**
   * Uses RoBERTa (Robustly Optimized BERT Pretraining Approach) to encode clinical interview transcripts, capturing semantic indicators of cognitive impairment, hopelessness, and negative emotional tone.
3. **Cross-Attention Fusion Module:**
   * Deploys a cross-attention late fusion layer that computes interactive attention scores between visual facial tokens and linguistic tokens. This allows nonverbal facial micro-cues to modulate and be refined by verbal statements.
4. **Validation:**
   * Utilizes rigorous Leave-One-Subject-Out (LOSO) cross-validation to guarantee patient-independent generalizability and prevent data leakage.

---

## Part 3: Methodological Mapping to Project Domains

| Project Domain | Clinical Phenomenon | Professor's Reference Technique | Selected Paper & Proposed CV Project Translation |
| :--- | :--- | :--- | :--- |
| **Affective** | Sadness, blunted affect, anxiety, loneliness | ViT visual feature extraction of morphological skin variations | ViT modeling of facial action units (AU4, AU12), eyebrow furrowing, and mouth depression |
| **Cognitive** | Hopelessness, worthlessness, negative self-evaluation | BERT encoding of structured ABCD lesion descriptors | RoBERTa / BERT encoding of interview transcripts and clinical symptom descriptors |
| **Psychomotor** | Reduced motor activity, agitation, facial rigidity | SAM-based boundary tracking and geometric shape metrics | Optical flow and temporal ViT patch tracking of facial movement dynamics and gaze fixations |
| **Multimodal Alignment** | Cross-modal coherence between verbal and nonverbal cues | Cross-Modal Attention (ViT query $\times$ BERT key/value) | Cross-attention fusion aligning facial visual embeddings with linguistic symptom tokens |
| **Model Interpretability** | Transparent diagnostic support | Grad-CAM visual heatmaps + LIME token saliency | Grad-CAM saliency over expressive facial regions (eyes, mouth) + attention weight visualization |
