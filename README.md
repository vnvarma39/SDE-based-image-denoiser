GMiSDE-Net
Gamma Mixture-of-Experts with Constraint-Aware Implicit SDE Denoising
Overview

This repository presents GMiSDE-Net, a principled denoising framework for multiplicative (Gamma) noise, integrating stochastic modeling with deep neural networks. The method is designed for imaging modalities such as SAR, ultrasound, and low-light imaging, where noise is signal-dependent and heteroscedastic.

Unlike diffusion or score-based denoising approaches that rely on explicit forward–reverse stochastic simulation, GMiSDE-Net directly learns the terminal solution of an implicit stochastic differential equation (SDE). This design improves numerical stability, reduces computational overhead, and enables uncertainty-aware restoration.

Key Contributions

Implicit SDE Denoising
A terminal SDE formulation that avoids explicit diffusion sampling while preserving stochastic interpretability.

Gamma Mixture-of-Experts (MoE)
Multiple experts specialize in different noise regimes and are adaptively selected via a learned routing mechanism.

Constraint-Aware Heteroscedastic Score Networks (CHSN)
Each expert jointly predicts spatially varying drift, diffusion, and uncertainty parameters.

Uncertainty-Guided Aggregation
Learned uncertainty maps regulate expert contributions, preventing over-smoothing and instability.

Robustness to Noise Mismatch
The model generalizes beyond pure Gamma noise and remains stable under mixed noise conditions.

Method Summary

Given a noisy observation

𝑦
=
𝑥
⋅
Γ
(
𝑘
,
𝑘
)
,
y=x⋅Γ(k,k),

the proposed model estimates a terminal SDE solution of the form

𝑥
^
=
𝑥
0
+
𝑓
𝜃
(
𝑥
0
,
𝜇
(
𝑥
0
)
,
𝜎
(
𝑥
0
)
)
,
x
^
=x
0
	​

+f
θ
	​

(x
0
	​

,μ(x
0
	​

),σ(x
0
	​

)),

where the drift 
𝜇
μ, diffusion 
𝜎
σ, and uncertainty are inferred through a mixture of constraint-aware experts.

Expert outputs are spatially aggregated using soft routing weights and uncertainty modulation before being passed to an implicit SDE head, which performs the final restoration in a single forward pass.

Experimental Evaluation

The model is evaluated on grayscale MNIST and CIFAR-10 with synthetic Gamma speckle noise. Performance is assessed using:

PSNR (Peak Signal-to-Noise Ratio)

SSIM (Structural Similarity Index)

Comparisons include:

Classical CNN baselines

Modern multiplicative-noise denoisers

Ablation variants of the proposed architecture

The proposed method consistently demonstrates improved restoration quality, greater robustness, and lower inference cost relative to baselines.

Ablation and Analysis

Comprehensive studies analyze:

The impact of uncertainty-aware routing

The role of the MoE structure versus single-expert models

Sensitivity to loss weighting parameters

Performance under varying Gamma noise severity

Robustness to mixed multiplicative–additive noise

Results show that architectural design dominates performance, reducing reliance on heavy regularization or fine-tuned hyperparameters.

Why Implicit SDE?

Traditional score-based SDE models:

Require expensive reverse-time sampling

Are sensitive to discretization error

Struggle with multiplicative noise

GMiSDE-Net avoids these limitations by:

Eliminating the forward diffusion process

Learning the terminal mapping directly

Embedding uncertainty within the SDE parameterization

Intended Audience

This repository is intended for:

Researchers in image restoration and inverse problems

Practitioners working with SAR and ultrasound data

Students studying stochastic modeling in deep learning

Author

Vanapala Nikhil Varma
Mahindra University, Hyderabad

Research focus:
Stochastic differential equations, uncertainty-aware deep learning, and inverse imaging problems.
