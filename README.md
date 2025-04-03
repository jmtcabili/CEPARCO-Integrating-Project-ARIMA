# CEPARCO-Integrating-Project-ARIMA<br/>

Video Link: https://drive.google.com/file/d/1k_ROdRdcEJVyEAHaBX1JD_p-4cUJKM2W/view?usp=sharing

## Screenshot of execution

The dataset used for verifying execution was obtained from: https://www.kaggle.com/code/prashant111/arima-model-for-time-series-forecasting/notebook 

### Differencing
<b>First 10 Output Elements:</b><br/>
  The first 10 elements of the differencing function is displayed. The python output only uses basic function like for loops to obtain the the difference. The CUDA output uses a basic for loop as well with the addition of spreading the workload to multiple threads for faster completion. The two images below showcase that both methods of calculating for the difference arrive at the same desired output.

- Python Output (Sequential): <br/>
  <img width="200" alt="image" src="https://github.com/user-attachments/assets/4c4b0989-25f8-47c7-b782-b9d5d7e431d1" />
  
- CUDA Output (Parallel): <br/>
  <img width="200" alt="image" src="https://github.com/user-attachments/assets/36199c0a-4968-4d4e-9ff0-594bc41a0a0a" />

### Autoregressive Coefficients 
- Finding the Autoregressive Coefficients of the ARIMA Model through Ordinary Least Squares (OLE)
- As seen in the different cases below, the  

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
From a simple sequential differencing loop, where the difference between consecutive elements is computed one by one in Python, the program was converted into a parallel algorithm using CUDA. In the CUDA version, a kernel is launched that assigns many GPU threads to perform the differencing operation concurrently. By taking advantage of the Single Instruction, Multiple Thread architecture of CUDA, each thread computes the difference for a specific array element, determined by its unique block and thread indices, and uses a stride to cover multiple elements if necessary. This approach, combined with unified memory management and prefetching, efficiently distributes the workload across thousands of threads on the GPU, significantly accelerating the computation compared to the sequential CPU-based implementation.
### Autoregressive Coefficients 

According to [1], the coefficients to an Autoregressive Model can be estimated via ordinary least squares. The derived solution can be expressed as: 

![image](https://github.com/user-attachments/assets/2430180d-3d45-4908-8eff-af960153e18f)

where φ is a (p+1) x 1 matrix which contains the coefficients of the autogressive model. As seen in the figure above, the solution involves multiple matrix operations such as transposition, inversion, and multiplication which CUDA should be able to handle well through proper thread, block, and grid allocation for parallel execution of operations. 

### Moving Average Coefficients 
The process of implementing Moving Average Coefficients combines the calculation of ordinary least squares and and residuals calculations looped over 5 to 10 times to get the moving average coefficients. 

In combination with the ordinary least squares following processes are parallelized: 
1. Getting Total Sums for Average 
2. Calculating Rate
3. Calculating first residuals
4. Calculating succeeding residuals 
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
### Autoregressive Coefficients 
Calculation of coefficients of the autoregressive model at p = 4 with different input sizes.

- Sequential<br>

  | Operation          | n = 10 | n = 100 | n = 1<<10 | n = 1<<20 | n = 1<<26 |
  |--------------------|--------|---------|-----------|-----------|-----------|
  | lagged            | 0.018   | 0.12    | 0.029     | 46.19     | 2246.49   |
  | mul, inv, trans   | 0.039   | 0.028   | 0.176     | 55.70     | 3283.11   |
  | **Total**         | 0.057   | 0.04    | 0.205     | 101.89    | 5529.60    |

- Parallel <br/>

  | Operation      | n = 10 | n = 100 | n = 1<<10 | n = 1<<20 | n = 1<<26 |
  |---------------|--------|---------|-----------|-----------|-----------|
  | matmulNaive   | 0.16   | 0.076   | 0.167     | 112.88    | 3856.87   |
  | lagged        | 0.09   | 0.1     | 0.05      | 0.36      | 22.89     |
  | inverse       | 0.11   | 0.059   | 0.2       | 0.059     | 0.026     |
  | transpose     | 0.06   | 0.065   | 0.03      | 0.53      | 33.59     |
  | transfer      | 0.01   | 0.01    | 0.03      | 0.34      | 22.25     |
  | **Total**     | 0.43   | 0.31    | 0.48      | 114.17    | 3935.63   |

- Speedup

  |          | n = 10 | n = 100 | n = 1<<10 | n = 1<<20 | n = 1<<26 |
  |----------|--------|---------|-----------|-----------|-----------|
  | speedup  | 0.12   | 0.13    | 0.43      | 0.89      | 1.41      |

  As seen in the tables above, parallelizing the Autoregressive coefficients computation can offer speedups in of up to 1.41 as the input dataset increases in magnitude. These speedups were achieved by parallelizing the matrix operations involved in computing the coefficients along with making use of memory management techniques in cuda such as memory advising and prefetching. However, the implementation failed to account for all penalties as there were still a few page faults that surfaced during the execution of some of the trials. 


## References
[1]C. Zaiontz, “Finding AR(p) coefficients using Regression,” Real-statistics.com, 2025. https://real-statistics.com/time-series-analysis/autoregressive-processes/finding-ar-coefficients-using-regression/ (accessed Apr. 03, 2025).





