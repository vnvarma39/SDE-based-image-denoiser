

# **GMiSDE-Net**

## **Gamma Mixture-of-Experts with Constraint-Aware Implicit SDE Denoising**

---

## **Abstract**

GMiSDE-Net is a stochastic deep learning framework for denoising images corrupted by **multiplicative Gamma noise**, commonly encountered in SAR, ultrasound, and low-light imaging. The method combines a **Gamma Mixture-of-Experts (MoE)** architecture with **Constraint-Aware Heteroscedastic Score Networks (CHSN)** and an **implicit stochastic differential equation (SDE)** formulation. Unlike diffusion-based approaches that rely on explicit forward–reverse SDE simulation, the proposed model directly learns the terminal SDE solution, enabling stable, efficient, and uncertainty-aware restoration. Experimental results demonstrate strong performance across multiple datasets and noise severities, with improved robustness to noise-model mismatch.

---

## **Motivation**

Multiplicative noise presents challenges that differ fundamentally from additive Gaussian corruption:

* Noise variance depends on the underlying signal
* Classical statistical filters oversmooth fine structures
* CNN denoisers are biased toward additive noise assumptions
* Score-based diffusion models are computationally expensive and unstable for speckle noise

**GMiSDE-Net** is designed to address these issues through **explicit noise modeling**, **spatial adaptivity**, and **stochastic interpretability** without iterative sampling.

---

## **Core Idea**

The proposed framework models denoising as the terminal solution of a stochastic differential equation:

[
\hat{x} = x_0 + f_\theta(x_0, \mu(x_0), \sigma(x_0)),
]

where:

* (x_0) is the noisy observation
* (\mu(\cdot)) and (\sigma(\cdot)) are spatially adaptive drift and diffusion terms
* (f_\theta) is a learned implicit SDE operator

Rather than simulating an SDE trajectory, the network **directly learns the terminal mapping**, achieving both efficiency and stability.

---

## **Architecture Overview**

### **1. Gamma Mixture-of-Experts (MoE)**

* Multiple experts specialize in distinct noise regimes
* A learnable router assigns soft spatial weights
* Enables local adaptivity to heterogeneous speckle patterns

### **2. Constraint-Aware Heteroscedastic Score Networks (CHSN)**

Each expert predicts:

* **Drift** ((\mu)): structured correction
* **Diffusion** ((\sigma)): noise magnitude
* **Uncertainty**: confidence in predictions

Positivity and boundedness constraints are enforced to ensure physical plausibility.

### **3. Uncertainty-Guided Aggregation**

Expert outputs are combined as:
[
\mu = \sum_i w_i \cdot \mu_i, \quad
\sigma = \sum_i w_i \cdot \sigma_i,
]
with uncertainty modulating expert influence to prevent over-smoothing.

### **4. Implicit SDE Head**

The final restoration is computed in a **single forward pass**, eliminating reverse-time sampling while preserving stochastic semantics.

---

## **Key Contributions**

* **Implicit SDE Denoising** without explicit diffusion simulation
* **Mixture-of-Experts for Multiplicative Noise**, not additive assumptions
* **Uncertainty-Aware Restoration** with spatial adaptivity
* **Robustness to Noise Mismatch**, including mixed noise settings
* **Reduced Hyperparameter Sensitivity**, demonstrated via ablation studies

---

## **Experimental Evaluation**

The model is evaluated on **MNIST and CIFAR-10 (grayscale)** with synthetic Gamma speckle noise across varying severity levels.

**Metrics used:**

* Peak Signal-to-Noise Ratio (PSNR)
* Structural Similarity Index (SSIM)

Comparisons include:

* Classical CNN denoisers
* Modern multiplicative-noise baselines
* Architectural ablations of the proposed method

Results show consistent improvements in restoration quality and stability.

---

## **Ablation and Sensitivity Analysis**

Experiments analyze:

* Effect of uncertainty modulation
* Impact of expert routing versus single-expert variants
* Sensitivity to loss-weighting parameters
* Performance under increasing noise severity

Findings indicate that **architectural design dominates performance**, minimizing dependence on delicate hyperparameter tuning.

---

## **Why Implicit SDEs?**

Traditional score-based SDE methods:

* Require costly iterative sampling
* Accumulate discretization error
* Are sensitive to multiplicative noise statistics

GMiSDE-Net:

* Eliminates forward diffusion
* Learns the terminal solution directly
* Retains stochastic interpretability with lower computational cost

---

## **Intended Use**

This work is relevant for:

* Researchers in **inverse imaging problems**
* Applications in **SAR, ultrasound, and speckle-dominated imaging**
* Study of **stochastic modeling in deep neural networks**

---

## **Author**

**Vanapala Nikhil Varma**
Mahindra University, Hyderabad


Just say the word.
