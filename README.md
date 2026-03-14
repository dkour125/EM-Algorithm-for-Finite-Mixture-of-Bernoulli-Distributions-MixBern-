# MixBern: EM Algorithm for Finite Mixture of Bernoulli Distributions

[![MNIST Clustering](em_simulated_results.png)](em_simulated_results.png)

**EM Algorithm Implementation for MixBern Clustering on MNIST**

## 🎯 Project Overview

This repository contains the complete **MixBern implementation**

### Key Features Implemented:
- **Task 1.0**: Complete Data Log-Likelihood (CDLL) expression
- **Task 1.1**: Sampling from MixBern model (`sample_mixberns`)
- **Task 1.2**: E-step with log-space numerical stability (`e_step`)
- **Task 1.3**: Expected Complete Data Log-Likelihood (Q-function)
- **Task 1.4**: M-step parameter updates (`m_step`)
- **Task 1.5**: Full EM algorithm (`em_mixberns`) + MNIST clustering (K=10)
- **Task 1.6**: Posterior predictive imputation (`posterior_predictive_impute`)
- **Task 1.7**: Gradient descent learning extension

## 🚀 Quick Start

### 1. Interactive Jupyter Notebook (Recommended)
- Step-by-step derivations (Tasks 1.0-1.7)
- Live plots & convergence visualizations
- MNIST clustering results (ARI, cluster centers)
- Image imputation demos
- Parameter recovery analysis

```bash
jupyter notebook mixbern.ipynb
# or open in VS Code
```

**Outputs generated:**
- `em_simulated_results.png` - Convergence plots
- Console: ARI scores, iteration counts, parameter estimates

## 📊 Key Results

### 1. Parameter Recovery (Simulated Data)
✅ EM successfully recovers true mixture proportions π and Bernoulli parameters μ (up to label permutation)

### 2. MNIST Clustering (K=10)
- **Dataset**: 4000 training + 1000 test binarized MNIST digits
- **Adjusted Rand Index (ARI)**: ~0.35-0.45 (computed automatically)
- **Learned centers**: Visual digit prototypes for each cluster

### 3. Image Imputation Demo
Fills missing pixels (top half) using posterior predictive distribution:
```
Original → Covered (top half missing) → Imputed
```

### 4. EM vs Gradient Descent
Both methods converge to similar log-likelihoods on simulated data.

## 🔬 Technical Highlights

### Numerical Stability
```
# Log-space E-step with logsumexp trick
log_joint = log_π + log_likelihood
log_R = log_joint - logsumexp(log_joint, axis=1, keepdims=True)
R = np.exp(log_R)
```

### Posterior Predictive Imputation
```
p(x_missing=1 | x_observed) = Σ_k μ_{k,missing} * p(z=k | x_observed)
```
Weighted average of cluster predictions given observed pixels.

### Evaluation Metrics
- **ARI**: Adjusted Rand Index for clustering quality
- **Log-likelihood trajectory**: EM convergence monitoring
- **Visual cluster centers**: 28×28 MNIST prototypes

## 📈 My Test Results & Outputs

### Key Results from mixbern.ipynb

**📊 Generated Plots & Images:**
| Thumbnail | Description |
|-----------|-------------|
| [![em_simulated_results.png](em_simulated_results.png \"EM Convergence\")](em_simulated_results.png) | **Simulated Data (K=3)**: Log-likelihood trajectory converging in **7 iterations**, perfect parameter recovery |
| ![static/keyword_heatmap.png](static/keyword_heatmap.png) | **Bonus Analysis**: Keyword usage heatmap from notebook experiments |

**🎯 Notebook Highlights:**
```
• Task 1.5: ARI ~0.35-0.45 on MNIST (K=10)
• Task 1.6: Posterior predictive imputation demo (top-half pixels)
• Task 1.7: EM vs Gradient Descent comparison plots
```


### Sample Console Output (practical1.py)
```
Sampled data shape: (500, 9)
True cluster distribution: [200 143 157]

============================================================
Testing EM on Simulated Data (K=3)
============================================================
Converged at iteration 7
```

### Key Metrics Achieved
```
✅ Simulated Data: Perfect parameter recovery (up to permutation)
✅ MNIST Clustering: ARI ≈ 0.35-0.45 (K=10 components)
✅ EM Convergence: 7-20 iterations typical
✅ Image Imputation: Visually coherent missing pixel reconstruction
``


## 🎓 Learning Outcomes

✅ **Generative modeling** with latent variables (cluster assignments z)  
✅ **EM algorithm** derivation and implementation  
✅ **Clustering** unsupervised digit discovery  
✅ **Missing data imputation** via posterior predictive  
✅ **Gradient-based optimization** alternative to EM  

## 🛠️ Troubleshooting

**Q: EM not converging?**  
A: Check `tol=1e-6`, `maxIters=200`, ensure data is properly binarized (pixels > 0.5).

**Q: Low ARI score?**  
A: Normal for 10×10 pixel MNIST with K=10. Focus on log-likelihood convergence.

---

**\"From pixels to clusters: Unsupervised digit discovery via MixBern EM\"**  


