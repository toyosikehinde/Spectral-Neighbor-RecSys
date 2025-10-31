# Spectral Neighbor Recommender

# Spectral Neighbor Recommender
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1o6_YSl7K44pgO8PPFZSlLrq9fVHS7qql?usp=sharing)


## Overview
The Spectral Neighbor Recommender is a prototype music recommendation system that uses spectral audio features and cosine similarity to find songs that are most similar to a given track. It demonstrates how signal processing and feature-based similarity can support audio-based music recommendations.

## Features
- Extracts spectral and temporal features using Librosa
- Computes cosine similarity between tracks
- Recommends top-K similar tracks
- Structured for experimentation and research

## Installation
```bash
python -m venv env
source env/bin/activate    # Windows: env\Scripts\activate
pip install -r requirements.txt
