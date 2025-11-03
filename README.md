# Spectral Neighbor Recommender

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1o6_YSl7K44pgO8PPFZSlLrq9fVHS7qql?usp=sharing)

*A Content-Based Music Recommendation Prototype Using Spectral and Cepstral Audio Features*  

---

### Overview  
The **Spectral Neighbor Recommender** is a content-based system that retrieves acoustically similar tracks from the [FMA Small Dataset](https://github.com/mdeff/fma) using **Fourier-domain spectral analysis** and **cosine similarity**.  

The system demonstrates how spectral features and timbral descriptors can model perceptual similarity between songs without using metadata or collaborative filtering.  
It also contributes to ongoing research on **adversarial and ethical risks in AI-based music recommendation systems**, exploring robustness, interpretability, and fairness in audio embeddings.

---

###  System Architecture  

1. **Dataset Processing**  
   - Extracts 30-second excerpts from ~40 tracks in the FMA Small dataset.  
   - Resamples all audio to 22,050 Hz for consistency.  

2. **Feature Extraction**  
   - Computes Short-Time Fourier Transform (STFT) using a 2048-point FFT and 512-sample hop.  
   - Derives mel-spectrograms, converts them to log-mel scale, and extracts 13-dimensional **MFCCs**.  
   - Adds complementary **spectral descriptors**: centroid, roll-off, flatness, zero-crossing rate, and tempo (from onset strength).  
   - Aggregates all descriptors across time using means and standard deviations to form fixed-length feature vectors.  

3. **Similarity Computation**  
   - Standardizes features to zero mean and unit variance.  
   - Computes **cosine similarity** between every pair of tracks, producing a dense similarity matrix.  
   - Returns the **Top-K nearest neighbors** for each seed track.  

4. **Ablation Study**  
   - Compares MFCC-only vs. combined (MFCC + spectral) representations to isolate the incremental contribution of broad spectral descriptors.

---

### Evaluation Metrics  

| Metric | Description | Result |
|:--|:--|:--:|
| **Feature Stability** | Correlation between MFCC vectors from random 5-second segments of the same track | **0.969** |
| **Artist@10** | Fraction of tracks whose Top-10 neighbors include at least one by the same artist | **0.226** |
| **Genre Purity@10** | Average proportion of Top-10 neighbors sharing the same genre | **0.648** |
| **Mean Reciprocal Rank** | Expected inverse rank of the first same-artist match (Top ≈ 50) | **1.000** |
| **Ablation (Artist@K)** | MFCC-only = 0.951  •  Combined = 0.949 | — |

These metrics quantify both **representation stability** and **semantic neighborhood quality** in the embedding space.  
Results suggest that cepstral (MFCC) features dominate retrieval performance at the current dataset scale.

---

## Feature Extraction

Each song is analyzed using the Short-Time Fourier Transform (STFT) to capture frequency information over time. From these spectrograms, features such as MFCCs, spectral centroid, roll-off, flatness, and tempo are computed to describe the timbral and spectral identity of each track.

### The Role of the Fourier Transform
The Fourier Transform of a sine wave explains the core principle behind the system’s feature extraction. A sine wave contains energy at only one frequency, and its Fourier Transform produces two impulses showing that concentration. In the Spectral Neighbors Recommender, this concept is extended through the Short-Time Fourier Transform, which analyzes real music signals over time to reveal their frequency content. Features such as MFCCs, spectral centroid, and roll-off are computed from these Fourier representations, allowing each song to be described by its unique spectral pattern. This forms the foundation for comparing tracks through cosine similarity and generating meaningful, sound-based recommendations.


### Installation & Usage  

```bash
# Clone repository
git clone https://github.com/<your-username>/spectral-neighbor-recommender.git
cd spectral-neighbor-recommender

# Install dependencies
pip install -r requirements.txt

# Launch the notebook
jupyter notebook Spectral_Neighbor_Recommender.ipynb
