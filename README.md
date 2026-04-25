# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date:  22.04.2026

### AIM:

To develop a Python program to analyze the given stock dataset using time series techniques.To apply transformations like differencing, log transformation, and seasonal decomposition on the closing price.

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.

### PROGRAM:

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

data = pd.read_csv("/content/TSLA.csv")

data['Date'] = pd.to_datetime(data['Date'])
data.set_index('Date', inplace=True)
target = 'Close'
data['diff'] = data[target] - data[target].shift(1)
data['diff'] = data[target] - data[target].shift(1)
result = seasonal_decompose(data[target], model='additive', period=30)
data['seasonal_diff'] = result.resid
data['log'] = np.log(data[target])

# 4. Log + Differencing
data['log_diff'] = data['log'] - data['log'].shift(1)

# 5. Seasonal Decomposition on Log Differenced Data
result = seasonal_decompose(data['log_diff'].dropna(), model='additive', period=30)
data['log_seasonal_diff'] = result.resid
plt.figure(figsize=(16,16))

plt.subplot(6, 1, 1)
plt.plot(data[target], label='Original', color='blue')
plt.legend()
plt.title('Original Stock Close Price')
plt.xlabel('Date')
plt.ylabel('Price')

# Regular Differencing
plt.subplot(6, 1, 2)
plt.plot(data['diff'], label='Regular Difference', color='orange')
plt.legend()
plt.title('Regular Differencing')

plt.subplot(6, 1, 3)
plt.plot(data['seasonal_diff'], label='Seasonal Adjustment', color='green')
plt.legend()
plt.title('Seasonal Adjustment (Residuals)')

# Log Transformation
plt.subplot(6, 1, 4)
plt.plot(data['log'], label='Log Transformation', color='red')
plt.legend()
plt.title('Log Transformation')

# Log + Differencing
plt.subplot(6, 1, 5)
plt.plot(data['log_diff'], label='Log + Differencing', color='purple')
plt.legend()
plt.title('Log Transformation + Differencing')

# Final Stationary Series
plt.subplot(6, 1, 6)
plt.plot(data['log_seasonal_diff'], label='Final Stationary Series', color='black')
plt.legend()
plt.title('Log + Diff + Seasonal Adjustment')

plt.tight_layout()
plt.show()
# Final Simple Plot
data[target].plot(figsize=(10,5), title="Stock Close Price Over Time")
plt.xlabel("Date")
plt.ylabel("Close Price")
plt.grid(True)
plt.show()

```

### OUTPUT:

## Original:

<img width="1289" height="311" alt="image" src="https://github.com/user-attachments/assets/db6fe93a-218e-4175-b038-aa947f1bb9c1" />

## REGULAR DIFFERENCING:

<img width="1566" height="342" alt="image" src="https://github.com/user-attachments/assets/010d7934-e61b-46f0-b89b-34684cf8ec77" />

## SEASONAL ADJUSTMENT:

<img width="1451" height="346" alt="image" src="https://github.com/user-attachments/assets/8af3e5c8-7800-47f5-92f0-a2ae683ba798" />

## LOG TRANSFORMATION:

<img width="1617" height="338" alt="image" src="https://github.com/user-attachments/assets/0a889d05-8cc7-4573-b9c2-d51b13bd3af0" />

<img width="1384" height="670" alt="image" src="https://github.com/user-attachments/assets/36743558-b38b-4692-852c-946cffd63692" />

### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
