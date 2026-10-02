# Self-Attentive Channel-Token Precoding for Multiuser Massive MIMO Downlink

This is the official implementation of **BeamTransformer** (paper under review; link and DOI will be added after publication).

## Overview

*BeamTransformer is a deep-learning precoder for the multi-user massive-MIMO downlink. Each user's estimated channel vector is embedded as one token, and an SNR conditioning token is prepended. A Pre-LN Transformer encoder then applies full self-attention across users, which lets the network coordinate inter-user interference directly. The user tokens are projected back to precoding vectors and power-normalised. The model is pre-trained on offline WMMSE targets and then trained end-to-end on the negative sum-rate under imperfect CSI. It is compared with classical beamformers (MRT, ZF, MMSE, WMMSE) and three deep-learning baselines (BlackboxFNN, IAIDNN, FNN-Zhang). An architecture ablation replaces the Transformer with MLPs to isolate the contribution of cross-user attention.*

## Repository Structure

```
Self-Attentive-Channel-Token-Precoding-for-Multiuser-Massive-MIMO-Downlink/
├── notebooks/
│   ├── 01_BeamTransformer_base.ipynb
│   ├── 02_BeamTransformer_baseline_comparison.ipynb
│   └── 03_BeamTransformer_merged_ablation.ipynb
├── requirements.txt
└── README.md
```

| Notebook | Description |
|---|---|
| `01_BeamTransformer_base.ipynb` | Channel simulator, classical beamformers, BeamTransformer training and evaluation suite (sum-rate / BER vs. SNR, beampatterns, antenna-count and CSI-quality ablations). |
| `02_BeamTransformer_baseline_comparison.ipynb` | Trains the DL baselines BlackboxFNN, IAIDNN and FNN-Zhang and compares them with BeamTransformer and WMMSE. |
| `03_BeamTransformer_merged_ablation.ipynb` | Final unified pipeline: dataset generation, one shared training protocol for every model, full evaluation, and the architecture ablation (BeamNet-UserMLP, FlatMLP). |

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/Aditto03/Self-Attentive-Channel-Token-Precoding-for-Multiuser-Massive-MIMO-Downlink.git
   ```
2. Go to the project directory:
   ```bash
   cd Self-Attentive-Channel-Token-Precoding-for-Multiuser-Massive-MIMO-Downlink
   ```
3. Install the dependencies:
   ```bash
   pip install -r requirements.txt
   ```
   For GPU training, install the CUDA build of PyTorch that matches your system (see [pytorch.org](https://pytorch.org/get-started/locally/)).

## Usage

Open a notebook and run it from top to bottom. All settings (Nₜ, K, dataset size, model and training hyperparameters, which models to run) are in the **Configuration** section near the top.

- **Google Colab:** results, checkpoints and the dataset cache are saved to Google Drive.
- **Local (Jupyter / VS Code):** results are saved to a run folder next to the notebook.
- Set `FAST = True` for a quick end-to-end demo with a small dataset and few epochs.

Each run saves plots (PNG), plot data (`.npz` + `.csv`), model checkpoints, a `run_params.txt` file and a Word report.

## Dataset

No external dataset is needed. The notebooks generate a geometry-based, spatially correlated multipath channel (ULA/UPA, L paths per user) with imperfect CSI from pilot-based estimation. Generated datasets, including the offline WMMSE labels, are cached and reused across runs. Default system: ULA, Nₜ = 32 transmit antennas, K = 8 single-antenna users, L = 5 paths per user.

## Results

Results will be added once the paper is published.

## References

- [B1] W. Xia, G. Zheng, Y. Zhu, J. Zhang, J. Wang, and A. P. Petropulu, "A deep learning framework for optimization of MISO downlink beamforming," *IEEE Trans. Commun.*, vol. 68, no. 3, pp. 1866–1880, 2020.
- [B2] Q. Hu, Y. Cai, Q. Shi, K. Xu, G. Yu, and Z. Ding, "Iterative algorithm induced deep-unfolding neural networks: Precoding design for multiuser MIMO systems," *IEEE Trans. Wireless Commun.*, vol. 20, no. 2, pp. 1394–1410, 2021.
- [B3] M. Zhang, J. Gao, and C. Zhong, "A deep learning-based framework for low complexity multiuser MIMO precoding design," *IEEE Trans. Wireless Commun.*, vol. 21, no. 12, pp. 11193–11206, 2022.
- [W] Q. Shi, M. Razaviyayn, Z.-Q. Luo, and C. He, "An iteratively weighted MMSE approach to distributed sum-utility maximization for a MIMO interfering broadcast channel," *IEEE Trans. Signal Process.*, vol. 59, no. 9, pp. 4331–4340, 2011.

## Copyright

Copyright (c) 2026 [Tarvir Anjum Aditto](https://github.com/Aditto03)

## Citation

If you find this work useful, please cite it. BibTeX (to be updated after publication):

```bibtex
@article{beamtransformer2026,
  title   = {Self-Attentive Channel-Token Precoding for Multiuser Massive MIMO Downlink},
  author  = {Aditto, Tarvir Anjum},
  journal = {Under review},
  year    = {2026}
}
```
