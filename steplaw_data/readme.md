## **1、Structure of Profiling data**  
The data is stored in the steplaw/data directory. The data is stored in CSV format. The data is stored in the following format:
### directory

```yaml
data/
  ├── dense_lr_bs_loss.csv   # Smooth loss results for dense models
  │   
  └── moe_lr_bs_loss.csv     # Smooth loss results for MoE models
```

### information

| **file**               | **data_count per file** | **n_files** | **n_config** | **n_perf** |
|------------------------|-------------------------|-------------|--------------|------------|
| dense_lr_bs_loss.csv   | 1912                    | 1           | 11           | 2          |
| moe_lr_bs_loss.csv     | 709                     | 1           | 25           | 5          |


### dense_lr_bs_loss.csv

Here’s the columns for the dense model loss data, **Configurations** (user-defined parameters) and **Performance Metrics** (output/result metrics):

#### **1. Hyperparameters (User-Controlled Configurations)**  
These are variables set by the user before training to influence the optimization process.  

| Column Name | Data Type | Description                                                               |
|-------------|-----------|---------------------------------------------------------------------------|
| `h`         | Integer   | Transformer hidden dimension – architectural hyperparameter               |  
| `ffnh`      | Integer   | Feed-forward network hidden dimension  – architectural hyperparameter     |  
| `numh`      | Integer   | Number of attention heads  – architectural hyperparameter                 |  
| `numl`      | Integer   | Number of Transformer layers  – architectural hyperparameter              |  
| `lr`        | Float     | Learning rate  – optimization hyperparameter                              |  
| `bs`        | Integer   | Batch size – optimization hyperparameter                                  |  
| `exp_name`  | String    | Experiment identifier                                                     |  
| `D`         | Integer   | Total training data size – training setup hyperparameter                  |  
| `N`         | Integer   | Non-embedding parameters – model scale hyperparameter                     | 
| `D_N`       | Float     | Data-to-parameter ratio – derived metric for data sufficiency             | 
| `ti`        | Integer   | Training iterations – total steps completed (indicates training progress) |  

#### **2. Performance Metrics (Model/Training Outcomes)**  
These are results generated during training that reflect model performance

| Column Name   | Data Type | Description                                                                  |  
|---------------|-----------|------------------------------------------------------------------------------|
| `loss`        | Float     | Raw training loss (un-smoothed cross-entropy) – immediate performance metric |  
| `smooth_loss` | Float     | Smoothed training loss (EMA) – primary performance metric for convergence    |  

### moe_lr_bs_loss.csv

Here’s the columns for the MoE model loss data, **Configurations** (user-defined parameters) and **Performance Metrics** (output/result metrics):

---

#### **1. Hyperparameters (User-Controlled Configurations)**  

| Name                  | Data Type   | Description                                                    |
|-----------------------|-------------|----------------------------------------------------------------|
| `seq_len`             | Integer     | Input sequence length.                                         |
| `topk`                | Integer     | Number of top-K experts selected by the router.                |
| `nume`                | Integer     | Total number of experts in the MoE layer.                      |
| `moeh`                | Integer     | Hidden dimension size of the MoE layer.                        |
| `h`                   | Integer     | Base hidden dimension of the model.                            |
| `ffnh`                | Integer     | Hidden dimension of the Feed-Forward Network (FFN) layer.      |
| `numh`                | Integer     | Number of attention heads in the transformer.                  |
| `numl`                | Integer     | Total number of layers in the model.                           |
| `lr`                  | Float       | Learning rate for optimization.                                |
| `bs`                  | Integer     | Batch size during training.                                    |
| `ti`                  | Integer     | Target iteration count (or warmup iterations).                 |
| `exp_name`            | String      | Name/identifier of the experiment.                             |
| `moe_layer_enum_type` | String      | Type of MoE layer placement (e.g., alternating layers).        |
| `mfa_version`         | String      | Version of the MoE framework/library used.                     |
| `numld`               | Integer     | Number of local experts per device (for distributed training). |
| `Nattn`               | Integer     | Number of attention modules in the model.                      |
| `N`                   | Integer     | Non-embedding parameters – model scale hyperparameter          |
| `Na`                  | Integer     | Number of activated parameters.                                |
| `M`                   | Integer     | Memory allocation configuration.                               |
| `kvcache`             | Integer     | Key-Value cache configuration for attention.                   |
| `D`                   | Integer     | Dataset size                                                   |
| `moe_name`            | String      | Name of the MoE variant                                        |
| `Na/N`                | Float/Ratio | Activated parameters ratio – sparsity efficiency metric        |
| `D/N`                 | Float/Ratio | Dataset size to model parameter ratio.                         |
| `target_iter`         | Integer     | Planned total number of training iterations.                   |

---

#### **2. Performance Metrics (Model/Training Outcomes)**  

| Name                | Data Type       | Description                                  |
|---------------------|-----------------|----------------------------------------------|
| `loss`              | Float           | Training loss value.                         |
| `smooth_loss`       | Float           | Smoothed training loss (e.g., EMA-filtered). |
| `average_iter_time` | Float (seconds) | Average time per training iteration.         |
| `final_iter`        | Integer         | Actual number of completed iterations.       |
| `total_time`        | Float (hours)   | Total training time.                         |
 
---




