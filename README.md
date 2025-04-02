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

---
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

## Discussion of parallel algorithms
### Differencing
### Autoregressive Coefficients 
### Moving Average Coefficients 
### Prediction


## Execution time comparison
- sequential and parallel columns for different array sizes
