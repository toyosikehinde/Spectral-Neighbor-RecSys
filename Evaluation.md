# Evaluation Plan  
### Spectral Neighbor Recommender Prototype

---

## 1. Overview

This document defines the evaluation framework for the **Spectral Neighbor Recommender**, a content-based music retrieval prototype that measures similarity between audio tracks based on **spectral and cepstral features**.  
The goal is to evaluate how consistently these features capture perceptual similarity across tracks of different genres and production styles.

The current evaluation focuses on **feature robustness**, **semantic neighborhood quality**, and **comparative ablation** of feature subsets.

---

## 2. Implemented Metrics

### **Feature Stability (MFCC Mean Correlation)**
- **Definition:** Measures correlation between MFCC mean vectors computed from two random five-second segments of the same track.  
- **Purpose:** Evaluates the temporal reliability of feature representations.  
- **Formula:**  
  \[
  r = corr(MFCC_{seg1}, MFCC_{seg2})
  \]
- **Interpretation:** Higher correlation (≈1.0) indicates that the cepstral descriptors capture stable timbral properties rather than transient variations.

---

### **Artist@K**
- **Definition:** Fraction of seed tracks whose top-K neighbors include at least one track by the same artist.  
- **Purpose:** Tests whether similar timbral profiles correspond to artist identity.  
- **Method:**  
  For each seed, check whether any of its K nearest neighbors match the seed’s artist name.  
  Average the results across all seeds.

---

### **Genre Purity@K**
- **Definition:** Mean proportion of tracks within the top-K neighborhood that share the same genre as the seed.  
- **Purpose:** Evaluates cluster homogeneity and stylistic consistency of retrievals.  
- **Interpretation:** Higher values indicate stronger genre grouping in feature space.

---

### **Mean Reciprocal Rank (MRR)**
- **Definition:** Average inverse rank of the first same-artist retrieval within the top-N (≈50) candidate list.  
- **Formula:**  
  \[
  MRR = \frac{1}{|Q|}\sum_{i=1}^{|Q|} \frac{1}{rank_i}
  \]
- **Purpose:** Quantifies how quickly relevant items appear in the ranked list.  
- **Interpretation:** Higher MRR means relevant matches are ranked near the top.

---

## 3. Proposed Next-Phase Metrics (Conceptual)

### **Precision@K**
- **Definition:** Proportion of relevant (same-genre or same-artist) items among the top-K results.  
- **Purpose:** Measures the accuracy of the recommender’s highest-ranked outputs.  
- **Status:** To be implemented once a validation subset with genre or artist ground-truth labels is finalized.

### **Recall@K**
- **Definition:** Fraction of all relevant items in the dataset that appear within the top-K list.  
- **Purpose:** Complements Precision@K by evaluating coverage and retrieval completeness.  
- **Status:** Planned extension for larger datasets.

---

## 4. Ablation and Comparative Studies

The prototype includes a comparison between:
- **MFCC-only feature vectors**, and  
- **Combined MFCC + Spectral + Tempo** vectors.  

This analysis identifies the contribution of cepstral versus spectral descriptors to neighborhood formation.  
Early results suggest that MFCCs alone dominate retrieval performance on the current dataset size.

---

## 5. Qualitative Evaluation

A **manual qualitative inspection** is performed to verify the perceptual validity of retrieved results.  
For each seed track, the top-K nearest neighbors are reviewed for timbral and stylistic similarity.  
Observations include:
- Genre coherence  
- Cross-genre blending  
- Instrumentation and texture similarity  
- Occasional mismatches (e.g., dynamic or production artifacts)

Findings from this inspection complement the quantitative metrics and help interpret system behavior beyond numerical scores.

---

## 6. Future Extensions 

Potential future enhancements include:
- Incorporating **Precision/Recall curves** on extended datasets.   
- Introducing optional **listening-based evaluations** or human-rated relevance scoring for subjective validation once system scaling is complete.

---

## 7. Alignment with Research Goals

These evaluation methods directly support the broader investigation into **adversarial and ethical risks in AI-based music recommendation systems**, particularly concerning:
- Feature robustness under signal perturbations,  
- Fairness across genres and production styles, and  
- Transparency of low-level similarity modeling.

---


