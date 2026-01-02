# MTGNN-results
This folder contains results for trained MTGNN models for solar, traffic, electricity and exchange rate data, from original Wu et al. (2020) paper

### Implementation notes
We used the publicly available MTGNN ([https://github.com/RWLinno/STUM](https://github.com/nnzhan/MTGNN)) codebase as our training framework. No changes were made to model architectures or loss functions. However, we reduced the number of runs in train_single_step.py from 10 to 3 to speed up training of the initial baselines.

### Files
- `model-solar-3.pt`: PyTorch checkpoint of the trained solar model
- `model-solar-3-sampling.pt`: PyTorch checkpoint of the trained solar model with sampling

### Environment
- Python:  3.7.1
- PyTorch: 1.2.0
- Device: CUDA (NVIDIA GTX 1060 3GB)
- Conda environment exported in `environment.yaml`

### Results
#### Model: MTGNN (Wu et al., 2020)
- Configuration: single step
- Dataset: Solar.txt
- Runs: 3
- Epochs: 30

|   valid    | RSE       | RAE      | corr.      |
| ---------- | --------- | --------- | --------- |
| mean      |    0.2324  |  0.1243  |   0.9797   |
| std |    0.0009  |   0.0003  |   0.0001  |

|   test    | RSE       | RAE      | corr.      |
| ---------- | --------- | --------- | --------- |
| mean      |    0.1750  | 0.0857 |   0.9858   |
| std |    0.0013  |   0.0006  |   0.0001  |

#### Model: MTGNN (Wu et al., 2020)
- Configuration: single step with sampling
- Dataset: Solar.txt
- Runs: 3
- Epochs: 30

|   valid    | RSE       | RAE      | corr.      |
| ---------- | --------- | --------- | --------- |
| mean      |    0.2361  |  0.1246  |   0.9790   |
| std |    0.0008  |   0.0012  |   0.0002  |

|   test    | RSE       | RAE      | corr.      |
| ---------- | --------- | --------- | --------- |
| mean      |    0.1785  | 0.0858 |   0.9851   |
| std |    0.0004  |   0.0006  |   0.0001  |

### References

The implementation for MTGNN (Wu et al.) is based on the KDD 2020 paper “Connecting the Dots: Multivariate Time Series Forecasting with Graph Neural Networks” (https://arxiv.org/abs/2005.11650), with the following citation:

```bibtex
@inproceedings{wu2020connecting,
  title={Connecting the dots: Multivariate time series forecasting with graph neural networks},
  author={Wu, Zonghan and Pan, Shirui and Long, Guodong and Jiang, Jing and Chang, Xiaojun and Zhang, Chengqi},
  booktitle={Proceedings of the 26th ACM SIGKDD international conference on knowledge discovery \& data mining},
  pages={753--763},
  year={2020}
}
```
