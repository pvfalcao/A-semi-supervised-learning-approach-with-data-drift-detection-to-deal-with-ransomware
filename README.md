# Performance Analysis of Drift-Aware Semi-Supervised Learning for Ransomware Detection

This project contains code associated with a paper presented at IEEE SMC 2025 in October 2025 in Vienna, Austria, as well as a master’s thesis presented in August 2025 in Recife, Brazil. **These works investigates the performance of a semi-supervised model enhanced with an integrated data-drift detector** and compares it with several conventional artificial intelligence models on publicly available ransomware datasets.

**The proposed approach employs a wrapper method known as Rel-RASCO, combined with a Kolmogorov-Smirnov test mechanism**. The model’s performance is evaluated against baseline methods developed by the creators of the datasets. **The datasets**, as well as details regarding the configuration of these baseline models, including parameter choices and hyperparameters, **are available in the [Mendeley - Ransomware and User Samples for Training and Validating ML Models](https://data.mendeley.com/datasets/yhg5wk39kf/2) within their respective files**.


The repository is organized into folders, each containing the code corresponding to the specific dataset on which the models were trained and evaluated. Each dataset provides three metrics collected over 1-second intervals:

a) the total number of **short commands** where the response occurs within the same interval,

b) the total number of **TCP bytes** sent from the server to the client during **read operations**, and

c) the total number of **TCP bytes** sent from the client to the server during **write operations**.

In addition to the original 1-second intervals, the authors explored the effect of supplying the models with data aggregated into **larger time windows**. For this project, **we used non-overlapping windows ranging from 10 to 60 seconds**, ensuring that each aggregated sample corresponds to a distinct time segment with **no duplicate data.**

The datasets follow the naming pattern “NXSY”, where each character indicates a specific configuration parameter. **N denotes the window size, and X specifies its value, while S represents the slide window and Y its corresponding value**. For example, N10S10 indicates that each data instance corresponds to a 10-second window with a 10-second slide. 


To simulate the neural networks, the following parameters and hyperparameters were employed:


| **Model**                  | **Number of Nodes**     | **Activation** | **Optimizer** | **Dropout** | **Learning Rate** |
|----------------------------|--------------------------|----------------|---------------|-------------|--------------------|
| 1 hidden layer — 10 s      | 128                      | ReLU           | Adam          | 0.5         | 0.1%              |
| 2 hidden layers — 10 s     | 128 × 64                 | ReLU           | Adam          | 0.5         | 0.1%              |
| 3 hidden layers — 10 s     | 128 × 128 × 128          | ReLU           | Adam          | 0           | 0.5%              |
| 1 hidden layer — 20 s      | 64                       | Tanh           | Adam          | 0.5         | 0.1%              |
| 2 hidden layers — 20 s     | 64 × 64                  | Tanh           | Adam          | 0.5         | 0.1%              |
| 3 hidden layers — 20 s     | 128 × 64 × 32            | ReLU           | Adam          | 0           | 0.1%              |
| 1 hidden layer — 30 s      | 128                      | ReLU           | Adam          | 0.5         | 0.5%              |
| 2 hidden layers — 30 s     | 128 × 64                 | ReLU           | Adam          | 0.5         | 0.1%              |
| 3 hidden layers — 30 s     | 128 × 64 × 32            | ReLU           | Adam          | 0           | 0.1%              |
| 1 hidden layer — 40 s      | 64                       | Tanh           | Adam          | 0.5         | 0.1%              |
| 2 hidden layers — 40 s     | 64 × 64                  | Tanh           | Adam          | 0.5         | 0.1%              |
| 3 hidden layers — 40 s     | 128 × 64 × 32            | ReLU           | Adam          | 0           | 0.1%              |
| 1 hidden layer — 50 s      | 64                       | Tanh           | Adam          | 0.5         | 0.1%              |
| 2 hidden layers — 50 s     | 64 × 64                  | Tanh           | Adam          | 0.5         | 0.1%              |
| 3 hidden layers — 50 s     | 128 × 64 × 32            | ReLU           | Adam          | 0           | 0.1%              |
| 1 hidden layer — 60 s      | 64                       | Tanh           | Adam          | 0.5         | 0.1%              |
| 2 hidden layers — 60 s     | 64 × 64                  | Tanh           | Adam          | 0.5         | 0.1%              |
| 3 hidden layers — 60 s     | 128 × 64 × 32            | ReLU           | Adam          | 0           | 0.1%              |


To simulate the tree ensembles, the following parameters and hyperparameters were employed:

| **Parameter**               | **Value**                 |
|-----------------------------|---------------------------|
| Model                       | Bootstrap Decision Forest |
| Number of Classifiers       | 10-model                  |
| Type                        | Deterministic order       |
| Split Candidates            | 32                        |
| Sample Rate                 | 1.0                       |
| Node Threshold              | 512                       |
| Cost-Complexity Pruning     | 0.001                     |

## References
- [Relevant Random Subspace Co-training (Rel-RASCO)](https://www.sciencedirect.com/science/article/abs/pii/S0925231210001256)
- [Open Repository for the Evaluation of Ransomware Detection Tools](https://ieeexplore.ieee.org/abstract/document/9050526)
- [Crypto-ransomware detection using machine learning models in file-sharing network scenarios with encrypted traffic](https://www.sciencedirect.com/science/article/pii/S0957417422014312)
- [Frouros: An open-source Python library for drift detection in machine learning systems](https://www.sciencedirect.com/science/article/pii/S2352711024001043)
- [SSLearn: A Semi-Supervised Learning library for Python](https://www.sciencedirect.com/science/article/pii/S2352711024003947)


