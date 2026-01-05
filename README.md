# Multivariate Time Series GNN (MTGNN) results
This folder contains results for trained MTGNN models for solar, traffic, electricity and exchange rate multivariate time series data, from original Wu et al. (2020) paper

### Implementation notes
We used the publicly available MTGNN (https://github.com/nnzhan/MTGNN) codebase as our training framework. No changes were made to model architectures or loss functions. However, we reduced the number of runs in train_single_step.py from 10 to 3 to speed up training of the initial baselines. We also used "--runs 3" in the multi-step training commands for METR-LA and PEMS-BAY. To resolve a tensor data type discrepancy, we changed the following line in both train_single_step.py and train_multi_step.py:

                #id = torch.tensor(id).to(device)
                id = torch.tensor(id, dtype=torch.long).to(device)

### Repo structure
```
MTGNN-results/
├── README.md
├── METR-LA/
│   └── model-metrla.ptexp1_0.pth
│   └── model-metrla.ptexp1_1.pth
│   └── model-metrla.ptexp1_2.pth
├── PEMS-BAY/
│   └── model-pemsbay.ptexp1_0.pth
│   └── model-pemsbay.ptexp1_1.pth
│   └── model-pemsbay.ptexp1_2.pth
├── electricity/
│   └── model-electricity-3.pt
|   └── model-electricity-sampling-3.pt
├── exchange-rate/
│   └── model-exchange-rate-3.pt
|   └── model-exchange-rate-sampling-3.pt
├── solar/
│   └── model-solar-3.pt
|   └── model-solar-sampling-3.pt
├── traffic/
│   └── model-traffic-3.pt
|   └── model-traffic-sampling-3.pt
└── requirements.txt
└── environment.yaml
```

### Environment
- Python:  3.7.1
- PyTorch: 1.2.0
- Device: CUDA (NVIDIA GTX 1060, 3GB)
- Conda environment exported in `environment.yaml`

### Results
#### Model: MTGNN (Wu et al., 2020)
- Configuration: single step
- Dataset: solar.txt
- Horizons: 3
- Batch size: 16
- Runs: 3
- Epochs/Run: 30
- Criterion: validation loss

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
- Dataset: solar.txt
- Horizons: 3
- Batch size: 16
- Runs: 3
- Epochs/Run: 30
- Criterion: validation loss

|   valid    | RSE       | RAE      | corr.      |
| ---------- | --------- | --------- | --------- |
| mean      |    0.2361  |  0.1246  |   0.9790   |
| std |    0.0008  |   0.0012  |   0.0002  |

|   test    | RSE       | RAE      | corr.      |
| ---------- | --------- | --------- | --------- |
| mean      |    0.1785  | 0.0858 |   0.9851   |
| std |    0.0004  |   0.0006  |   0.0001  |


#### Model: MTGNN (Wu et al., 2020)
- Configuration: single step 
- Dataset:  electricity.txt
- Horizons: 3
- Batch size: 16
- Runs: 3
- Epochs/Run: 30
- Criterion: validation loss

|   valid    | RSE       | RAE      | corr.      |
| ---------- | --------- | --------- | --------- |
| mean      |    0.0496  |  0.0348  |   0.9407   |
| std |    0.0002  |   0.0002  |   0.0003  |

|   test    | RSE       | RAE      | corr.      |
| ---------- | --------- | --------- | --------- |
| mean      |    0.0749  | 0.0417 |   0.9476   |
| std |    0.0003  |   0.0003  |   0.0003  |

#### Model: MTGNN (Wu et al., 2020)
- Configuration: multi step 
- Dataset: METR-LA
- Horizons: 12
- Batch size: 16
- Runs: 3
- Epochs/Run: 100
- Criterion: validation loss

|   valid    | MAE       | RMSE      | MAPE     |
| ---------- | --------- | --------- | --------- |
| mean      |    2.7548  |  5.7862  |   0.0774   |
| std |    0.0034  |   0.0265  |   0.0005  |

|   test / horizon   | MAE-mean       | RMSE-mean      | MAPE-mean      | MAE-std       | RMSE-std      | MAPE-std      |
| ---------- | --------- | --------- | --------- |--------- | --------- | --------- |
| 3      |    2.6803  | 5.1870 |   0.0691   | 0.0050 | 0.0202 |0.0004|
| 6      |    3.0441  | 6.1775|   0.0829   | 0.0015 | 0.0202 |0.0005|
| 12      |    3.4747  | 7.2334 |   0.0996   | 0.0078 | 0.0322 |0.0010|

#### Model: MTGNN (Wu et al., 2020)
- Configuration: multi step 
- Dataset: PEMS-BAY
- Horizons: 12
- Batch size: 16
- Runs: 3
- Epochs/Run: 100
- Criterion: validation loss

|   valid    | MAE       | RMSE      | MAPE     |
| ---------- | --------- | --------- | --------- |
| mean      |    1.5801  |  3.6220  |   0.0360   |
| std |    0.0042  |   0.0119  |   0.0002  |

|   test / horizon   | MAE-mean       | RMSE-mean      | MAPE-mean      | MAE-std       | RMSE-std      | MAPE-std      |
| ---------- | --------- | --------- | --------- |--------- | --------- | --------- |
| 3      |    1.3295  | 2.7979 |   0.0279   | 0.0033 | 0.0153 |0.0002|
| 6      |    1.6511  | 3.7422|   0.0372   | 0.0055 | 0.0203 |0.0001|
| 12      |    1.9491  | 4.5015 |   0.0460   | 0.0116 | 0.0332 |0.0001|

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
