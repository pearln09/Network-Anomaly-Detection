# Network-Anomaly-Detection
## Project Overview
In modern day cybersecurity landscape, signature-based detection is no longer effective to stop Zero-day DDoS attacks. This project implements a **proactive,anomaly-based detection framework** that learns to identify the "DNA" or the basis of normal network traffic and flags deviations as potential threats. I have developed and compared four distinct machine learning models to determine the most effective balance between detection accuracy and computational efficiency, ranging from **Deep Learning Autoencoders** to **Ensemble Tree methods**

## Key Features
- **Deep Learning Optimization:** Self-tuned Autoencoder with a hierarchical 4-layer architecture
- **Comparative Analysis:** Benchmarked Autoencoder, isolation Forest and Local Outlier Factor (LOF)
- **Statistical Thresholding:** Implemented a 4-sigma($4\sigma$) reconstruction error threshold to minimize false positives in high-traffic environments
- **Manifold Visualization:** Utilized t-SNE to project 41-dimensional network data into 2D space for cluster analysis.

## Model Performance Comparison
| Algorithm | DDoS Precision | DDoS Recall | **DDoS F1-Score** | Verdict |
| :--- | :--- | :--- | :--- | :--- |
| ***Optimized Autoencoder** | **0.99** | | 0.90 | **0.95** | Best for Accuracy |
| **Isolation Forest** | 0.98 | **0.93** | **0.95** | Best for Speed/Recall |
| Baseline Autoencoder | 0.99 | 0.84 | 0.91 | Solid Baseline |
| Local Outlier Factor | 0.97 | 0.64 | 0.77 | Weakest Performance |

## Technical Aspects
- **The Autoencoder Logic:** The model uses a symmetric Encoder-Decoder structure. By forcing 41 features through a 8-neuron bottleneck, the network learns a "lossy compression" of normal traffic patterns. Hence for **Normal Traffic**, there is **Low Reconstruction Error (MSE)** while for a **DDoS attack**, there is a **High Reconstruction Error** as the model "fails" to rebulid patterns it hasn't seen i.e. patterns observed during a DDoS attack.
- **Dimensionality Reduction (t-SNE):** Before modeling, I used t-SNE to verify class separability. The visualization confirmed that DDoS attacks majorly form distinct non-linear clusters, justifying the use of deep learning over simple linear filters.

## Installation & Usage

**1. Clone the Repository**
```bash
git clone [https://github.com/pearln09/Network-Anomaly-Detection.git](https://github.com/pearln09/Network-Anomaly-Detection.git)
```
**2. Install dependencies**
```bash
pip install tensorflow scikit-learn matplotlib seaborn pandas numpy
```
**3. Run the notebook:** Open the .ipynb file in Google Colab or Jupyter Notebook and run the cells sequentially to reproduce the results.

## Optimization Strategy

To improve the inital baseline Autoencoder precision from 0.58 to 0.70 in the Optimized Autoencoder, i implemented:
-**Layer Expansion:** Added a 64-neuron entry layer to capture more complex feature correlations.
-**Epoch Tuning:** Increased training from 50 epochs to reach a more stable global minimum.
-**Threshold Refinement:** Shifted from $3\sigma$ to $4\sigma$ thresholding, prioritizing the reduction of false alarms while maintaining a 0.95 F1-score.
