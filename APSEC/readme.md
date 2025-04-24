## **1、Structure of data**  
The profiling data is stored in the data/ directory. The data is stored in CSV format. The data is stored in the following format:
### directory
```yaml
data/
  ├── set 1 - aggregated results.csv   # set1: fixed top_p  aggregated: 4 class        
  |
  └── set 1 - initial results.csv    # initial: 13 task 
  |
  └── set 2 - aggregated results.csv   # set2: fixed temp
  |
  └── set 2 - initial results.csv 

```

### information

| **file**                          | **data_count per file** | **n_files** | **n_config** | **n_perf** |
|-----------------------------------|-------------------------|-------------|--------------|------------|
| set 1 - aggregated results.csv    | 730                     | 1           | 3            | 4          |
| set 1 - initial results.csv       | 730                     | 1           | 3            | 13         |
| set 2 - aggregated results.csv    | 406                     | 1           | 3            | 4          |
| set 2 - initial results.csv       | 406                     | 1           | 3            | 13         |


### **1. Hyperparameters (User-Controlled Configurations)**  
These are variables set by the user to influence the process.  


| name             | data type | description                                                                                                                                                     |
|------------------|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| temp             | numeric   | Temperature parameter for code generation in LLM.                                                                                                               |
| top_p            | numeric   | Nucleus sampling parameter for code generation in LLM, which selects tokens from the smallest set whose cumulative probability exceeds the given probability p. | 
| freq_pen         | numeric   | Frequency penalty parameter for code generation in LLM.                                                                                                         |
| pres_pen         | numeric   | Presence penalty parameter for code generation in LLM.                                                                                                          |

### **2. Performance Metrics (Model/Training Outcomes)**  

| name             | data type | description                                                                                 |
|------------------|-----------|---------------------------------------------------------------------------------------------|
| Correct          | integer   | The number of correctly generated code tasks out of 13 tasks.                               |
| Fail to generate | integer   | The number of tasks that failed to generate code out of 13 tasks.                           |
| Fail to execute  | integer   | The number of tasks that generated code but failed to execute out of 13 tasks.              |
| Fail unit tests  | integer   | The number of tasks that generated and executed code but failed unit tests out of 13 tasks. |
| Pi               | bool      | True or not the taski is run successfully                                                   |
