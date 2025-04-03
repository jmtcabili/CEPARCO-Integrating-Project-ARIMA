# CEPARCO-Integrating-Project-ARIMA

## Screenshot of execution
Include screenshots for excel, python, and CUDA. For differencing, no need excel
- include results only, focus on time comparisons later
- focus on correct answers across executions (excel, python, cuda)

The dataset used for verifying execution was obtained from: https://www.kaggle.com/code/prashant111/arima-model-for-time-series-forecasting/notebook 

### Differencing
<b>First 10 Output Elements:</b><br/>

- Python Output (Sequential): <br/>
  <img width="200" alt="image" src="https://github.com/user-attachments/assets/4c4b0989-25f8-47c7-b782-b9d5d7e431d1" />
  
- CUDA Output (Parallel): <br/>
  <img width="200" alt="image" src="https://github.com/user-attachments/assets/36199c0a-4968-4d4e-9ff0-594bc41a0a0a" />

### Autoregressive Coefficients 
- Finding the Autoregressive Coefficients of the ARIMA Model through Ordinary Least Squares (OLE) 

*Case 1: p=1* 
- Excel Output (LINTEST Result): <br/>
  <img width="216" alt="image" src="https://github.com/user-attachments/assets/de2dcb6d-13ee-454c-b925-3757a79484be" />

- Python Output (Sequential): <br/>
  <img width="200" alt="image" src="https://github.com/user-attachments/assets/c097fc1f-5e43-417c-bcfa-9f143140b93c" />
  
- CUDA Output (Parallel): <br/>
  <img width="336" alt="image" src="https://github.com/user-attachments/assets/c556122d-65f5-4994-b0fe-011d822c9340" />

*Case 2: p=2*
- Excel Output (LINTEST Result): <br/>
  <img width="287" alt="image" src="https://github.com/user-attachments/assets/ad12bb6d-fff1-46ca-af47-2cc4a73a96ee" />

- Python Output (Sequential): <br/>
  <img width="200" alt="image" src="https://github.com/user-attachments/assets/23aa3c4b-d070-4ce5-bbe8-69568b695bdb" />


- CUDA Output (Parallel): <br/>
  <img width="317" alt="image" src="https://github.com/user-attachments/assets/52eeae9c-b34f-4ec0-9e6f-d094284f7836" />

*Case 3: p=3*
- Excel Output (LINTEST Result): <br/>
  <img width="417" alt="image" src="https://github.com/user-attachments/assets/80fa1401-e14a-4ee2-84fe-a2c78861d370" />

- Python Output (Sequential): <br/>
  <img width="300" alt="image" src="https://github.com/user-attachments/assets/f2a7e274-3bc7-4afc-8335-c5dd55374ce1"/>
  
- CUDA Output (Parallel): <br/>
  <img width="274" alt="image" src="https://github.com/user-attachments/assets/4a08bdd5-dc85-460e-812c-e8a2feb67d83" />

*Case 4: p=4*
- Excel Output (LINTEST Result): <br/>
  <img width="500" alt="image" src="https://github.com/user-attachments/assets/d7641138-1082-470a-a13b-2d4700021f93" />

- Python Output (Sequential): <br/>
  <img width="300" alt="image" src="https://github.com/user-attachments/assets/93f9ccf0-4bd9-4033-83f4-a5cb2261295d" />

- CUDA Output (Parallel): <br/>
  <img width="282" alt="image" src="https://github.com/user-attachments/assets/ab63c87c-6d19-4f92-9696-d729a7184cb6" />




### Moving Average Coefficients 
### Prediction

---
## Discussion of parallel algorithms
### Differencing
### Autoregressive Coefficients 
### Moving Average Coefficients 
### Prediction

---
## Execution time comparison
### Differencing <br/>
- Sequential (in mS) <br/>
| Operation   | n = 10 | n = 100 | n = 1 << 10 | n = 1 << 20 |
  |------------|--------|---------|-------------|-------------|
  | differencing | 0.0392 | 0.328118 | 3.81056 | 3263.39383 |
  | **Total**  | **0.0392** | **0.328118** | **3.81056** | **3263.39383** |

- Parallel (in mS) <br/>
| Operation   | n = 10 | n = 100 | n = 1 << 10 | n = 1 << 20 |
  |------------|--------|---------|-------------|-------------|
  | differencing | 0.16681 | 0.12489 | 0.064381 | 1.1513 |
  | **Total**  | **0.16681** | **0.12489** | **0.064381** | **1.1513** |

- Speedup of Parallel compared to Sequential <br/>
| Operation   | n = 10 | n = 100 | n = 1 << 10 | n = 1 << 20 |
  |------------|--------|---------|-------------|-------------|
  | **Speedup**  | **0.2350** | **49.4022** | **1.1513** | **2834.5295** |


### Autoregressive Coefficients 
Calculation of coefficients of the autoregressive model at p = 4 with different input sizes.

- Sequential<br>

  | Operation          | n = 10 | n = 100 | n = 1<<10 | n = 1<<20 | n = 1<<26 |
  |--------------------|--------|---------|-----------|-----------|-----------|
  | lagged            | 0.12   | 0.13    | 0.08      | 46.19     | 2246.49   |
  | mul, inv, trans   | 0.36   | 0.38    | 0.176     | 52.26     | 3283.11   |
  | **Total**         | 0.48   | 0.51    | 0.26      | 98.45     | 5529.60    |

- Parallel <br/>

  | Operation      | n = 10 | n = 100 | n = 1<<10 | n = 1<<20 | n = 1<<26 |
  |---------------|--------|---------|-----------|-----------|-----------|
  | matmulNaive   | 0.16   | 0.076   | 0.167     | 112.88    | 3856.87   |
  | lagged        | 0.09   | 0.1     | 0.05      | 0.36      | 22.89     |
  | inverse       | 0.11   | 0.059   | 0.2       | 0.059     | 0.026     |
  | transpose     | 0.06   | 0.065   | 0.03      | 0.53      | 33.59     |
  | **Total**     | 0.42   | 0.30    | 0.45      | 113.83    | 3913.38   |

- Speedup

  |          | n = 10 | n = 100 | n = 1<<10 | n = 1<<20 | n = 1<<26 |
  |----------|--------|---------|-----------|-----------|-----------|
  | speedup  | 1.14   | 1.70    | 0.57      | 0.86      | 1.41      |


### Moving Average Coefficients 
### Prediction





